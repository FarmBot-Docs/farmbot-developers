---
title: "Message Broker Examples"
slug: "message-broker-examples"
excerpt: "Use Python to communicate directly with FarmBot"
---

* toc
{:toc}

These examples use concepts in [CeleryScript](/v6/Documentation/celery-script.md) and [Message Broker](/v6/Documentation/web-app/message-broker.md).


__send message:__

```python
import json
import paho.mqtt.publish as publish

# Inputs:
my_device_id = 'device_1'
# Never hardcode this value into a production application-
#  It may change without notice.
# Instead, use the URL found in the "mqtt" property of your auth token.
my_mqtt_host = 'brisk-bear.rmq.cloudamqp.com'
my_token = ''

# Prepare the Celery Script command.
message = {
    'kind': 'send_message',
    'args': {
        'message': 'Hello World!',
        'message_type': 'success'
    }
}

# Send the command to the device.
publish.single(
    'bot/{}/from_clients'.format(my_device_id),
    payload=json.dumps(message),
    hostname=my_mqtt_host,
    auth={
        'username': my_device_id,
        'password': my_token
        }
    )
```

Also see [FarmBot Python Examples](https://github.com/FarmBot-Labs/FarmBot-Python-Examples) on GitHub.

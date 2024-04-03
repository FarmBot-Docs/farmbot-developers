---
title: "Message Broker Examples"
slug: "message-broker-examples"
description: "Use Python to communicate directly with FarmBot"
---

These examples use concepts in [CeleryScript](../docs/celery-script.md) and [Message Broker](../docs/message-broker.md).

{%
include callout.html
type="info"
title="Authorization required"
content='To get the authorization token required in these examples (`TOKEN`), see [Authorization](authorization.md).'
%}

{%
include callout.html
type="info"
title="Libraries required"
content='The following examples require either the FarmBot Python library or the **Paho MQTT** library. To install, run `python -m pip install farmbot paho-mqtt` in the command line.'
%}

# Show FarmBot communications

Listen in on FarmBot's activities and requests made via Python or the FarmBot Web App frontend. Running this can be helpful while going through the rest of the examples. Included in all communications between FarmBot and the Web App are FarmBot status updates; reviewing the output from this example will show many of the data fields available to track in the next example.

## via Python
```python
import json
from datetime import datetime
import paho.mqtt.client as mqtt

# TOKEN = ...

def on_connect(client, *_args):
    # subscribe to all channels
    client.subscribe(f"bot/{TOKEN['token']['unencoded']['bot']}/#")
    print('connected')

def on_message(_client, _userdata, msg):
    print('-' * 100)
    # print channel
    print(f'{msg.topic} ({datetime.now().strftime("%Y-%m-%d %H:%M:%S")})\n')
    # print message
    print(json.dumps(json.loads(msg.payload), indent=4))

client = mqtt.Client()
client.username_pw_set(
    TOKEN['token']['unencoded']['bot'],
    password=TOKEN['token']['encoded'])
client.connect(TOKEN['token']['unencoded']['mqtt'])
client.on_connect = on_connect
client.on_message = on_message
client.loop_forever()
```
You should see a stream of status updates if your FarmBot is online. Type <Ctrl + C> to stop.

# Track specific data updates

## via FarmBot Python library
```python
import json
from farmbot import Farmbot

# TOKEN = ...

fb = Farmbot(json.dumps(TOKEN))

class MyHandler():
    def on_connect(self, bot, _mqtt_client): print('connected')
    def on_change(self, _bot, state):
        x = state['location_data']['position']['x'] or 0
        y = state['location_data']['position']['y'] or 0
        z = state['location_data']['position']['z'] or 0
        print(f'Current position: ({x:.2f}, {y:.2f}, {z:.2f})')
    def on_log(*args): pass
    def on_error(*args): pass
    def on_response(*args): pass

fb.connect(MyHandler())
```
You should see position reports if your FarmBot is online. Type <Ctrl + C> to stop.

## via Python
```python
import json
from datetime import datetime
import paho.mqtt.client as mqtt

# TOKEN = ...

def on_connect(client, *_args):
    # subscribe to the status channel
    client.subscribe(f"bot/{TOKEN['token']['unencoded']['bot']}/status")
    print('connected')

def on_message(_client, _userdata, msg):
    state = json.loads(msg.payload)
    x = state['location_data']['position']['x'] or 0
    y = state['location_data']['position']['y'] or 0
    z = state['location_data']['position']['z'] or 0
    print(f'Current position: ({x:.2f}, {y:.2f}, {z:.2f})')

client = mqtt.Client()
client.username_pw_set(
    TOKEN['token']['unencoded']['bot'],
    password=TOKEN['token']['encoded'])
client.connect(TOKEN['token']['unencoded']['mqtt'])
client.on_connect = on_connect
client.on_message = on_message
client.loop_forever()
```
You should see position reports if your FarmBot is online. Type <Ctrl + C> to stop.

{%
include callout.html
type="warning"
title="Rate limits in place"
content="If you plan on sending many messages (more than 10 messages within a 5 minute period), see the section titled [Send multiple messages](#send-multiple-messages)."
%}

# Send a single message

## via FarmBot Python library
```python
import json
from farmbot import Farmbot

# TOKEN = ...

fb = Farmbot(json.dumps(TOKEN))

class MyHandler():
    def on_connect(self, bot, _mqtt_client):
        print('connected')
        bot.send_message('Hello World!')
        print('message sent')

    def on_change(*args): pass
    def on_log(*args): pass
    def on_error(*args): pass
    def on_response(*args): pass

fb.connect(MyHandler())
```
You should see 'connected' and 'message sent' in the output. Type <Ctrl + C> to stop.

For a list of FarmBot commands available to the FarmBot Python library, see [the list of supported commands](https://github.com/FarmBot/farmbot-py?tab=readme-ov-file#supported-remote-procedure-calls).

## via Python
```python
import json
import paho.mqtt.publish as publish

# TOKEN = ...

# prepare the Celery Script command
message = {
    "kind": "rpc_request",
    "args": {
        "label": "abcdef"
    },
    "body": [{
        'kind': 'send_message',
        'args': {
            'message': 'Hello World!',
            'message_type': 'success'
        }
    }]
}

# send the command to the device
publish.single(
    f'bot/{TOKEN['token']['unencoded']['bot']}/from_clients',
    payload=json.dumps(message),
    hostname=TOKEN['token']['unencoded']['mqtt'],
    auth={
        'username': TOKEN['token']['unencoded']['bot'],
        'password': TOKEN['token']['encoded']
        }
    )
print('message sent')
```
You should see 'connected' and 'message sent' in the output.

For a list of Celery Script commands, see [the list of available nodes](../docs/celery-script/nodes.md#available-nodes).

# Send multiple messages

## via FarmBot Python library
```python
import json
from time import sleep
from threading import Thread
from farmbot import Farmbot

# TOKEN = ...

fb = Farmbot(json.dumps(TOKEN))

class MyHandler():
    def __init__(self, bot):
        self.bot = bot
        self.connected = False
    def on_connect(self, bot, _mqtt_client):
        print('connected')
        self.connected = True
    def on_change(*args): pass
    def on_log(*args): pass
    def on_error(*args): pass
    def on_response(*args): pass
    def disconnect(self):
        self.bot._connection.mqtt.disconnect()
        print('disconnected')
        print()

handler = MyHandler(fb)
Thread(target=fb.connect, name="thread", args=[handler]).start()
while not handler.connected:
    print('.', end='', flush=True)
    sleep(0.1)
handler.bot.send_message('Hello World!')
handler.bot.send_message('second message')
print('messages sent')
handler.disconnect()
```
You should see 'connected', 'messages sent', and 'disconnected' in the output.

## via Python
```python
import json
from time import sleep
import paho.mqtt.client as mqtt

# TOKEN = ...

# prepare the Celery Script command
def prepare_message(message):
  return {
      "kind": "rpc_request",
      "args": {
          "label": "abcdef"
      },
      "body": [{
          'kind': 'send_message',
          'args': {
              'message': message,
              'message_type': 'success'
          }
      }]
  }

client = mqtt.Client()
client.username_pw_set(
    TOKEN['token']['unencoded']['bot'],
    password=TOKEN['token']['encoded'])
client.connect(TOKEN['token']['unencoded']['mqtt'])
print('connected')
channel = f'bot/{TOKEN['token']['unencoded']['bot']}/from_clients'
client.publish(channel, json.dumps(prepare_message('Hello World!')))
client.publish(channel, json.dumps(prepare_message('second message')))
print('messages sent')
sleep(1)
client.disconnect()
print('disconnected')
```
You should see 'connected', 'messages sent', and 'disconnected' in the output.

# Additional FarmBot Python library examples:
 * [Move to coordinate and send message](https://github.com/FarmBot/farmbot-py/blob/main/example.py)
 * [Move FarmBot using keyboard inputs](https://github.com/FarmBot/farmbot-py/blob/main/example_threads.py)

# What's next?

 * [Web App API Examples](web-app-api-examples.md)

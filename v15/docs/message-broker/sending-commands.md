---
title: "Sending Commands"
slug: "sending-commands"
---

FarmBotJS wraps common MQTT and [CeleryScript](../celery-script.md) operations into a single module. This allows you to focus on controlling FarmBot without needing to understand the underlying protocols of the system.

Not every project is written in Javascript, however, and users occasionally wish to write their own wrapper libraries in a language of choice (Python, Ruby, Java etc...)

# Step 1: Understand the protocols

FarmBot uses MQTT for realtime data such as sending commands and getting live status updates. Before writing FarmBot control software, **knowledge of MQTT is required**.

We recommend HiveMQ's excellent ["MQTT Essentials" tutorial](http://www.hivemq.com/mqtt-essentials/) for developers who are new to MQTT.

# Step 2: Find required information

Before sending commands, you need the following information:

1. An API token
2. The device's ID (see `"bot"` claim of the API token)
3. The MQTT server host name (See `"mqtt"` claim of API token).

All of this information is provided by the API when you create an API token. Instructions for generating a token can be found [here](../web-app/rest-api.md#generating-an-api-token).

Here is an example token:

```json
{
  "token": {
    "unencoded": {
      ...
      "mqtt": "clever-octopus.rmq.cloudamqp.com",
      "bot": "device_36"
    },
    "encoded": "eyJ0eXAiOiJK.eyJzdWIiOiJlbGl.6YWJldGhAaGFu"
    ...
  }
}
```

In the token above, we can see the following:

 * The device ID is `device_36`. **This is your MQTT server username. You will also need to use this later.**
 * The API token is `eyJ0eX....NGE0`. **Use this as a password when logging into MQTT.**
 * The MQTT host is found in the `mqtt` property of your token. In this case, the MQTT server host is `clever-octopus.rmq.cloudamqp.com`. Your `mqtt` value may be different and host values *may change without notice*. Always grab this value from the token. **Never hard-code the `mqtt` host directly into application code**- it may change in the future without notice.

# Step 3: Subscribing to topics

{%
include callout.html
type="info"
title="What's a Topic?"
content="If the concepts of **publishing**, **subscribing** and **topics** are unfamiliar to you, please review MQTT protocol concepts. For brevity, we avoid explaining MQTT in the documentation.

We recommend HiveMQ's excellent [\"MQTT Essentials\" tutorial](http://www.hivemq.com/mqtt-essentials/) for developers who are new to MQTT."
%}

Now that you have all the required information we can subscribe to topics (listed below). In all these examples, you can replace `DEVICE_ID_HERE` with your actual device ID. In the example above, the device ID would be entered as `device_36`.

 * **bot/DEVICE_ID_HERE/from_clients**: This channel will receive inbound [RPC](https://en.wikipedia.org/wiki/Remote_procedure_call) requests that the device must process.
 * **bot/DEVICE_ID_HERE/from_device**: Responses to inbound RPC requests will be sent back to clients from this channel.
 * **bot/DEVICE_ID_HERE/status**: The bot's "state tree" is constantly updated on this channel. This will include information such as the X/Y/Z coordinates and the bot's sync status.
 * **bot/DEVICE_ID_HERE/logs**: Logs intended to be read by humans are sent here. This is identical to the "ticker" seen in the web app.

# Step 4: Publishing commands

{%
include callout.html
type="success"
title="See real-world examples"
content="A great way to see real-world FarmBot RPCs is to subscribe to the `/from_clients` channel while trying commands in the [Web App](https://my.farm.bot) interface. You can observe the format and content of different RPCs using a [desktop MQTT client](https://www.hivemq.com/blog/seven-best-mqtt-client-tools)."
%}

As mentioned above, commands are sent to the device via the `/from_clients` channel. These commands must be formatted as valid [CeleryScript](../../docs/celery-script.md). Conversely, responses from the device are viewable in the `/from_device` channel.

Subscribing to the `/status` channel allows developers to get a real-time view of the entire FarmBot OS state tree.

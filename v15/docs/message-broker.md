---
title: "Message Broker"
slug: "message-broker"
---

The FarmBot API provides an HTTP based [REST API](../docs/web-app/rest-api.md). HTTP follows a response-request format, which is great when you are explicitly looking for data. However, some interactions do not lend themselves well to a request/response pattern. For example, if FarmBot must perform an emergency stop, we do not want to constantly check the API for such a message. Instead, we wish to receive such messages as soon as they are created and without explicitly asking. Other use cases include remote procedure calls and real-time data syncing.

The **message broker** is a sub-component of the web API which provides another method of communication which satisfies this requirement. It is a specially configured instance of [RabbitMQ](https://www.rabbitmq.com) that serves the following functions:

 * Passes push notifications between users and devices (discussed below).
 * Passes background messages between server background workers.
 * Uses a set of custom authorization plugins (to prevent unauthorized use).

The broker accepts messages over a variety of channels, such as [AMQP](https://www.amqp.org), [MQTT](http://mqtt.org) and [WebSockets](https://developer.mozilla.org/en-US/docs/Web/API/WebSockets_API) (discussed later in this document).

# Realtime control

One place where HTTP fails to be an adequate solution is remote procedure calls. If FarmBot _only_ used HTTP as a communication mechanism, a device would be forced to perform long polling and constantly make HTTP requests to the API for any new remote procedure calls. Polling would create tremendous scalability issues for the web app and provide a sub-par real-time experience for users.

With a real-time message broker, there is no need to check for new messages. Messages (such as a user clicking the "move" button on the [frontend](../docs/web-app/frontend.md)) can be sent back and forth between client, device and server without initiating a request.

**In many ways, the message broker acts as a machine-to-machine chat application.** Any software package, whether it be the [REST API](../docs/web-app/rest-api.md), [FarmBot OS](../docs/farmbot-os.md) or a third-party script can send a message to any other entity that is currently connected to the message broker, with correct authorization of course.

![rpc diagram](_images/rpc_diagram.png)

# Data sync

The Web API will constantly upload data changes to the bot in real-time and without user intervention. This means that the user no longer needs to push the "sync" button after making changes in the [frontend](../docs/web-app/frontend.md).

As mentioned previously, the Web API cannot send outbound messages via HTTP, since the protocol only supports request/response communication. In the case of data updates, FarmBot does not know that data on the API has changed and as such, does not make a request to download the data.

The workaround for this problem is to _allow the Web API to send outbound messages via the message broker_. These messages are initiated in a background process on the Web API. The messages are sent over the message broker rather than HTTP. In this case, the Web API acts both as a web _server_ and a message broker _client_.

![data update diagram](_images/data_update_diagram.png)

# Logging in

A device or user may log in to the message broker using a username and password:

 * **Username:** Use the `"bot"` claim* of your [authorization token](../docs/web-app/rest-api.md#generating-an-api-token) as a username
 * **Password:** Use the `encoded` authorization token as a password. It is a very long string that contains two `.` characters in it. It is contained in the `encoded` property of your auth token.

**The specific login process will vary based on the communication channel used (see below).**

\*This [JWT claim](https://scotch.io/tutorials/the-anatomy-of-a-json-web-token) follows the format of `"device_<id>"` where `<id>` is the numeric ID of your FarmBot. After generating the authorization token, it will be visible on the `unencoded.bot` property of the token.

# Communication channels

As mentioned previously, the message broker is an instance of [RabbitMQ](https://www.rabbitmq.com). RabbitMQ supports multiple communication channels such as [AMQP](https://www.rabbitmq.com/tutorials/amqp-concepts.html), [WebSockets](https://www.rabbitmq.com/web-mqtt.html) and [MQTT](https://www.rabbitmq.com/mqtt.html).

## WebSockets

If you are attempting to connect to the message broker from a web browser, you will need to connect via **WebSockets**. This is a popular approach for developers that are:

 * Building custom user interfaces.
 * Building custom device control software.
 * Remotely debugging device issues in a browser.

The best way to connect to the broker via WebSockets is with [FarmBotPy](../python/intro.md) or [FarmBotJS](../docs/farmbot-js.md) (easy). Some advanced users may prefer to directly connect via [MQTT.js](https://github.com/mqttjs/MQTT.js), though this is not appropriate for any use case other than debugging.

## MQTT

If your application does not run in a browser, **MQTT** is the preferred connection mechanism. Examples:

 * Building a desktop application to control FarmBot
 * Building a server that provides supplemental features to the Web API

The client used depends heavily on the language of your application and personal preference. A list of MQTT client libraries is [available here](https://github.com/mqtt/mqtt.github.io/wiki/libraries). Please see the specific library documentation for specific instructions.

## AMQP

A third connection channel is **AMQP**. This is the channel used by [FarmBot OS](../docs/farmbot-os.md). We do not recommend the use of AMQP and reserve the right to make breaking changes to AMQP usage without notice. You should only use AMQP if you are directly modifying the FarmBot OS source code.

# What's next?

 * [Subscribing to Resource Updates](message-broker/realtime-updates-auto-sync.md)
 * [Sending Commands](message-broker/sending-commands.md)

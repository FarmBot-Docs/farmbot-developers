---
title: "Identifying Success and Failure"
slug: "identifying-success-and-failure"
---

* toc
{:toc}

Imagine writing a software package that sends a single `rpc_request` node once every five minutes. You could easily track the status of your RPC request by simply waiting for the next `rpc_ok` or `rpc_error` node from the device.

However, what if we are required to send 100 requests in a one-minute timeframe? Identifying success or failure is no longer a trivial task. This is especially true for operations that result in partial failure, where only a portion of the requests succeed.

When using the HTTP protocol, the solution is simple - open a connection, start a request, and then close the connection when finished. The situation is more complicated over MQTT, which is a persistent, session-based protocol where many requests are sent over the same TCP socket.

CeleryScript authors can solve this problem by tagging each outbound request with a unique `label` arg. You can think of this as a sort of request ID.

# Multiplexing requests with the label arg

FarmBot has the ability to send many commands over a single MQTT channel. Messages do not follow a call/response cycle seen with HTTP servers. Unlike HTTP, MQTT connections are persistent, full duplex connections. If you send three commands to a FarmBot, they might not come back in the order that they were received.


__Request order != response order:__

```text
     | BROWSER  Request "ABC"             DEVICE
     |        ------------------------->
     |          Request "DEF"
Time |        ------------------------->
     |          Request "GHI"
     |        ------------------------->
     |          Response to "DEF"
     |        <-------------------------
     v          Response to "ABC"
              <-------------------------
                Response to "GHI"
              <-------------------------
```

To make sense of which messages have been acknowledged, the `rpc_request`, `rpc_ok`, and `rpc_error` nodes all contain a `label` argument. The `label` serves as a unique identifier for a message. Assigning unique IDs to each RPC message allows re-assembly of message order on arrival.

In the case of an `rpc_error`, it allows us to specify not only that an error has occurred, but also *which command* caused the error to occur.

## Example

Here is an example of a `move_relative` command sent to a device over MQTT. First, a message is published to MQTT channel `/bot/device_123/from_clients`:

```json
{
  "kind": "rpc_request",
  "args": { "label": "adslkjhfalskdha" },
  "body": [
    { "kind": "move_relative", "args": { "x": 0, "y": 0, "z": 0, "speed": 100 } }
  ]
}
```

After some time the bot will respond on MQTT channel `/bot/device_123/from_device`:

```json
{
  "kind": "rpc_ok",
  "args": { "label": "adslkjhfalskdha" }
}
```

Notice that the `label` in the response matches the label in the request. When sending requests, any unique identifier can be used as a label. UUIDs are highly recommended.


# Out-of-band responses

Not every piece of data that FarmBot works with can be transmitted as CeleryScript. When an RPC creates data that is not formatted as CeleryScript, the response is said to be "out of band", meaning that it relays the information through a channel that does not support CeleryScript (typically the [REST API](../web-app/rest-api.md) or status channel on the [Message Broker](../../docs/message-broker.md)).

|              |                              |
|--------------|------------------------------|
|`take_photo`  |Creates an image resource in the [REST API](../web-app/rest-api.md) .
|`read_pin`    |Updates the bot state tree and broadcasts over the appropriate status channel on the [Message Broker](../../docs/message-broker.md).
|`read_status` |Forces the bot to re-transmit the entire status tree over the appropriate channel on the [Message Broker](../../docs/message-broker.md).
|`sync`        |Causes the bot to upload and download newly created resources on the [REST API](../web-app/rest-api.md).

{%
include callout.html
type="info"
title="This list is not exhaustive"
content="If you have questions about a specific RPC, please raise an issue on [Github](https://www.github.com/farmbot) or [the forum](https://forum.farmbot.org/)."
%}

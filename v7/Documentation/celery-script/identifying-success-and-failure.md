---
title: "Identifying Success and Failure"
slug: "identifying-success-and-failure"
---

Imagine writing a software package that sends a single `rpc_request` node once every five minutes. You could easily track the status of your RPC request by simply waiting for the next `rpc_ok`, `rpc_error` node from the device over MQTT.

How would we handle this situation if the software requirements changed? What if, instead of one request every five minutes, we are now required to send 100 requests in a one-minute timeframe? Identifying success or failure is no longer a trivial task. This is especially true for operations that result in partial failure, where only a portion of the requests succeed.

When using the HTTP protocol, the solution is simple- open a connection, start a request and then close the connection when finished. The situation is more complicated over MQTT, which is a persistent, session-based protocol where many requests are sent over the same TCP socket.

CeleryScript authors can solve this problem by tagging each outbound request with a unique `"label"` tag. You can think of this as a sort of request ID. We will investigate this `arg` in the next section.

# Solution: Multiplex requests via the "label" arg

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

To make sense of which messages have been acknowledged, the `rpc_request`, `rpc_ok` and `rpc_error` nodes all contain a `label` argument. The `label` serves as a unique identifier for a message. Assigning unique IDs to each RPC message allows re-assembly of message order on arrival.

In the case of an `rpc_error`, it allows us to specify not only that an error has occurred, but also *which command* caused the error to occur.

Here is an example of a `move_relative` command sent to a device over MQTT:


__move_relative RPC:__

```json
// Message published to MQTT channel:
// '/bot/device_123/from_clients'
{
    kind: "rpc_request",
    // Any unique identifier can be used as a label.
    // UUIDs are highly recommended.
    args: { label: "adslkjhfalskdha" },
    body: [
      { kind: "move_relative", args: { x: 0, y: 0, z: 0, speed: 100 } }
    ]
}
// ... after some time the bot will respond on MQTT channel `/bot/device_123/from_device`

{
    kind: "rpc_ok",
    // The "label" here matches the "label" of the move_relative request (shown above).
    args: { label: "adslkjhfalskdha" }
}
```


# What's next?

 * [Out-of-Band Responses](out-of-band-responses.md)

---
title: "Message Broker"
slug: "message-broker"
description: "List of message broker Python functions in the FarmBot Sidecar Starter Pack"
---

# listen(channel="#", duration=None, stop_count=1)

Listen for messages on the given channel for the given duration or until the given number of messages are received.

If no channel is provided, the command will listen across all channels.

If no duration is provided, the default duration for the channel type will be used. See [setting timeouts](../sidecar-starter-pack.md#configure-timeouts).

If a stop count greater than 1 is provided, the command will listen indefinitely until the stop count is reached, ignoring any duration or timeout values.

See [configuring verbosity](../sidecar-starter-pack.md#configure-function-output-verbosity) for output verbosity controls.

```python
# Listen for 5 seconds or until a message is received on any channel
fb.listen(duration=5)

# Listen for a message from the device
fb.listen("from_device")

# Listen until 3 messages are received on the logs channel
fb.listen("logs", stop_count=3)
```

# listen_for_status_changes(duration=None, stop_count=1, diff_only=True, info_path=None)

This is a special case of the `listen()` command that listens to the `status` channel and exposes additional options.

Listen for status changes from the device for the given duration or until the given number of messages are received.

The output is the **device state tree**. The device state tree contains numerous properties that are relevant to the device's operation. It is the same state tree seen in [FarmBotJS](https://github.com/FarmBot/farmbot-js/blob/main/src/interfaces.ts#L6-L25).

To capture the device state tree for use, see the [read_status() command](./configuration.md#read_statuspathnone).

```python
# Listen for 5 seconds or until a status change is received
fb.listen_for_status_changes(duration=5)

# Listen until 3 status changes are received, and only output the difference from the first status
fb.listen_for_status_changes(stop_count=3)

# Listen until 10 status changes are received, outputting only the info at the given path. Note: The reason for the status change may be different than the info requested.
fb.listen_for_status_changes(stop_count=10, diff_only=False, info_path="location_data.position")
```

# What's next?

 * [Configuration](./configuration.md)

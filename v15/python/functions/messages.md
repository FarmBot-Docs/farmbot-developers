---
title: "Messages"
slug: "messages"
description: "List of messaging Python functions in the FarmBot Python library"
---

# debug(message_str)

**Sends a log** with type `debug`.

```python
fb.debug("This just happened")
```

# send_message(message_str, message_type="info", channels=None)

**Sends a message** to the logs channel and optionally as a toast, email, or as synthesized spoken word.

- The first required parameter is the message, which may be either a string or a number.
- The second parameter is the log `type`, which is optional but must be one of the following string values: `assertion`, `busy`, `debug`, `error`, `fun`, `info`, `success`, `warn`.
- The third parameter is the log channel, which is optional but must be a list of channels that may include: `toast`, `email`, `espeak`.

```python
# Send an error message to the default logs channel:
fb.send_message("Movement failed.", message_type="error")

# Send a success message to the logs channel and by email:
fb.send_message("You've got mail!", message_type="success", channels=["email"])

# Compose and send a more complex message:
position = fb.get_xyz()
message = f"Movement failed. The FarmBot is currently at {position} and is not moving."
fb.send_message(message, message_type="error", channels=["toast"])
```

# log(message_str, message_type="info", channels=None)

Same as `send_message()`, but adds a log message directly to the API instead of through FarmBot OS over the message broker. The frontend will need to be refreshed to show this message in the browser.

# toast(message_str, message_type="info")

**Sends a message as a toast notification** and to the logs channel. Defaults to type `info` if no type is given.

```python
# Send a toast notification:
fb.toast("This is a toast")

fb.wait(1000)

# Send a toast notification with a different type:
fb.toast("I'll cheers to that", message_type="success")
```

# What's next?

 * [Movements](./movements.md)

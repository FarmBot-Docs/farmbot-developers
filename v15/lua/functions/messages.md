---
title: "Messages"
slug: "messages"
description: "List of messaging Lua functions in FarmBot OS"
---

# debug(message)

**Sends a log** with type `debug`.

```lua
debug("This just happened")
```

# send_message(type, message, channels?)

**Sends a message** to the logs channel and optionally as a toast, email, or as synthesized spoken word.

- The first required parameter is the log `type`, which must be one of the following string values: `assertion`, `busy`, `debug`, `error`, `fun`, `info`, `success`, `warn`.
- The second required parameter is the message, which may be either a string or a number.
- The third parameter is optional and can be a single string or an array of strings. The strings must be one of the following available channels: `toast`, `email`, `espeak`.

```lua
-- Send an error message to the default logs channel:
send_message("error", "Movement failed.")

-- Send a success message to the logs channel and by email:
send_message("success", "You've got mail!", "email")

-- Send a message to the logs channel and multiple other channels:
send_message("info", "All systems running.", {"toast", "espeak"})

-- Compose and send a more complex message:
local position = get_xyz()
local message = "Movement failed. " ..
                "The FarmBot is currently at (" ..
                position.x .. ", " ..
                position.y .. ", " ..
                position.z ..
                ") and is not moving."
send_message("error", message, {"toast", "email"})
```

# toast(message, type?)

**Sends a message as a toast notification** and to the logs channel. Defaults to type `info` if no type is given.

```lua
-- Send a toast notification:
toast("This is a toast")

wait(1000)

-- Send a toast notification with a different type:
toast("I'll cheers to that", "success")
```

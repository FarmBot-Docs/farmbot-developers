---
title: "Messages"
slug: "messages"
description: "List of messaging Lua functions in FarmBot OS"
---

# debug(message)

Send a log with type `debug`.

```lua
debug("This just happened")
```

# send_message(type, message, channels?)

Send a message to the logs channel and optionally as a toast, email, or as synthesized spoken word.

- The first required parameter is a log type, which is one of the following string values: `assertion`, `busy`, `debug`, `error`, `fun`, `info`, `success`, `warn`
- The second required parameter is the message, which may be either a string or a number.
- The third parameter is optional. It can be a single string or an array of strings. The strings must be one of the following: `ticker`, `toast`, `email`, `espeak`

```lua
-- Send a message to the default channel ("ticker"):
send_message("error", "Hello")

-- Send a message to a single channel:
send_message("success", "You've got mail!", "email")

-- Send a message to multiple channels:
send_message("info", "All systems running.", {"toast", "espeak"})
```

# toast(message, type?)

Send a message as a log and a toast notification. Defaults to type `info` if no type is given.

```lua
toast("This is a toast")
wait(2000)
toast("I'll cheers to that", "success")
```

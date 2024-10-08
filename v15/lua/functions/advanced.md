---
title: "Advanced"
slug: "advanced"
description: "List of advanced Lua functions in FarmBot OS"
---

# sequence(id, variables?)

**Executes a subsequence** with optional variables.

```lua
-- Execute a subsequence without variables
subsequence = variable("Subsequence")
sequence(subsequence.id)
```

```lua
-- Execute a subsequence that has a number variable named "time"
subsequence = variable("Subsequence")
sequence(subsequence.id, {
 time = {
   kind = "numeric",
   args = { number = 1500 } }
})
```

```lua
-- Execute a subsequence that has a text variable named "time in ms"
subsequence = variable("Subsequence")
variable = {}
variable["time in ms"] = {
  kind = "numeric",
  args = { number = 1500 }
}
sequence(subsequence.id, variable)
```

# rpc()

**Wraps a CeleryScript node into an `rpc_request` and executes it**.

```lua
command = {
 kind = "wait",
 args = {
   milliseconds = 500
 }
}

rpc(command)
```

{%
include callout.html
type="info"
title="Using CeleryScript from the sequence editor"
content='You can use the **[VIEW CELERYSCRIPT](https://software.farm.bot/docs/sequences#sequence-editor-options)** option in the sequence editor to view the shape of raw CeleryScript nodes for the basic commands. However, you cannot perform a straight copy/paste into a Lua command - you will need to remove quotes from keys (eg: `"kind"` must be written as `kind`) and change colons to equal signs (`:` to `=`).'
%}

# cs_eval(celeryscript_ast)

**Executes arbitrary CeleryScript nodes**.

{%
include callout.html
type="warning"
content='In most cases, you should use the [`rpc()`](#rpc) function instead of `cs_eval()`. Using `cs_eval()` without properly wrapping the command into an `rpc-request` is not recommended and will likely not work.'
%}

```lua
cs_eval({
  kind = "rpc_request",
  args = {
    label = "example",
    priority = 500
  },
  body = {
    {
      kind = "move_absolute",
      args = {
        location = {kind = "coordinate", args = {x = 2, y = 2, z = 2}},
        offset = {kind = "coordinate", args = {x = 0, y = 0, z = 0}},
        speed = 100
      }
    }
  }
})
```

```lua
-- Execute a subsequence
subsequence = variable("Subsequence")
cs_eval(subsequence)
```

# gcode(command, params)

**Sends raw G code to the Farmduino**. No validations will be applied. The function will block the calling process until a response is received from the firmware.

```lua
-- Send "G00 X1.23 Y4.56 Z7.89" to the Farmduino
gcode("G00", { X = 1.23, Y = 4.56, Z = 7.89 })
```

{%
include callout.html
type="danger"
content="A `Q` param will implicitly be added by FarmBot OS. Do not explicitly set the `Q` value; it will cause FBOS to crash."
%}

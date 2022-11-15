---
title: "Variables"
slug: "variables"
description: "List of variable Lua functions in FarmBot OS"
---

# variable(name)

If the sequence executing the <span class="fb-step fb-lua">Lua</span> command contains a [sequence variable](https://software.farm.bot/docs/variables), you can access its content by calling the `variable(name)` function:

```lua
-- Assumes you are inside of a function that has a variable:
x_pos = variable("parent").x
send_message("info", x_pos, {"toast"});
```
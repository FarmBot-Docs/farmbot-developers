---
title: "Variables"
slug: "variables"
description: "List of variable Lua functions in FarmBot OS"
---

# variable(name)

**Gets a [sequence variable](https://software.farm.bot/docs/variables) by name**. Sequence variables can be of type `Location` (Plant, Weed, Point, or Tool), `Number`, `Text`, or `Resource` (Sequence, Peripehral, or Sensor).

{%
include callout.html
type="info"
content="The <span class='fb-step fb-lua'>Lua</span> command will only be able to access sequence variables that belong to its parent sequence. To access variables from a grandparent, you must pass them into the direct parent sequence by using [externally defined](https://software.farm.bot/docs/externally-defined-variables) variables in the parent sequence."
%}

```lua
-- Get the value of the variable named "Location 1"
location = variable("Location 1")

-- Print the location variable's X, Y, and Z coordinates
toast("The location variable is set to: (" .. location.x .. ", " .. location.y .. ", " .. location.z .. ")")
```

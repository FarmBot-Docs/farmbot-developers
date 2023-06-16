---
title: "Tools"
slug: "tools"
description: "List of tool Lua functions in FarmBot OS"
---

# dismount_tool()

**Dismounts the currently mounted tool** into it's assigned slot, taking into account the slot's direction.

{%
include callout.html
type="info"
content="This function only applies to FarmBots with interchangeable tools, such as FarmBot Genesis."
%}

```lua
-- Dismount the currently mounted tool
dismount_tool()

-- It is recommended to find home after dismounting tools
-- to stage FarmBot for future operations
find_home()
```

# dispense(mL, params?)

**Dispenses the given amount of liquid in milliliters**. The `params` argument is optional and can be used to override the default `tool_name` of "Watering Nozzle" and the default `pin` of `8`.

```lua
-- Dispense 100 mL of water using the default "Watering Nozzle" tool operated by pin 8
dispense(100)
```

```lua
-- Dispense 200 mL of fertilizer using a custom tool named "Fertigator" operated by pin 7
dispense(200, {tool_name = "Fertigator", pin = 7})
```

# mount_tool(tool)

**Mounts the given tool** and pulls it out of its slot, taking into account the slot's direction.

{%
include callout.html
type="info"
content="This function only applies to FarmBots with interchangeable tools, such as FarmBot Genesis."
%}

```lua
-- It is recommended to find home before mounting tools
-- to ensure accuracy of movements
find_home()

-- Add a Location variable named "Tool" to the sequence
-- and select the tool you wish to mount
tool = variable("Tool")

-- Because tools themselves do not have coordinates, FarmBot
-- will look up which slot the chosen tool has been assigned
-- to and use the slot's coordinates in the mount_tool() function
mount_tool(tool)
```

To mount a specific tool without using variables, fetch the tool from the FarmBot API using its ID:

```lua
-- The ID for the tool you wish to mount
tool_id = 1

-- Fetch the tool from the API
tool = api({method = "get", url = "/api/tools/" .. tool_id})

-- Mount the tool
mount_tool(tool)
```

Alternatively, simply specify a tool name:

```lua
-- Mount a tool by name
mount_tool("My Tool")
```

# verify_tool()

**Verifies if a tool is mounted to the UTM** by checking the UTM's tool verification pin as well as the **MOUNTED TOOL** field in FarmBot's state tree. Returns `true` if a tool is mounted or `false` if no tool is mounted.

{%
include callout.html
type="info"
content="This function only applies to FarmBots with interchangeable tools, such as FarmBot Genesis."
%}

{%
include callout.html
type="info"
content="The `verify_tool()` functionality is built-in to the `mount_tool()` and `dismount_tool()` helpers."
%}

```lua
-- Exit sequence if tool verification fails (no tool)
if not verify_tool() then
  return
end
```

# water(plant)

**Moves to and waters the given plant** based on its age and assigned watering curve.

{%
include callout.html
type="info"
content="A plant's `age` is calculated from its `planted_at` date and the current date. If a plant's `planted_at` date is not set, try changing the plant's **STATUS** to _Planted_ from the frontend."
%}

{%
include callout.html
type="info"
content="If using a FarmBot with interchangeable tools, such as FarmBot Genesis, you will need to first mount the watering tool before using the `water()` function."
%}

```lua
-- Get the "Plant" variable from the sequence
plant = variable("Plant")

-- Water the plant based on its age and watering curve
water(plant)
```

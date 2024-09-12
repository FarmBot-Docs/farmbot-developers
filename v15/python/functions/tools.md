---
title: "Tools"
slug: "tools"
description: "List of tool Python functions in the FarmBot Python library"
---

# dismount_tool()

**Dismounts the currently mounted tool** into it's assigned slot, taking into account the slot's direction.

{%
include callout.html
type="info"
content="This function only applies to FarmBots with interchangeable tools, such as FarmBot Genesis."
%}

```python
# Dismount the currently mounted tool
fb.dismount_tool()

# It is recommended to find home after dismounting tools
# to stage FarmBot for future operations
fb.find_home()
```

# mount_tool(tool_name)

**Mounts the given tool** and pulls it out of its slot, taking into account the slot's direction.

{%
include callout.html
type="info"
content="This function only applies to FarmBots with interchangeable tools, such as FarmBot Genesis."
%}

```python
# It is recommended to find home before mounting tools
# to ensure accuracy of movements
fb.find_home()

# Because tools themselves do not have coordinates, FarmBot
# will look up which slot the chosen tool has been assigned
# to and use the slot's coordinates in the mount_tool() function
fb.mount_tool("Seeder")
```

# dispense(milliliters, tool_name=None, pin=None)

**Dispenses the given amount of liquid in milliliters**. Defaults to using the "Watering Nozzle" tool, its **WATER FLOW RATE (ML/S)** value, and the solenoid valve operated by pin `8`.

```python
# Dispense 100 mL of water using default values
fb.dispense(100)
```

The `tool_name` and `pin` arguments are optional and can be used to override the default `tool_name` (and therefore the **WATER FLOW RATE (ML/S)** value) as well as which `pin` to operate.

```python
# Dispense 200 mL of fertilizer using a custom tool operated by pin 7
fb.dispense(200, tool_name="Custom Watering Nozzle 2", pin=7)
```

```python
# Dispense 300 mL of water with the standard "Watering Nozzle" tool, but using a solenoid valve operated by pin 10
fb.dispense(300, pin=10)
```

{%
include callout.html
type="info"
content='In order to add a **WATER FLOW RATE (ML/S)** value to a tool, the tool name must contain "Watering Nozzle" in the name.
![water flow rate](_images/water_flow_rate.png)'
%}

# water(plant_id, tool_name=None, pin=None)

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

{%
include callout.html
type="info"
content="Manually find a plant's ID by navigating to the plant in the web app and copying the number at the end of the URL."
%}

```python
# Water the plant based on its age and watering curve
fb.water(plant_id=123)
```

Under the hood, the `water()` function makes a call to `dispense()`. If provided, the `tool_name` and `pin` arguments will be passed into the `dispense` call to override its default values. See the [dispense() docs](#dispensemilliliters-tool_namenone-pinnone) for more information.

```python
# Water the plant based on its age and watering curve, using a solenoid valve operated by pin 10
fb.water(plant_id=123, pin=10)
```

# What's next?

 * [Time](./time.md)

---
title: "Movements"
slug: "movements"
description: "List of movement Lua functions in FarmBot OS"
---

# go_to_home(axis?)

**Moves to the home (0) position** of a given axis.

```lua
-- Go to home for a single axis:
go_to_home("x")
go_to_home("y")
go_to_home("z")

-- Go to home for every axis in the order Z, Y, X:
go_to_home()
go_to_home("all")
```

# move{args}

**Moves to an absolute coordinate position or by a relative offset**, where all arguments are optional.

* When an `x`, `y`, or `z` coordinate is omitted, the current position along that axis will be maintained unless an `offset` is provided for that axis.
* An optional `offset` table with `x`, `y`, and/or `z` values adds offsets in millimeters to the target coordinates. For an axis with an absolute coordinate, the offset is added to that coordinate. For an axis without an absolute coordinate, the offset is added to the current position.
* An optional `speed` argument will modify the speed of the movement as a percentage of the maximum speed.
* An optional `safe_z` argument can be set to `true` to perform the movement in three steps: first, the Z axis will be moved to the **SAFE HEIGHT**, then the X and Y axes will be moved to their new position, and finally the Z axis will be moved to the new position. This is useful for avoiding collisions with plants.

{%
include callout.html
type="info"
content="This helper is essentially a character saving version of [move_absolute()](#move_absolutex-y-z-s)."
%}

```lua
-- Move to the new X, Y, and Z coordinates
move{x=100, y=200, z=-20}

-- Safe Z move to the new position, keeping X constant
move{y=0, z=-20, safe_z=true}

-- Move to the new X coordinate, keeping Y and Z constant
move{x=0}

-- Move to the new Y and Z coordinates, keeping X constant
move{y=100, z=-10}

-- Move to Y=100 at 10% speed
move{y=100, speed=10}

-- Move 10 mm along X and -5 mm along Z from the current position
move{offset={x=10, z=-5}}

-- Move to X=110 and Y=200, keeping Z constant
move{x=100, y=200, offset={x=10}}
```

An optional `grouping` string controls which axes move together. Axes within a group move simultaneously, and commas separate movement steps. For example, `"xy,z"` moves X and Y together, then Z; `"z,y,x"` moves each axis separately.

An optional `route` string controls the order of those groups:

|Route|Behavior|
|-----|--------|
|`"in_order"`|Preserves the order in `grouping`.
|`"high"`|Moves the group containing Z first when retracting toward Z=0, or last when extending away from Z=0.
|`"low"`|Moves the group containing Z first when extending away from Z=0, or last when retracting toward Z=0.

If either `grouping` or `route` is provided, the omitted value defaults to `"xyz"` or `"in_order"`, respectively. If neither is provided, the configured default axis order is used. Setting `safe_z=true` takes precedence over `grouping` and `route`.

```lua
-- Move Z first, then X and Y together
move{x=100, y=200, z=-20, grouping="z,xy", route="in_order"}
```

# move_absolute(x, y, z, s?)

**Move to an absolute coordinate position**. The single-table form also accepts all [move() arguments](#moveargs). These table arguments are not available in the positional `(x, y, z, s?)` form.

* An optional `speed` argument will modify the speed of the movement as a percentage of the maximum speed.
* An optional `safe_z` argument can be set to `true` to perform the movement in three steps: first, the Z axis will be moved to the **SAFE HEIGHT**, then the X and Y axes will be moved to their new position, and finally the Z axis will be moved to the new position. This is useful for avoiding collisions with plants.

```lua
-- Move to the new position
move_absolute(30.5, 75, -20)

-- Move to the new position at 25% of the max speed:
move_absolute(30.5, 75, -20, 25)

-- Safe Z move to the new position
move_absolute({
  x = 1.0,
  y = 20,
  z = 30,
  safe_z = true
})
```

# move_with_tool(params)

See [tools](tools.md#move_with_toolparams).

# find_axis_length(axis?)

**Determines the length of an axis** using stall detection, rotary encoders, or limit switch hardware.

```lua
-- Find the length of a single axis:
find_axis_length("x")
find_axis_length("y")
find_axis_length("z")

-- Find the length of every axis in the order Z, Y, X:
find_axis_length()
find_axis_length("all")
```

# find_home(axis?)

**Finds the home (0) position** for an axis using stall detection, rotary encoders, or limit switch hardware.

```lua
-- Find the home position of a single axis:
find_home("x")
find_home("y")
find_home("z")

-- Find the home position of every axis in the order Z, Y, X:
find_home()
find_home("all")
```

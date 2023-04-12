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

**Moves to an absolute coordinate position**, where all arguments are optional.

* When an `x`, `y`, or `z` coordinate is omitted, the current position along that axis will be maintained.
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
```

# move_absolute(x, y, z, s?)

**Move to an absolute coordinate position**.

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

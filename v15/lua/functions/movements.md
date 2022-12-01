---
title: "Movements"
slug: "movements"
description: "List of movement Lua functions in FarmBot OS"
---

# go_to_home(axis?)

Move to the `0` (home) position of a given axis.

```lua
-- Single axis:
go_to_home("x")
go_to_home("y")
go_to_home("z")

-- Every axis:
go_to_home("all")
go_to_home()
```

# move{args}

Moves to an absolute coordinate position, where all arguments are optional. When an `x`, `y`, or `z` coordinate is omitted, the current position along that axis will be maintained. This helper is essentially a character saving version of `move_absolute`.

```lua
-- Move absolute to the new X, Y, and Z coordinates
move{x=100, y=200, z=-20}

-- Safe Z move to the new position where the X coordinate stays constant
move{y=0, z=-20, safe_z=true}

-- Move to the new X coordinate, keeping Y and Z constant
move{x=0}

-- Move to the new Y and Z coordinates, keeping X constant
move{y=100, z=-10}

-- Move to Y=100 at 10% speed
move{y=100, speed=10}
```

# move_absolute(x, y, z, s?)

Move to an absolute coordinate position.

```lua
move_absolute(30.5, 75, -20)

-- Enable "Safe Z":
move_absolute({
  x = 1.0,
  y = 20,
  z = 30,
  safe_z = true
})

-- Modify speed as a percentage of max speed:
move_absolute({
  x = 0,
  y = 100,
  z = 0,
  speed = 25
})
```

# find_axis_length(axis?)

Determines the length of an axis using stall detection, rotary encoders, or limit switch hardware.

```lua
-- Single axis:
find_axis_length("x")
find_axis_length("y")
find_axis_length("z")

-- Every axis in the order Z, Y, X:
find_axis_length()
find_axis_length("all")
```

# find_home(axis?)

Finds the `0` (home) position for an axis using stall detection, rotary encoders, or limit switch hardware.

```lua
-- Single axis:
find_home("x")
find_home("y")
find_home("z")

-- Every axis in the order Z, Y, X:
find_home("all")
find_home()
```
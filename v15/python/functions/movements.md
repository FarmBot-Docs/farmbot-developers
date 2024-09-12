---
title: "Movements"
slug: "movements"
description: "List of movement Python functions in the FarmBot Python library"
---

# move(x=None, y=None, z=None, safe_z=None, speed=None)

**Moves to an absolute coordinate position**, where all arguments are optional.

* When an `x`, `y`, or `z` coordinate is omitted, the current position along that axis will be maintained.
* An optional `speed` argument will modify the speed of the movement as a percentage of the maximum speed.
* An optional `safe_z` argument can be set to `True` to perform the movement in three steps: first, the Z axis will be moved to the **SAFE HEIGHT**, then the X and Y axes will be moved to their new position, and finally the Z axis will be moved to the new position. This is useful for avoiding collisions with plants.

```python
# Move to the new X, Y, and Z coordinates
fb.move(x=100, y=200, z=-20)

# Safe Z move to the new position, keeping X constant
fb.move(y=0, z=-20, safe_z=True)

# Move to the new X coordinate, keeping Y and Z constant
fb.move(x=0)

# Move to the new Y and Z coordinates, keeping X constant
fb.move(y=100, z=-10)

# Move to Y=100 at 10% speed
fb.move(y=100, speed=10)
```

# find_axis_length(axis="all")

**Determines the length of an axis** using stall detection, rotary encoders, or limit switch hardware.

```python
# Find the length of a single axis:
fb.find_axis_length("x")
fb.find_axis_length("y")
fb.find_axis_length("z")

# Find the length of every axis in the order Z, Y, X:
fb.find_axis_length()
fb.find_axis_length("all")
```

# find_home(axis="all")

**Finds the home (0) position** for an axis using stall detection, rotary encoders, or limit switch hardware.

```python
# Find the home position of a single axis:
fb.find_home("x")
fb.find_home("y")
fb.find_home("z")

# Find the home position of every axis in the order Z, Y, X:
fb.find_home()
fb.find_home("all")
```

# What's next?

 * [Pins](./pins.md)

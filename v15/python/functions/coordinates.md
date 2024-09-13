---
title: "Coordinates"
slug: "coordinates"
description: "List of coordinate Python functions in the FarmBot Python library"
---

# check_position(coordinate, tolerance)

Returns `True` if the device is **within the tolerance range** of the provided coordinate.

```python
if fb.check_position({"x": 0, "y": 0, "z": 0}, 1.23):
  fb.toast("FarmBot is at the home position", "success")
else:
  fb.toast("FarmBot is not at the home position", "warn")
```

# garden_size()

Returns the `x`, `y`, and `z` of the **length, width, and height in mm of FarmBot's working volume** according to the **AXIS LENGTH** settings.

```python
size = fb.garden_size()
fb.toast(f"Length: {size['x']}mm")
fb.toast(f"Width: {size['y']}mm")
fb.toast(f"Height: {size['z']}mm")
```

# get_seed_tray_cell(tray_name, tray_cell)

Calculates the **coordinates of a seed tray cell**, such as `B3`, based on the cell label and the coordinates of the center of the seed tray. See the [Pick from Seed Tray featured sequence](https://my.farm.bot/app/shared/sequence/32) for an example.

```python
cell = fb.get_seed_tray_cell("Seed Tray", "B3")
cell_depth = 5

# Send message with cell info
fb.toast(f"Picking up seed from cell {tray_cell} ({cell.x, cell.y, cell.z - cell_depth})")

# Safe Z move to above the cell
fb.move(x=cell.x, y=ell.y, z=cell.z + 25, safe_z=True)
```

{%
include callout.html
type="info"
content="Tray ID lookups are cached. See [clearing the cache](../settings.md#clear-resource-cache)."
%}

# get_xyz()

Gets the current **x, y, and z coordinates** of the Farmfb.

```python
position = fb.get_xyz()
fb.toast(f"FarmBot's X coordinate is: {position['x']}")
```

# group(group_id=None)

Returns group info.

```python
group_info = fb.group(1234)
```

{%
include callout.html
type="info"
content="Find a group's ID by navigating to the group in the web app and copying the number at the end of the URL."
%}

# safe_z()

Returns the value of the **[SAFE HEIGHT](https://my.farm.bot/app/designer/settings?highlight=safe_height)** setting.

```python
# Display the current Safe Height
fb.toast(f"Safe Z Height: {fb.safe_z()}")

# Move FarmBot's Z-axis to the Safe Height
fb.move(z=fb.safe_z())
```

{%
include callout.html
type="info"
content="`safe_z()` on it's own does not initiate a movement, and it should not be confused with adding a `safe_z=True` argument to a `move` command."
%}

# What's next?

 * [Curves](./curves.md)

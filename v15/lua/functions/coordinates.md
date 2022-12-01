---
title: "Coordinates"
slug: "coordinates"
description: "List of coordinate Lua functions in FarmBot OS"
---

# coordinate(x, y, z)

Generate a coordinate for use in location-based functions such as `move_absolute` and `check_position`.

```lua
coordinate(1.0, 20, 30)
-- Returns:
-- {x = 1.0, y = 20,  z = 30}
```

# check_position(coord, tolerance)

`check_position(coordinate, tolerance)` returns `true` if the device is within the `tolerance` range of `coordinate`.

```lua
if check_position({x = 0, y = 0,  z = 0}, 1.23) then
  send_message("info", "FarmBot is at the home position")
end
```

```lua
home = coordinate(0, 0, 0)
if check_position(home, 0.5) then
  send_message("info", "FarmBot is at the home position")
end
```

# garden_size()

Returns a table with an `x` and `y` attribute represent the maximum length of the garden bed as determined by firmware config settings.

```lua
size = garden_size()
send_message("info", "Width: " .. size.y)
send_message("info", "Length: " .. size.x)
```

# get_seed_tray_cell(tray, cell)

Calculates the coordinates of a seed tray cell, such as **B3**, based on the cell label and the coordinates of the center of the seed tray. See the [Pick from Seed Tray featured sequence](https://my.farm.bot/app/shared/sequence/32) for an example.

```lua
tray = variable("Seed Tray")
cell_label = variable("Seed Tray Cell")
cell = get_seed_tray_cell(tray, cell_label)
cell_depth = 5

-- Send message with cell info
local cell_coordinates = " (" .. cell.x .. ", " .. cell.y .. ", " .. cell.z - cell_depth .. ")"
send_message("info", "Picking up seed from cell " .. cell_label .. cell_coordinates, "toast")

-- Safe Z move to above the cell
job("Moving to Seed Tray", 25)
move_absolute({
    x = cell.x,
    y = cell.y,
    z = cell.z + 25,
    safe_z = true
})
```

# get_xyz()

Returns a table with the current `x`, `y`, and `z` coordinates of the FarmBot.

```lua
position = get_xyz()
toast("FarmBot's X coordinate is: " .. position.x)
```

# group(id)

Given a group ID, returns a table of current group member IDs, sorted by the group's **SORT BY** method.

```lua
group_members = group(1234)
for i,member in ipairs(group_members) do
    plant = api({
        method = "get",
        url = "/api/points/" .. member
    })
    move_absolute(plant.x, plant.y, 0)
end
```

{%
include callout.html
type="info"
content="Find a group's ID by navigating to the group in the web app and copying the number at the end of the URL."
%}

# safe_z()

Returns the value of the **[SAFE HEIGHT](https://my.farm.bot/app/designer/settings?highlight=safe_height)** setting. Note that `safe_z()` on it's own does not initiate a movement, and it should not be confused with adding a `safe_z=true` argument to a `move` or `move_absolute` command.

```lua
-- Move FarmBot's Z-axis to the Safe Height
move{z=safe_z()}
```

# soil_height(x, y)

Given an X and Y coordinate, returns a best-effort estimate of the Z axis height of the soil. This function requires at least 3 soil height measurements. When there are less than 3 measurements available, it will return the SOIL HEIGHT setting from the device settings page.

```lua
x = 10
y = 29
my_soil_height = soil_height(x, y)
send_message("info", "Distance to soil at (10, 29): " .. inspect(my_soil_height))
-- => "Distance to soil at (10, 29): -409.84"
```

# sort(points, method)

Sorts the given table of points using the chosen sorting method.

```lua
points = group(1234)
sorted_points = sort(points, "xy_alternating")
send_message("info", "Second point ID is: " .. sorted_points[2])
```

The following sorting methods are available. See [point group sorting](../../other/how-it-works/point-group-sorting.md) for additional details.

- `xy_ascending`
- `yx_ascending`
- `xy_descending`
- `yx_descending`
- `xy_alternating`
- `yx_alternating`
- `nn` (Nearest Neighbor)
- `random`
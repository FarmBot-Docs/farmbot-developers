---
title: "Coordinates"
slug: "coordinates"
description: "List of coordinate Lua functions in FarmBot OS"
---

# coordinate(x, y, z)

**Generates a coordinate** for use in location-based functions such as `move_absolute` and `check_position`.

```lua
coordinate(1.0, 20, 30)
-- Returns {x = 1.0, y = 20,  z = 30}
```

# check_position(coordinate, tolerance)

Returns `true` if the device is **within the tolerance range** of the provided coordinate.

```lua
if check_position({x = 0, y = 0,  z = 0}, 1.23) then
  toast("FarmBot is at the home position", "success")
else
  toast("FarmBot is not at the home position", "warn")
end
```

```lua
home = coordinate(0, 0, 0)
if check_position(home, 0.5) then
  toast("FarmBot is at the home position", "success")
else
  toast("FarmBot is not at the home position", "warn")
end
```

# garden_size()

Returns a table with an `x` and `y` attribute representing the **length and width of the garden bed** in mm as determined by firmware config settings.

```lua
size = garden_size()
toast("Length: " .. size.x .. "mm")
toast("Width: " .. size.y .. "mm")
```

# get_seed_tray_cell(tray, cell)

Calculates the **coordinates of a seed tray cell**, such as `B3`, based on the cell label and the coordinates of the center of the seed tray. See the [Pick from Seed Tray featured sequence](https://my.farm.bot/app/shared/sequence/32) for an example.

```lua
tray = variable("Seed Tray")
cell_label = variable("Seed Tray Cell")
cell = get_seed_tray_cell(tray, cell_label)
cell_depth = 5

-- Send message with cell info
local cell_coordinates = " (" .. cell.x .. ", " .. cell.y .. ", " .. cell.z - cell_depth .. ")"
toast("Picking up seed from cell " .. cell_label .. cell_coordinates)

-- Safe Z move to above the cell
move_absolute({
    x = cell.x,
    y = cell.y,
    z = cell.z + 25,
    safe_z = true
})
```

# get_xyz()

Gets the current **x, y, and z coordinates** of the FarmBot.

```lua
position = get_xyz()
toast("FarmBot's X coordinate is: " .. position.x)
```

# group(id)

Returns a table of **current group member IDs**, sorted by the group's **SORT BY** method.

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

Returns the value of the **[SAFE HEIGHT](https://my.farm.bot/app/designer/settings?highlight=safe_height)** setting.

```lua
-- Display the current Safe Height
toast("Safe Z Height: " .. safe_z())

-- Move FarmBot's Z-axis to the Safe Height
move{z=safe_z()}
```

{%
include callout.html
type="info"
content="`safe_z()` on it's own does not initiate a movement, and it should not be confused with adding a `safe_z=true` argument to a `move` or `move_absolute` command."
%}


# soil_height(x, y)

Given an X and Y coordinate, returns a best-effort estimate of the **Z axis height of the soil**.

```lua
x = 100
y = 300
soil_height = soil_height(x, y)
toast("Distance to soil at (" .. x .. ", " .. y .. "): " .. soil_height)
```

{%
include callout.html
type="info"
content="This function requires at least 3 soil height measurements. When there are less than 3 measurements available, it will return the **SOIL HEIGHT** setting from the device settings page."
%}

# sort(points, method)

**Sorts** the given table of points using the chosen **sorting method**.

```lua
points = group(1234)
sorted_points = sort(points, "xy_alternating")
toast("Second point ID is: " .. sorted_points[2])
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
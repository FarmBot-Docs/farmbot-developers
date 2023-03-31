---
title: "Curves"
slug: "curves"
description: "List of curve Lua functions in FarmBot OS"
---

Water, spread, and height curves can be assigned to plants from the plant details panel in the FarmBot web app. Curve IDs can be retrieved in Lua from the `water_curve_id`, `spread_curve_id`, or `height_curve_id` attributes of a plant (point) object. The curve ID can be used to get a curve object, which can then be used to get the curve value for a given day, usually based on the plant's current age.

# get_curve(id)

Gets a curve object by its ID.

```lua
-- Get plant object from sequence variable
local plant = variable("Plant")

if plant.water_curve_id then
    -- Get water curve object
    local water_curve = get_curve(plant.water_curve_id)
    -- Get water amount in mL for the plant's current age
    local water_ml = water_curve.day(plant.age)
    -- Display message about how much to water the plant today
    local days_old = " (" .. plant.age .. " days old)"
    toast(plant.name .. days_old .. " should be watered " .. water_ml .. "mL", "success")
else
    toast("Plant has no assigned water curve.", "warn")
end
```

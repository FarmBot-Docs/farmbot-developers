---
title: "Curves"
slug: "curves"
description: "List of curve Lua functions in FarmBot OS"
---

# get_curve(id)

Gets a **curve object** by its ID which can then be used to get the **curve value** for a given day, usually based on a plant's current age. Properties of the curve object include:

- `name` - The curve's name
- `type` - The curve's type (`water`, `spread`, or `height`)
- `unit` - The curve's unit (`mL` for water curves or `mm` for spread and height curves)
- `day(number)` - The curve's value for the given day, eg: `curve.day(10)`

{%
include callout.html
type="info"
content="Manually find a curve's ID by navigating to the curve in the web app and copying the number at the end of the URL."
%}

```lua
-- Get curve by its ID
curve = get_curve(123)

-- Display curve value and units for day 10
day = 10
toast("The " .. curve.type .. " on day " .. day .. " is " .. curve.day(day) .. curve.unit)
```

{%
include callout.html
type="info"
content="A plant's curve IDs can be retrieved from the `water_curve_id`, `spread_curve_id`, and `height_curve_id` properties of the plant object."
%}

```lua
-- Get plant from sequence variable
local plant = variable("Plant")

if plant.water_curve_id then
    -- Get water curve from plant
    local water_curve = get_curve(plant.water_curve_id)

    -- Get water amount in mL from curve for the plant's current age
    local water_ml = water_curve.day(plant.age)

    -- Display how much to water the plant today
    local days_old = " (" .. plant.age .. " days old)"
    toast(plant.name .. days_old .. " should be watered " .. water_ml .. "mL")
else
    toast("Plant has no assigned water curve.", "warn")
end
```

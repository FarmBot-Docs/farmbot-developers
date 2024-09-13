---
title: "Curves"
slug: "curves"
description: "List of curve Python functions in the FarmBot Python library"
---

# get_curve(curve_id)

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

```python
# Get curve by its ID
curve = bot.get_curve(123)

# Display curve value and units for day 10
day = 10
bot.toast(f"The {curve['type']} on day {day} is {curve.day(day)} {curve['unit']}")
```

{%
include callout.html
type="info"
content="A plant's curve IDs can be retrieved from the `water_curve_id`, `spread_curve_id`, and `height_curve_id` properties of the plant object."
%}

{%
include callout.html
type="info"
content="Manually find a plant's ID by navigating to the plant in the web app and copying the number at the end of the URL."
%}

```python
import datetime as dt

# Get plant from the API
plant = fb.api_get('points', 123)

if plant['water_curve_id']:
    # Get water curve from plant
    water_curve = fb.get_curve(plant['water_curve_id'])

    if plant['planted_at'] is not None:
        # Get the plant's age
        now = dt.datetime.now(dt.UTC)
        planted_at = dt.datetime.fromisoformat(plant['planted_at'])
        plant['age'] = (now - planted_at).days

        # Get water amount in mL from curve for the plant's current age
        water_ml = water_curve.day(plant['age'])

        # Display how much to water the plant today
        fb.toast(f"{plant['name']} ({plant['age']} days old) should be watered {water_ml}mL")
    else:
        fb.toast("Plant has no planted date.", "warn")
else:
    fb.toast("Plant has no assigned water curve.", "warn")
```

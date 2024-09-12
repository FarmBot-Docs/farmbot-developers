---
title: "Curves"
slug: "curves"
description: "List of curve Python functions in the FarmBot Python library"
---

# curve(curve_id)

Gets a **curve object** by its ID which can then be used to get the **curve value** for a given day, usually based on a plant's current age. Properties of the curve object include:

- `name` - The curve's name
- `type` - The curve's type (`water`, `spread`, or `height`)
- `unit` - The curve's unit (`mL` for water curves or `mm` for spread and height curves)

{%
include callout.html
type="info"
content="Manually find a curve's ID by navigating to the curve in the web app and copying the number at the end of the URL."
%}

```python
# Get curve by its ID
curve = fb.curve(123)

# Display curve units
fb.toast(f"The {curve['type']} unit is {curve['unit']}")
```

{%
include callout.html
type="info"
content="A plant's curve IDs can be retrieved from the `water_curve_id`, `spread_curve_id`, and `height_curve_id` properties of the plant object."
%}

# What's next?

 * [E-Stop and Unlock](./e-stop-and-unlock.md)

---
title: "Images"
slug: "images"
description: "List of image Python functions in the FarmBot Python library"
---

# take_photo()

**Takes a photo** using the device camera and uploads it to the web app.

{%
include callout.html
type="warning"
content="`take_photo` returns errors asynchronously, which may lead developers to believe the operation has succeeded when it actually fails in the background."
%}

```python
# Take a photo:
fb.take_photo()
```

# calibrate_camera()

Performs **camera calibration**.

{%
include callout.html
type="warning"
content="Calling this function will reset camera calibration settings."
%}

```python
# Calibrate the camera:
fb.calibrate_camera()
```

# measure_soil_height()

Use the camera to **determine soil depth at the current location**. Results will be available as point resources in the API. Performing this action over a wide area in many locations will improve the accuracy of `soil_height(x, y)` calculations.

```python
# Measure soil height at the current location:
fb.measure_soil_height()
```

```python
grid_spacing = 100
garden_size = fb.garden_size()

# Move in a grid pattern and measure soil height at each point:
for x in range(0, garden_size["x"], grid_spacing):
    for y in range(0, garden_size["y"], grid_spacing):
        fb.move(x=x, y=y, z=0)
        fb.measure_soil_height()
```

# detect_weeds()

Take a photo and **detect weeds in the image**. If any weeds are detected, weed points will be created in the API.

```python
# Detect weeds:
fb.detect_weeds()
```

# What's next?

 * [Jobs](./jobs.md)

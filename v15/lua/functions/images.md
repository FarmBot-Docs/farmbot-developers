---
title: "Images"
slug: "images"
description: "List of image Lua functions in FarmBot OS"
---

# take_photo()

**Takes a photo** using the device camera and uploads it to the web app. Returns `nil` on success. Returns an error object if capture fails.

{%
include callout.html
type="warning"
content="`take_photo` returns errors asynchronously, which may lead developers to believe the operation has succeeded when it actually fails in the background. If you require a high level of control over errors or are taking photos beyond the limits that the web app allows, see `take_photo_raw()`."
%}

```lua
-- Take a photo:
take_photo()
```

```lua
error = take_photo()

if error then
  toast("Take photo failed: " .. inspect(error), "error")
else
  toast("Take photo succeeded", "success")
end
```

# photo_grid()

Every FarmBot has a different garden size and camera viewport. `photo_grid()` returns a **metadata object** about the **point grid** required to perform a scan of the full garden. It returns a table with the following properties:

| Property          | Description |
|-------------------|-------------|
| `each`            | An iterator function that is called once per cell (see example below). |
| `total`           | The number of cells contained in the photo grid for the device. |
| `x_grid_points`   | The length of the garden scan on the X axis, measured in cells. |
| `y_grid_points`   | The length of the garden scan on the Y axis, measured in cells. |
| `x_grid_start_mm` | The X coordinate for the center of the first cell in the grid. |
| `y_grid_start_mm` | The Y coordinate for the center of the first cell in the grid. |
| `x_offset_mm`     | The camera's relative X offset from the FarmBot position. |
| `y_offset_mm`     | The camera's relative Y offset from the FarmBot position. |
| `x_spacing_mm`    | The number of millimeters between cells on the X axis. |
| `y_spacing_mm`    | The number of millimeters between cells on the Y axis. |
| `z`               | The height at which the camera was calibrated. |

```lua
-- Get the photo grid metadata:
local grid = photo_grid()

-- Move to each point in the grid and take a photo:
grid.each(function(cell)
    move_absolute({x = cell.x, y = cell.y, z = cell.z})
    local message = "Taking photo " .. cell.count .. " of " .. grid.total
    send_message("info", message)
    take_photo()
end)
```

# take_photo_raw()

**Takes a photo** using the device camera and **holds it in memory**. This is useful when uploading photos to 3rd party APIs. If your use case requires taking hundreds or thousands of photos per day, you can use `take_photo_raw()` to upload your images to a third-party image hosting provider that does not impose the same image hosting limits as the web app.

{%
include callout.html
type="info"
content="`take_photo_raw()` does not upload images to the web app. You must manually upload the resulting images to a hosting provider."
%}

```lua
-- Take a photo and hold it in memory, encoded in base64:
photo = take_photo_raw()
encoded_photo = base64.encode(photo)

-- Create the request headers and body:
headers = {}
headers["Content-Type"] = "application/json"
headers["Api-Key"] = 123abc
body = {
    images = {encoded_photo},
    plant_details = {"common_names"}
}

-- Send the request to the Plant.ID API:
response, error = http({
    url = "https://api.plant.id/v2/enqueue_identification",
    method = "POST",
    headers = headers,
    body = json.encode(body)
})
```

# base64.encode()

Performs **base64 encoding** on an object such as an image. Useful for uploading images to 3rd party APIs. Can also be used in reverse: `base64.decode()`.

```lua
-- Take a photo and hold it in memory:
photo = take_photo_raw()

-- Encode the photo in base64:
encoded_photo = base64.encode(photo)

-- Decode the photo from base64:
decoded_photo = base64.decode(encoded_photo)
```

# calibrate_camera()

Performs **camera calibration**.

{%
include callout.html
type="warning"
content="Calling this function will reset camera calibration settings."
%}

```lua
-- Calibrate the camera:
calibrate_camera()
```

# measure_soil_height()

Use the camera to **determine soil depth at the current location**. Results will be available as point resources in the API. Performing this action over a wide area in many locations will improve the accuracy of `soil_height(x, y)` calculations.

```lua
-- Measure soil height at the current location:
measure_soil_height()
```

```lua
local grid_spacing = 100

-- Move in a grid pattern and measure soil height at each point:
for x = 0, garden_size().x, grid_spacing do
    for y = 0, garden_size().y, grid_spacing do
        move_absolute(x, y, 0)
        measure_soil_height()
    end
end
```

# detect_weeds()

Take a photo and **detect weeds in the image**. If any weeds are detected, weed points will be created in the API.

```lua
-- Detect weeds:
detect_weeds()
```
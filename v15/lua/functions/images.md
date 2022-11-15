---
title: "Images"
slug: "images"
description: "List of image Lua functions in FarmBot OS"
---

# take_photo()

{%
include callout.html
type="bug"
title="Known bug"
content="`take_photo` returns errors asynchronously, which may lead developers to believe the operation has succeeded when it actually fails in the background. If you require a high level of control over errors or are taking photos beyond the limits that the Web App allows, see `take_photo_raw()`."
%}

Takes a photo using the device camera and uploads it to the web app. Returns `nil` on success. Returns an error object if capture fails.

```lua
error = take_photo()

if error then
  send_message("error", "Capture failed " .. inspect(error))
else
  send_message("info", "Capture OK")
end
```

# photo_grid()

Every FarmBot has a different garden size and camera viewport. The `photo_grid()` helper provides developers with a metadata object about the unique camera setup for the current device. The helper is most useful for operations that perform full-garden photography, such as taking a scan of the garden.

Calling `photo_grid()` will return a table with the following properties:

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

**Example:** Perform a full-garden photo scan:

```lua
local grid = photo_grid()

grid.each(function(cell)
    if read_status("informational_settings", "locked") then
        return
    else
        move_absolute({x = cell.x, y = cell.y, z = cell.z})
        local msg = "Taking photo " .. cell.count .. " of " .. grid.total
        send_message("info", msg)
        take_photo()
    end
end)

```

# take_photo_raw()

`take_photo_raw()` takes a photo using the device camera and holds it in memory. This functionality is useful when uploading photos to 3rd party APIs. If your usecase requires taking hundreds or thousands of photos per-use, you can use `take_photo_raw()` to upload your images to a third-party image hosting provider that does not impose the same image hosting limits as the Web App.

{%
include callout.html
type="info"
content="`take_photo_raw()` does not upload images to the web app. You must manually upload the resulting images to a hosting provider."
%}

```lua
data = take_photo_raw()
return base64.encode(data)
```

# base64.encode()

Performs `base64` encoding on an object such as an image. Useful for uploading images to 3rd party APIs. Can also be used in reverse: `base64.decode()`.

```lua
data = take_photo_raw()
return base64.encode(data)
```

# calibrate_camera()

Performs camera calibration. Calling this function will **reset camera calibration settings**.

# measure_soil_height()

Use the camera to determine soil depth at the current location.
Results will be available as point resources in the API.
Performing this action over a wide area in many locations will improve the accuracy of soil height readings taken via `soil_height(x, y)`.

# detect_weeds()

Take a photo of the current location. If any vegetation is detected in the photo, it will be added to the device's list of weeds.
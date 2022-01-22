---
title: "Lua Functions"
slug: "functions"
description: "List of available Lua functions in FarmBot OS"
---

* toc
{:toc}

All of the available Lua functions are listed below. Additionally, you may access most of the functions available in the [Lua 5.2 standard library](https://www.lua.org/manual/5.2/). If you have questions about the available functions or would like us to make new features available, please let us know in the [FarmBot Forum](https://forum.farmbot.org/).

# api(options)

Performs an HTTP request to the FarmBot API, returning `nil` if an error occurs (see logs for details).

This is a limited convenience function that provides an alternative to the `http()` helper. It has a few differences from `http()`:

 * You do not need to run `json.encode` on inputs
 * You do not need to run `json.decode` on outputs
 * The only supported request format is JSON
 * You do not need to pass an `auth_token()` in the header
 * The base URL is not configurable. `https://my.farm.bot` is the only endpoint supported.
 * Returns `nil` if there was an error
 * Errors are sent to the log stream (if any).

```lua
result = api({
    method = "post",
    -- Don't forget the leading "/":
    url = "/api/points",
    -- `body` is optional for GET requests.
    body = {
        x = 200,
        y = 200,
        z = 0,
        radius = 100,
        pointer_type = "GenericPointer"
    }
})

if result then
    send_message("debug", "Point creation OK", "toast")
else
    send_message("error", "ERROR - See logs for details", "toast")
end
```

# auth_token()

Returns the device's authorization token (string). This value can be used to access API resources without the need to store account passwords in Lua code or ENV vars.

```lua
-- Fetch all points from API:

resp_json, err = http({
    method = "GET",
    url = "https://my.farm.bot/api/points",
    headers = {
        Authorization = ("bearer " .. auth_token()),
        Accept = "application/json"
    }
})

points = json.decode(resp_json)
```

# base64.encode()

Performs `base64` encoding on an object such as an image. Useful for uploading images to 3rd party APIs. Can also be used in reverse: `base64.decode()`.

```lua
data = take_photo_raw()
return base64.encode(data)
```

# calibrate_camera()

Performs camera calibration. Calling this function will **reset camera calibration settings**.

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

# coordinate(x, y, z)

Generate a coordinate for use in location-based functions such as `move_absolute` and `check_position`.

```lua
coordinate(1.0, 20, 30)
-- Returns:
-- {x = 1.0, y = 20,  z = 30}
```

# cs_eval(celeryscript_ast)

**ADVANCED USERS ONLY.** Allows you to execute arbitrary CeleryScript nodes. Even advanced users should avoid using this function directly.

```lua
cs_eval({
  kind = "rpc_request",
  args = {
    label = "example",
    priority = 500
  },
  body = {
    {
      kind = "move_absolute",
      args = {
        location = {kind = "coordinate", args = {x = 2, y = 2, z = 2}},
        offset = {kind = "coordinate", args = {x = 0, y = 0, z = 0}},
        speed = 100
      }
    }
  }
})
```

# current_month / current_hour / current_minute / current_second

Returns a number representing the current month, hour, minute, or second.

# detect_weeds()

Take a photo of the current location. If any vegetation is detected in the photo, it will be added to the device's list of weeds.

# emergency_lock()

Emergency locks the Farmduino microcontroller, preventing motor and peripheral usage. Some features, such as `send_message`, are still available while emergency locked.

```lua
-- Lock the device:
emergency_lock()
```

# emergency_unlock()

Unlock a previously locked device.

```lua
-- Unlock the device:
emergency_unlock()
```

# env(key, value) / env(key)

Store and retrieve key/value pairs to disk. This information will be stored on the device SD card and eventually synced with your web app account.

`key` and `value` must be strings. No other values are allowed. Values may not exceed 1,000 characters in length.

To create or update a key/value pair:

```lua
env("key", "value")

-- Example:
env("MY_API_TOKEN", "abc123")
```

To retrieve a previously stored value:

```lua
env("key")
-- Returns `nil` if no value is found.

-- Example:
api_token = env("MY_API_TOKEN")
if api_token then
  send_message("info", "Token value is " .. api_token)
else
  send_message("info", "Value not found")
end
```

# fbos_version()

Returns a string representation of FarmBot OS's version.

```lua
fbos_version()
```

# find_axis_length(axis?)

Determines the length of an axis using stall detection, rotary encoders, or limit switch hardware.

```lua
-- Single axis:
find_axis_length("x")
find_axis_length("y")
find_axis_length("z")

-- Every axis in the order Z, Y, X:
find_axis_length()
find_axis_length("all")
```

# find_home(axis?)

Finds the `0` (home) position for an axis using stall detection, rotary encoders, or limit switch hardware.

```lua
-- Single axis:
find_home("x")
find_home("y")
find_home("z")

-- Every axis in the order Z, Y, X:
find_home("all")
find_home()
```

# firmware_version()

Returns a string representation of the firmware version on the Farmduino/Arduino.

```lua
firmware_version()
```

# garden_size()

Returns a table with an `x` and `y` attribute represent the maximum length of the garden bed as determined by firmware config settings.

```lua
size = garden_size()
send_message("info", "Width: " .. size.y)
send_message("info", "Length: " .. size.x)
```

# get_device(property?)

Fetch device properties. This is the same [device resource found on the API](https://gist.github.com/RickCarlino/10db2df375d717e9efdd3c2d9d8932af).

```lua
-- Every property:
get_device()

-- Single property:
get_device("name")
```

# get_job_progress / set_job_progress

Creates new jobs in the UI jobs panel. This is useful for long running tasks such a photo grids.

```lua
set_job_progress("example", {
  type = "anything",
  status = "working",
  percent = 12.3,
})
progress = get_job_progress("example")
send_message("debug", "Job progress: " .. progress.percent, "toast")
```
# get_fbos_config(property?)

Fetch FarmBot OS configuration properties. This is the same [FarmBot OS configuration resource found on the API](https://gist.github.com/RickCarlino/10db2df375d717e9efdd3c2d9d8932af).

```lua
-- Fetch all properties:
get_fbos_config()

-- Fetch single property:
get_fbos_config("disable_factory_reset")
```

# get_firmware_config(property?)

Fetch firmware configuration properties. This is the same [firmware configuration resource found on the API](https://gist.github.com/RickCarlino/10db2df375d717e9efdd3c2d9d8932af).

```lua
get_firmware_config()
get_firmware_config("encoder_enabled_z")
```

# get_position()

Return a table containing the currrent X, Y, Z value of the device.

```lua
position, error = get_position()

if error then
  send_message("error", error, "toast")
else
  message = "Y position is " .. position.y
  send_message("info", message)
end
```

# go_to_home(axis?)

Move to the `0` (home) position of a given axis.

```lua
-- Single axis:
go_to_home("x")
go_to_home("y")
go_to_home("z")

-- Every axis:
go_to_home("all")
go_to_home()
```

# http(params)

Performs an HTTP request. Example:

```lua
response, error = http({
  -- REQUIRED
  url="https://my.farm.bot/api/farmware_envs",
  -- OPTIONAL. Default value is "get".
  method="POST",
  -- OPTIONAL. Only strings and numbers.
  headers={
    Authorization="bearer eyJ....4cw",
    Accept="application/json"
  },
  -- OPTIONAL. Must be a string. Use included JSON lbrary for
  --           JSON APIs
  body=json.encode({
  })
})

if error then
  -- The `error` object is reserved for non-HTTP errors.
  -- Example: missing URL.
  -- `error` will be `nil` if no issues are found.
  send_message("info", "Unknown error: " .. inspect(error))
else
  -- The `response` object has three properties:
  --   `status`: Number              - Response code. Example: 200.
  --   `body`: String                - Response body. Always a string.
  --   `headers`: Map<String, String> - Response headers.
end
```

# inspect(any)

Alias for `json.encode`.

# json.decode(string)

Converts a JSON encoded string to a Lua table:

```lua
result, error = json.decode('{"foo":"bar","example":123}')
-- { foo="bar", example=123 }
```

# json.encode(any)

Converts a Lua variable into stringified JSON.

```lua
result, error = json.encode({ foo="bar", example=123 })
-- => '{"foo":"bar","example":123}'
```

# measure_soil_height()

Use the camera to determine soil depth at the current location.
Results will be available as point resources in the API.
Performing this action over a wide area in many locations will improve the accuracy of soil height readings taken via `soil_height(x, y)`.

# move_absolute(x, y, z, s?) / move_absolute(coord)

Move to an absolute coordinate position.

```lua
move_absolute(1.0, 2, 3.4)
-- Alternative syntax:
move_absolute(coordinate(1.0, 20, 30))
```

**NOTE:** `move_absolute` can accept an optional fourth argument that sets movement speed as a percentage of max speed.

# new_sensor_reading(params)

Plot a sensor reading point on the [sensors panel](https://my.farm.bot/app/designer/sensors). Please note that calling `new_sensor_reading()` does not perform any readings, it only records a value. See also: `read_pin()`

```lua
DIGITAL = 0
ANALOG = 1
position, error = get_position()

i = 0
while (i < 10) do
  i = i + 1
  new_sensor_reading({
    x=position.x,
    y=position.y,
    z=position.z,
    mode=ANALOG,
    pin=0,
    value=(math.random() * 1024)
  })
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

# read_pin(pin, mode?)

`read_pin(pin_num, mode?)` reads a pin when given a pin number and read mode (`"analog"` or `"digital"`). Defaults to `"digital"` if no mode is given:

```lua
pin23 = read_pin(23) -- Digital is the default mode
pin24 = read_pin(24, "digital")
pin25 = read_pin(25, "analog")
```

# read_status(...path?)

`read_status(...path?)` reads the entire device state tree into memory.

The device state tree contains numerous properties that are relevant to the device's operation. It is the same state tree seen in [FarmBotJS](https://github.com/FarmBot/farmbot-js/blob/main/src/interfaces.ts#L6-L25).

```lua
-- Provide a path to the property you are interested in:
read_status("location_data", "raw_encoders", "x")

-- Alternative syntax:
status = read_status().location_data.raw_encoders.x
```

# send_message(type, message, channels)

`send_message(type, message, channels?)`

The first required parameter is a log type, which is one of the following string values: `"assertion"`, `"busy"`, `"debug"`, `"error"`, `"fun"`, `"info"`, `"success"`, `"warn"`

The second required parameter is the message, which may be either a string or a number.

The third parameter is optional. It can be a single string or an array of strings. The strings must be one of the following: `"ticker"`, `"toast"`, `"email"`, `"espeak"`

```lua
-- Send a message to the default channel ("ticker"):
send_message("error", "Hello")

-- Send a message to a single channel:
send_message("success", "You've got mail!", "email")

-- Send a message to multiple channels:
send_message("info", "All systems running.", {"toast", "espeak"})
```

# set_pin_io_mode(pin, mode)

Sets the I/O mode of an Arduino pin. It is slightly similar to the [`pinMode()` function in the Arduino IDE](https://www.arduino.cc/reference/en/language/functions/digital-io/pinmode/).

**Valid pin modes:** `"input"`, `"input_pullup"`, `"output"`.

```lua
result, error = set_pin_io_mode(13, "output")
if error then
  send_message("error", inspect(error))
else
  send_message("info", inspect(result))
end
```

# soil_height(x, y)

Given an X and Y coordinate, returns a best-effort estimate of the Z axis height of the soil. This function requires at least 3 soil height measurments. When there are less than 3 measurements available, it will return the SOIL HEIGHT setting from the device settings page.

```lua
x = 10
y = 29
my_soil_height = soil_height(x, y)
send_message("info", "Distance to soil at (10, 29): " .. inspect(my_soil_height))
-- => "Distance to soil at (10, 29): -409.84"
```

# soft_stop()

This is an advanced feature that is intended to be used in conjunction with `watch_pin`.

When called, `soft_stop` will cancel all current and pending movement requests. Unlike `emergency_lock`, it will not lock the device nor will it reset the state of peripherals. Commands (including movement commands) will continue normally after a soft stop occurs. This function can be used to pause FarmBot temporarily if a peripheral value changes mid-movement.

# take_photo()

{%
include callout.html
type="bug"
title="Known bug"
content="`take_photo` returns errors asyncronously, which may lead developers to believe the operation has succeeded when it actually fails in the background. If you require a high level of control over errors or are taking photos beyond the limits that the Web App allows, see `take_photo_raw()`."
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

# uart.close()

See documentation for `uart.open()`.

# uart.list()

Returns a list of UART devices.

```lua
uart_list = uart.list()

for _number, device_path in ipairs(uart_list) do
  send_message("debug", inspect(device_path), {"toast"})
end
```

# uart.open(path, baud)

Open a UART device (typically, via USB) for reading and writing. Please note that the UART devices must be connected to the Raspberry Pi, not the Arduino.

```lua
-- device name, baud rate:
my_uart, error = uart.open("ttyAMA0", 115200)

if error then
    send_message("error", inspect(error), "toast")
    return
end

if my_uart then
    -- Wait 60s for data...
    string, error2 = my_uart.read(15000)
    if error2 then
        send_message("error", inspect(error2), "toast")
    else
        send_message("info", inspect(string), "toast")
    end

    error3 = my_uart.write("Hello, world!")

    if error3 then
        -- Handle errors etc..
    end

    my_uart.close()
end
```

# uart.read()

See documentation for `uart.open()`.

# uart.write()

See documentation for `uart.open()`.

# update_device(params)

Update device properties. This is the same [device resource found on the API](https://gist.github.com/RickCarlino/10db2df375d717e9efdd3c2d9d8932af).

```lua
update_device({key = "value"})
update_device({name = "Test Farmbot"})
```

# update_fbos_config()

Update FarmBot OS configuration properties. This is the same [FarmBot OS configuration resource found on the API](https://gist.github.com/RickCarlino/10db2df375d717e9efdd3c2d9d8932af).

```lua
update_fbos_config({key = "value"})
update_fbos_config({disable_factory_reset = true})
```

# update_firmware_config(params)

Update firmware configuration properties. This is the same [firmware configuration resource found on the API](https://gist.github.com/RickCarlino/10db2df375d717e9efdd3c2d9d8932af).

```lua
update_firmware_config({key = "value"})
update_firmware_config({encoder_enabled_z = 1.0})
```

# variable(name)

If the sequence executing the <span class="fb-step fb-lua">Lua</span> command contains a [sequence variable](https://software.farm.bot/docs/variables), you can access its content by calling the `variable(name)` function:

```lua
-- Assumes you are inside of a function that has a variable:
x_pos = variable("parent").x
send_message("info", x_pos, {"toast"});
```

# wait(ms)

Pause execution for a certain number of milliseconds. **Crashes if the value is three minutes or greater.**

```lua
-- wait for 1 second:
wait(1000)
```

# watch_pin(pin, callback)

Fork the current Lua process into a second, parellel Lua script that is initialized every 500 milliseconds for the duration of the parent script's lifetime.

Things to keep in mind:

 * The pin watcher feature exists to support internal functionality of the FarmBot, such as motor load monitoring for vacuum and rotary tools. It is an advanced feature that should only be used as a last resort when more simple solutions cannot be used.
 * The callback is a _forked copy of the running Lua script_. It is not executed in the same script.
 * The callback _does not share memory_ with the calling script. It is completely isolated from its parent. Even though you can access variables with identical names as the parent script, they are _not_ shared. They are duplicate copies.
 * Because the callback is _re-initialized_ every 500 ms. It is not possible to store state in the callback function. Any variables that are modified will be reset upon the next run.
 * The callback is terminated within 500 ms of the parent's termination.

```lua
watch_pin(13, function(data)
  local pin = data.pin
  local val = data.value
  local msg = "Pin " .. pin .. " has a value of " .. val
  send_message("debug", msg, "toast")
end)

-- Wait 3 seconds so that the watcher
-- can run a few (~6) times.
--
wait(3000)
```
# write_pin(pin, mode, value)

Sets a pin to a particular mode and value:

```lua
write_pin(13, "analog", 128)
```

# What's next?

 * [Lua Examples](examples.md)

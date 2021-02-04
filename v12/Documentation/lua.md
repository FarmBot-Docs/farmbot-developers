---
title: "Lua"
slug: "lua"
description: "List of available Lua functions in FBOS"
---

* toc
{:toc}

The [sequence editor](https://software.farm.bot/docs/sequences) is an easy to use tool for automating FarmBot operations. However, advanced users who are familiar with computer programming concepts may opt for a more advanced interface. For these users, we provide several methods to insert **Lua code fragments** directly into sequences:

 * By using the <span class="fb-step fb-lua">Lua</span> command ([learn more](https://software.farm.bot/docs/advanced-sequence-commands)).
 * By using the <span class="fb-step fb-assertion">Assertion</span> command ([learn more](https://software.farm.bot/docs/advanced-sequence-commands)).
 * By adding a **formula** to a <span class="fb-step fb-move">Move</span> command input field ([learn more](https://software.farm.bot/v12/The-FarmBot-Web-App/sequences/sequence-commands.html#advanced-options)).

 The table below shows the features available to each of the methods:

|Command|Executes Lua code|Variable access|Recovery options|
|-------|-----------------|---------------|----------------|
|<span class="fb-step fb-lua">Lua</span>|:white_check_mark:|:white_check_mark:|:no_entry:|
|<span class="fb-step fb-assertion">Assertion</span>|:white_check_mark:|:no_entry:|:white_check_mark:|
|<span class="fb-step fb-move">Move</span> formula inputs|:white_check_mark:|:no_entry:|:no_entry:|

All of the available Lua functions are listed below. Additionally, you may access most of the functions available in the [Lua 5.2 standard library](https://www.lua.org/manual/5.2/). If you have questions about the available functions or would like us to make new features available, please let us know in the [FarmBot Forum](https://forum.farmbot.org/).

# coordinate()

Generate a coordinate for use in location-based functions such as `move_absolute` and `check_position`.

```lua
coordinate(1.0, 20, 30)
-- Returns:
-- {x = 1.0, y = 20,  z = 30}
```

# check_position()

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

# fbos_version()

Returns a string representation of FarmBot OS's version.

```lua
fbos_version()
```

# find_axis_length()

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

# find_home()

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

# get_device()

Fetch device properties. This is the same [device resource found on the API](https://gist.github.com/RickCarlino/10db2df375d717e9efdd3c2d9d8932af).

```lua
-- Every property:
get_device()

-- Single property:
get_device("name")
```

# get_fbos_config()

Fetch FarmBot OS configuration properties. This is the same [FarmBot OS configuration resource found on the API](https://gist.github.com/RickCarlino/10db2df375d717e9efdd3c2d9d8932af).

```lua
-- Fetch all properties:
get_fbos_config()

-- Fetch single property:
get_fbos_config("disable_factory_reset")
```

# get_firmware_config()

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

# go_to_home()

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

# move_absolute()

Move to an absolute coordinate position.

```lua
move_absolute(1.0, 2, 3.4)
-- Alternative syntax:
move_absolute(coordinate(1.0, 20, 30))
```

# read_pin()

`read_pin(pin_num, mode?)` reads a pin when given a pin number and read mode (`"analog"` or `"digital"`). Defaults to `"digital"` if no mode is given:

```lua
pin23 = read_pin(23) -- Digital is the default mode
pin24 = read_pin(24, "digital")
pin25 = read_pin(25, "analog")
```

# read_status()

`read_status(...path?)` reads the entire device state tree into memory.

The device state tree contains numerous properties that are relevant to the device's operation. It is the same state tree seen in [FarmBotJS](https://github.com/FarmBot/farmbot-js/blob/main/src/interfaces.ts#L6-L25).

```lua
-- Provide a path to the property you are interested in:
read_status("location_data", "raw_encoders", "x")

-- Alternative syntax:
status = read_status().location_data.raw_encoders.x
```

# send_message()

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

# update_device()

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

# update_firmware_config()

Update firmware configuration properties. This is the same [firmware configuration resource found on the API](https://gist.github.com/RickCarlino/10db2df375d717e9efdd3c2d9d8932af).

```lua
update_firmware_config({key = "value"})
update_firmware_config({encoder_enabled_z = 1.0})
```

# variable()

{%
include callout.html
type="warning"
title="BETA"
content="The `variable()` function is not yet available to <span class='fb-step fb-move'>Move</span> input formuals or the <span class='fb-step fb-assertion'>Assertion</span> command."
%}

If the sequence executing the <span class="fb-step fb-lua">Lua</span> command contains a [sequence variable](https://software.farm.bot/docs/variables), you can access its content by calling the `variable()` function:

```lua
-- Assumes you are inside of a function that has a variable:
x_pos = variable().x
send_message("info", x_pos, {"toast"});
```

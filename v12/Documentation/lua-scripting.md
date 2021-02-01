---
title: "Lua Scripting"
slug: "lua-scripting"
description: "An overview of the functions available when writing Lua code."
---

* toc
{:toc}

The [sequence editor](https://software.farm.bot/docs/sequences) is an easy to use tool for automating FarmBot operations. Advanced users who are familiar with computer programming concepts may opt for a more advanced interface, however. For these users, we provide several methods to insert Lua code fragments.

Advanced users can add Lua code to their sequences in the following manners:

 * Calling the [ASSERT block](assertions.md) within a sequence.
 * Calling the Lua block within a sequence (described below).
 * By [adding a formula to the MOVE block](https://software.farm.bot/v12/The-FarmBot-Web-App/sequences/sequence-commands.html#advanced-options).

 # The "LUA" Sequence Block

The LUA block is similar to the [ASSERT block](assertions.md). Unlike the ASSERT block, it is more generic and does not offer recovery options. Additionally, **it is  possible to access sequence variables from within a LUA block**, which is **currently not possible via the ASSERT block**.

# Lua API

All of the functions available in the LUA block are listed below. Additionally, you may access most of the functions available in the [Lua 5.2 standard library](https://www.lua.org/manual/5.2/). If you have questions about the available functions or would like us to make new features available, please let us know in the [FarmBot Forum](https://forum.farmbot.org/).

## Accessing Sequence Variables

If the sequence executing the LUA block contains a [sequence variable](https://software.farm.bot/v12/The-FarmBot-Web-App/sequences/variables.html), you can access its content by calling the `variable()` function:


**ONLY AVAILABLE IN THE LUA BLOCK**. Not yet available in MOVE block formulas or the ASSERT block.

```lua
-- Assumes you are inside of a function that has a variable:
x_pos = variable().x
send_message("info", x_pos, {"toast"});
```

## emergency_lock()

Locks the Farmduino. Prevents motor and peripheral usage.

Some features, such as `send_message`, are still available while locked.

Example:

```lua
-- Lock the device:
emergency_lock()
```

## emergency_unlock()

Unlock a previously locked device:

```lua
-- Unlock the device:
emergency_unlock()
```

## find_axis_length(axis?)

Determine the length of an axis.

```lua
-- Find length of single axis:
find_axis_length("x")
find_axis_length("y")
find_axis_length("z")

-- Find length of all axes:
find_axis_length()
find_axis_length("all")
```

## find_home(axis?)

Set the 0 position for an axis.

```lua
-- Single axis:
find_home("x")
find_home("y")
find_home("z")

-- Every axis:
find_home("all")
find_home()
```

## go_to_home(axis?)

Move to the 0 position of a given axis.

```lua
-- Single axis:
go_to_home("x")
go_to_home("y")
go_to_home("z")

-- Every axis:
go_to_home("all")
go_to_home()
```

## firmware_version()

Returns a string representation of the firmware version on the Farmduino/Arduino.

```lua
firmware_version()
```

## get_device()

Fetch device properties. This is the same [device resource found on the API](https://gist.github.com/RickCarlino/10db2df375d717e9efdd3c2d9d8932af).

```lua
-- Single property:
get_device("name")

-- Every property:
get_device()
```

## update_device({key = "value"})

Update device properties. This is the same [device resource found on the API](https://gist.github.com/RickCarlino/10db2df375d717e9efdd3c2d9d8932af).

```lua
update_device({name = "Test Farmbot"})
```

## get_fbos_config()

Fetch FarmBot OS configuration properties. This is the same [FarmBot OS configuration resource found on the API](https://gist.github.com/RickCarlino/10db2df375d717e9efdd3c2d9d8932af).

```lua
-- Fetch all properties:
get_fbos_config()

-- Fetch single property:
get_fbos_config("disable_factory_reset")
```

## update_fbos_config({key = "value"})

Update FarmBot OS configuration properties. This is the same [FarmBot OS configuration resource found on the API](https://gist.github.com/RickCarlino/10db2df375d717e9efdd3c2d9d8932af).

```lua
update_fbos_config({disable_factory_reset = true})
```

## get_firmware_config()

Fetch firmware configuration properties. This is the same [firmware configuration resource found on the API](https://gist.github.com/RickCarlino/10db2df375d717e9efdd3c2d9d8932af).

```lua
get_firmware_config()
get_firmware_config("encoder_enabled_z")
```

## update_firmware_config({key = "value"})

Update firmware configuration properties. This is the same [firmware configuration resource found on the API](https://gist.github.com/RickCarlino/10db2df375d717e9efdd3c2d9d8932af).

```lua
update_firmware_config({encoder_enabled_z = 1.0})
```

## coordinate(1.0, 20, 30)

Generate a coordinate for use in location-based functions such as `move_absolute` and `check_position`.

```lua
coordinate(1.0, 20, 30)
-- Returns:
-- {x = 1.0, y = 20,  z = 30}
```

## check_position(coordinate, tolerance)

Returns `true` if the device is within `tolerance` range of `coordinate`.

```lua
if check_position({x = 0, y = 0,  z = 0}, 1.23) then
  send_message("info", "We are HOME")
end
```

## move_absolute(x, y, z)

Move to an absolute coordinate.

```lua
move_absolute(1.0, 2, 3.4)
-- Alternative syntax:
move_absolute(coordinate(1.0, 20, 30))
```

## read_pin(pin_num, mode?)

Reads a pin when given a pin number and read mode (`"analog"` or `"digital"`). Defaults to `"digital"` if no mode is given:

```lua
pin24 = read_pin(24) -- Digital is the default
pin23 = read_pin(23, "analog")
```

## get_position()

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

## read_status(...path?)

Read the entire device state tree into memory.

The device state tree contains numerous properties that are relevant to the device's operation. It is the same state tree seen in [FarmBotJS](https://github.com/FarmBot/farmbot-js/blob/main/src/interfaces.ts#L6-L25).

```lua
-- Provide a path to the property you are interested in:
read_status("location_data", "raw_encoders", "x")

-- Alternative syntax:
status = read_status().location_data.raw_encoders.x
```

## send_message(level, message, channels?)

The first required parameter is a log level, which is one of the following string values: `"assertion"`, `"busy"`, `"debug"`, `"error"`, `"fun"`, `"info"`, `"success"`, `"warn"`

The second required parameter is the message, which may be either a string or a number.

The third parameter is optional. It can be a single string or an array of strings. The strings must be one of the following: `"ticker"`, `"toast"`, `"email"`, `"espeak"`

```lua
-- Multiple channels:
send_message("info", "All systems running.", {"toast", "espeak"})

-- Single channel:
send_message("debug", "You've got mail!", "email")

-- Default channel ("ticker"):
send_message("error", "Hello")
```

---
title: "Pins"
slug: "pins"
description: "List of pin Lua functions in FarmBot OS"
---

# new_sensor_reading(params)

**Plots a sensor reading point** which can be viewed from the [sensors panel](https://my.farm.bot/app/designer/sensors). Accepts a table of parameters that include the X, Y, and Z coordinates of the reading (usually the FarmBot's current position), the pin number, the pin mode (analog or digital), the value, and the time in UTC at which the sensor was read at.

The `mode` must be either `0` for `digital` readings or `1` for `analog` readings.

{%
include callout.html
type="info"
content="Calling `new_sensor_reading()` does not perform any readings, it only records a value. See also: [read_pin()](#read_pinpin-mode)."
%}

```lua
local pin_63 = 63 -- Tool verification pin
local pin_value = read_pin(pin_63)
local xyz = get_xyz()
local read_at = utc()

-- Create a digital sensor reading for Pin 63 at the current position
new_sensor_reading({
  x = xyz.x,
  y = xyz.y,
  z = xyz.z,
  mode = 0,
  pin = pin_63,
  value = pin_value,
  read_at = read_at
})
```

```lua
local pin_59 = 59 -- Soil moisture sensor pin
local pin_value = read_pin(pin_59, "analog")
local read_at = utc()

-- Create an analog sensor reading for Pin 59 at the position (100, 200, 0)
new_sensor_reading({
  x = 100,
  y = 200,
  z = 0,
  mode = 1,
  pin = pin_59,
  value = pin_value,
  read_at = read_at
})
```

# on(pin)

**Sets the state of the given pin to digital `1`**, also known as "high" or "on".

```lua
-- Turn on the lighting peripheral
on(7)
```

# off(pin)

**Sets the state of the given pin to digital `0`**, also known as "low" or "off".

```lua
-- Turn off the lighting peripheral
off(7)
```

# read_pin(pin, mode?)

**Reads the given pin** with the read mode `analog` or `digital`. Defaults to `digital` if no mode is given.

{%
include callout.html
type="info"
content="Calling `read_pin()` does not record the reading in the API, it only reads the pin. Use [new_sensor_reading()](#new_sensor_readingparams) to record the reading."
%}

```lua
-- Read pin 23 in digital mode
pin23 = read_pin(23)

-- Read pin 23 in digital mode (alternative syntax)
pin23 = read_pin(23, "digital")

-- Read pin 25 in analog mode
pin25 = read_pin(25, "analog")
```

# set_pin_io_mode(pin, mode)

**Sets the I/O mode of a pin**, similar to the [`pinMode()` function in the Arduino IDE](https://www.arduino.cc/reference/en/language/functions/digital-io/pinmode/). Valid pin modes include `input`, `input_pullup`, and `output`.

```lua
-- Set pin 13 to input mode
set_pin_io_mode(13, "input")

-- Set pin 13 to input_pullup mode
set_pin_io_mode(13, "input_pullup")

-- Set pin 13 to output mode
set_pin_io_mode(13, "output")
```

# toggle_pin(pin)

**Toggles the state of the given pin** between digital `1` (on) and `0` (off).

{%
include callout.html
type="info"
content="If the pin is initially set to an analog value, it will be rounded to the nearest digital value and then toggled."
%}

```lua
-- Toggle pin 13
toggle_pin(13)
```

# watch_pin(pin, callback)

**Forks the Lua process** into a second, parallel Lua script for the purpose of **watching a pin**. The callback function is executed every 500 milliseconds for the duration of the parent script's lifetime.

Things to keep in mind:

 * The pin watcher feature exists to support internal functionality of the FarmBot, such as motor load monitoring for vacuum and rotary tools. It is an advanced feature that should only be used as a last resort when more simple solutions cannot be used.
 * The callback is a _forked copy of the running Lua script_. It is not executed in the same script.
 * The callback _does not share memory_ with the calling script. It is completely isolated from its parent. Even though you can access variables with identical names as the parent script, they are _not_ shared. They are duplicate copies.
 * Because the callback is _re-initialized_ every 500 ms. It is not possible to store state in the callback function. Any variables that are modified will be reset upon the next run.
 * The callback is terminated within 500 ms of the parent's termination.

```lua
-- Watch pin 13 and toast the pin number and value every 500 ms
watch_pin(13, function(data)
  toast("Pin " .. data.pin .. " has a value of " .. data.value)
end)

-- Wait so the watcher's callback function can execute about six times
wait(3000)
```

# write_pin(pin, mode, value)

**Sets a pin to a particular mode and value.** The `mode` must be either `0` for `digital` values or `1` for `analog` values.

```lua
-- Set pin 13 to digital mode and write a value of 1
write_pin(13, "digital", 1)

-- Set pin 13 to analog mode and write a value of 128
write_pin(13, "analog", 128)
```
---
title: "Pins"
slug: "pins"
description: "List of pin Lua functions in FarmBot OS"
---

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

# on(pin)

Sets the state of the given pin to digital `1`.

```lua
on(7)
```

# off(pin)

Sets the state of the given pin to digital `0`.

```lua
off(7)
```

# read_pin(pin, mode?)

Reads the given pin with the read mode `analog` or `digital`. Defaults to `digital` if no mode is given.

```lua
pin23 = read_pin(23) -- Digital is the default mode
pin24 = read_pin(24, "digital")
pin25 = read_pin(25, "analog")
```

# set_pin_io_mode(pin, mode)

Sets the I/O mode of an Arduino pin. It is slightly similar to the [`pinMode()` function in the Arduino IDE](https://www.arduino.cc/reference/en/language/functions/digital-io/pinmode/).

**Valid pin modes:** `input`, `input_pullup`, `output`.

```lua
result, error = set_pin_io_mode(13, "output")
if error then
  send_message("error", inspect(error))
else
  send_message("info", inspect(result))
end
```

# toggle_pin(pin)

Toggles the state of the given pin between digital `1` and `0`. If the pin is initially set to an analog value, it will be rounded to the nearest digital value and then toggled.

```lua
toggle_pin(13)
```

# watch_pin(pin, callback)

Fork the current Lua process into a second, parallel Lua script that is initialized every 500 milliseconds for the duration of the parent script's lifetime.

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
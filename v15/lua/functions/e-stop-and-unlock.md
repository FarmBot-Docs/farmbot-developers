---
title: "E-stop and Unlock"
slug: "e-stop-and-unlock"
description: "List of E-stop and Unlock Lua functions in FarmBot OS"
---

# emergency_lock()

**Emergency locks** (E-stops) the Farmduino microcontroller, preventing motor and peripheral usage, and resetting peripheral pins to OFF.

{%
include callout.html
type="info"
content="Features that do not rely on the microcontroller, such as sending messages and taking photos, are still available while emergency locked."
%}

```lua
-- Lock (E-stop) the device:
emergency_lock()
```

# emergency_unlock()

**Unlocks** a locked (E-stopped) device.

```lua
-- Unlock the device:
emergency_unlock()
```

# soft_stop()

**Cancels all current and pending movement requests**. Unlike `emergency_lock()`, it will not lock the device nor will it reset the state of peripherals. Subsequent commands (including movement commands) will continue normally after a soft stop occurs, without requiring the device to be unlocked. This function can be used to pause FarmBot temporarily if a peripheral value changes mid-movement.

{%
include callout.html
type="info"
content="This is an advanced feature intended to be used in conjunction with [watch_pin()](../functions/pins.md#watch_pinpin-callback)."
%}

```lua
-- Soft stop the device:
soft_stop()
```

```lua
rotary_tool_motor_pin = 2
rotary_tool_load_sense_pin = 60
max_load = 90

-- Watcher function that soft stops the device and turns off the
-- rotary tool motor if the rotary tool load exceeds the max load
watcher = function(data)
    if (data.value > max_load) and (env("load") ~= "stalled") then
        env("load", "stalled")
        soft_stop()
        off(rotary_tool_motor_pin)
        toast("Rotary tool max load exceeded (load = " .. data.value .. ")", "warn")
    end
end

-- Watch the rotary tool load sense pin
watch_pin(rotary_tool_load_sense_pin, watcher)
```

---
title: "E-stop and Unlock"
slug: "e-stop-and-unlock"
description: "List of E-stop and Unlock Lua functions in FarmBot OS"
---

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

# soft_stop()

This is an advanced feature that is intended to be used in conjunction with `watch_pin`.

When called, `soft_stop` will cancel all current and pending movement requests. Unlike `emergency_lock`, it will not lock the device nor will it reset the state of peripherals. Commands (including movement commands) will continue normally after a soft stop occurs. This function can be used to pause FarmBot temporarily if a peripheral value changes mid-movement.
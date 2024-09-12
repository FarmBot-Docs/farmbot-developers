---
title: "Configuration"
slug: "configuration"
description: "List of configuration Python functions in the FarmBot Python library"
---

# read_status(path=None)

Reads the **device state tree**. The device state tree contains numerous properties that are relevant to the device's operation. It is the same state tree seen in [FarmBotJS](https://github.com/FarmBot/farmbot-js/blob/main/src/interfaces.ts#L6-L25).

```python
# Read the entire state tree
status = fb.read_status()
wifi = status["informational_settings"]["wifi_level_percent"]
fb.toast(f"WiFi strength is {wifi}%")

# Read a single property
raw_encoder_position_x = fb.read_status("location_data.raw_encoders.x")
fb.toast(raw_encoder_position_x)
```

```python
x_position = fb.read_status("location_data.position.x")
if x_position > 100:
  fb.toast("X is greater than 100")
else:
  fb.toast("X is less than or equal to 100")
```

# What's next?

 * [Coordinates](./coordinates.md)

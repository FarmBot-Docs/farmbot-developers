---
title: "Configuration"
slug: "configuration"
description: "List of configuration Lua functions in FarmBot OS"
---

# env(key, value) / env(key)

Store and retrieve **key/value pairs** to FarmBot's SD card.

* `key` and `value` must be strings.
* Values may not exceed 1,000 characters in length.
* ENVs will eventually sync with your web app account.

```lua
-- Store a value:
env("key", "value")

-- Example:
env("MY_API_TOKEN", "abc123")
```

```lua
-- Retrieve a value:
env("key")
-- Returns `nil` if no value is found.

-- Example:
api_token = env("MY_API_TOKEN")
if api_token then
  toast("Token is " .. api_token, "success")
else
  toast("Token not found", "error")
end
```

# read_status(...path?)

Reads the **device state tree**. The device state tree contains numerous properties that are relevant to the device's operation. It is the same state tree seen in [FarmBotJS](https://github.com/FarmBot/farmbot-js/blob/main/src/interfaces.ts#L6-L25).

```lua
-- Read the entire state tree:
read_status()

-- Example:
status = read_status()
wifi = status.informational_settings.wifi_level_percent
toast("WiFi strength is " .. wifi .. "%")

-- Read a single property:
read_status("path", "to", "property")

-- Example:
raw_encoder_position_x = read_status("location_data", "raw_encoders", "x")
toast(raw_encoder_position_x)
```

```lua
status = read_status()
if status.location_data.position.x > 100 then
  toast("X is greater than 100")
else
  toast("X is less than or equal to 100")
end
```

# fbos_version()

Returns a string representation of the **FarmBot OS version**.

```lua
fbos_version()
```

# firmware_version()

Returns a string representation of the **Farmduino/Arduino firmware version**.

```lua
firmware_version()
```

# get_device(property?)

Get **device properties**. This is the same [device resource found on the API](../../docs/web-app/api-docs.md#device).

```lua
-- Get all properties:
get_device()

-- Example:
device = get_device()
toast("FarmBot name is " .. device.name)

-- Get a single property:
get_device("property_name")

-- Example:
id = get_device("id")
toast("Device ID is " .. id)
```

# get_fbos_config(property?)

Get **FarmBot OS configuration properties**. This is the same [FarmBot OS configuration resource found on the API](../../docs/web-app/api-docs.md#fbos_config).

```lua
-- Get all properties:
get_fbos_config()

-- Example:
fbos_config = get_fbos_config()
toast("FarmBot's firmware hardware is " .. fbos_config.firmware_hardware)

-- Get a single property:
get_fbos_config("property_name")

-- Example:
firmware_hardware = get_fbos_config("firmware_hardware")
toast("FarmBot firmware hardware is " .. firmware_hardware)
```

# get_firmware_config(property?)

Get **firmware configuration properties**. This is the same [firmware configuration resource found on the API](../../docs/web-app/api-docs.md#firmware_config).

```lua
-- Get all properties:
get_firmware_config()

-- Example:
firmware_config = get_firmware_config()
toast("Encoder enabled Z is " .. firmware_config.encoder_enabled_z)

-- Get a single property:
get_firmware_config("property_name")

-- Example:
encoder_enabled_z = get_firmware_config("encoder_enabled_z")
toast("Encoder enabled Z is " .. encoder_enabled_z)
```

# update_device(params)

Update **device properties**. This is the same [device resource found on the API](../../docs/web-app/api-docs.md#device).

```lua
update_device({key = "value"})

-- Example:
update_device({name = "Test Farmbot"})
```

# update_fbos_config()

Update **FarmBot OS configuration properties**. This is the same [FarmBot OS configuration resource found on the API](../../docs/web-app/api-docs.md#fbos_config).

```lua
update_fbos_config({key = "value"})

-- Example:
update_fbos_config({disable_factory_reset = true})
```

# update_firmware_config(params)

Update **firmware configuration properties**. This is the same [firmware configuration resource found on the API](../../docs/web-app/api-docs.md#firmware_config).

```lua
update_firmware_config({key = "value"})

-- Example:
update_firmware_config({encoder_enabled_z = 1.0})
```

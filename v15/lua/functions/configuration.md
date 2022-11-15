---
title: "Configuration"
slug: "configuration"
description: "List of configuration Lua functions in FarmBot OS"
---

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

# read_status(...path?)

`read_status(...path?)` reads the entire device state tree into memory.

The device state tree contains numerous properties that are relevant to the device's operation. It is the same state tree seen in [FarmBotJS](https://github.com/FarmBot/farmbot-js/blob/main/src/interfaces.ts#L6-L25).

```lua
-- Provide a path to the property you are interested in:
read_status("location_data", "raw_encoders", "x")

-- Alternative syntax:
status = read_status().location_data.raw_encoders.x
```

# fbos_version()

Returns a string representation of FarmBot OS's version.

```lua
fbos_version()
```

# firmware_version()

Returns a string representation of the firmware version on the Farmduino/Arduino.

```lua
firmware_version()
```

# get_device(property?)

Fetch device properties. This is the same [device resource found on the API](../../docs/web-app/api-docs.md#get-apidevice).

```lua
-- Every property:
get_device()

-- Single property:
get_device("name")
```

# get_fbos_config(property?)

Fetch FarmBot OS configuration properties. This is the same [FarmBot OS configuration resource found on the API](../../docs/web-app/api-docs.md#get-apifbos_config).

```lua
-- Fetch all properties:
get_fbos_config()

-- Fetch single property:
get_fbos_config("disable_factory_reset")
```

# get_firmware_config(property?)

Fetch firmware configuration properties. This is the same [firmware configuration resource found on the API](../../docs/web-app/api-docs.md#get-apifirmware_config).

```lua
get_firmware_config()
get_firmware_config("encoder_enabled_z")
```

# update_device(params)

Update device properties. This is the same [device resource found on the API](../../docs/web-app/api-docs.md#get-apidevice).

```lua
update_device({key = "value"})
update_device({name = "Test Farmbot"})
```

# update_fbos_config()

Update FarmBot OS configuration properties. This is the same [FarmBot OS configuration resource found on the API](../../docs/web-app/api-docs.md#get-apifbos_config).

```lua
update_fbos_config({key = "value"})
update_fbos_config({disable_factory_reset = true})
```

# update_firmware_config(params)

Update firmware configuration properties. This is the same [firmware configuration resource found on the API](../../docs/web-app/api-docs.md#get-apifirmware_config).

```lua
update_firmware_config({key = "value"})
update_firmware_config({encoder_enabled_z = 1.0})
```
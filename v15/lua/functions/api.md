---
title: "API"
slug: "api"
description: "List of API Lua functions in FarmBot OS"
---

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
  -- OPTIONAL. Must be a string. Use included JSON library for
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

# inspect(any)

Alias for `json.encode`.
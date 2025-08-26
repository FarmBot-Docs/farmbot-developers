---
title: "API"
slug: "api"
description: "List of API Lua functions in FarmBot OS"
---

# api(options)

Performs an **HTTP request to the FarmBot API**. This convenience function provides a subset of the functionality of the [http()](#httpparams) helper. Note the following key differences:

 * You do not need to run `json.encode` on inputs.
 * You do not need to run `json.decode` on outputs.
 * The only supported request format is JSON.
 * You do not need to pass an `auth_token()` in the header.
 * The base URL is not configurable. `https://my.farm.bot` is the only URL supported.
 * `body` is optional for `GET` requests.
 * Returns `nil` if there was an error.
 * Errors are sent to the log stream (if any).

{%
include callout.html
type="warning"
title="Making requests"
content="Making requests other than GET to the API will permanently alter the data in your account. Be especially careful making DELETE requests and POST requests to singular resources, like the /device endpoint, as the API will destroy data that cannot be recovered. Altering data through the API may cause account instability."
%}

```lua
-- Create a new point at (200, 200, 0) with a radius of 100
result = api({
    method = "post",
    url = "/api/points",
    body = {
        x = 200,
        y = 200,
        z = 0,
        radius = 100,
        pointer_type = "GenericPointer"
    }
})

if result then
    toast("Point creation ok", "debug")
else
    toast("Error - See logs for details", "error")
end
```

```lua
-- Fetch all points from the API
points = api({
    method = "get",
    url = "/api/points"
})
```

```lua
-- Update the color and size of point with ID 1
api({
    method = "put",
    url = "/api/points/1",
    body = {
        meta = {
            color = "red"
        },
        radius = 250
    }
})
```

# auth_token()

Returns the device's **authorization token** (string). This value can be used to access API resources without the need to store account passwords in Lua code or ENV vars.

```lua
-- Fetch all points from the API
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

Performs an **HTTP request**.

{%
include callout.html
type="info"
title="Using the FarmBot API?"
content="If you are making an API call to the FarmBot API, we recommend the simpler [api()](#apioptions) helper."
%}

{%
include callout.html
type="warning"
title="Making requests"
content="Making requests other than GET to the API will permanently alter the data in your account. Be especially careful making DELETE requests and POST requests to singular resources, like the /device endpoint, as the API will destroy data that cannot be recovered. Altering data through the API may cause account instability."
%}

{%
include callout.html
type="info"
title="Sidecar"
content="For an example of how to use the `http` function to communicate with a sidecar, see the [sidecar docs](../../docs/farmbot-os/sidecar-hardware.md)."
%}

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
  -- OPTIONAL. Must be a string. Use included JSON library for JSON APIs
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
    -- `status`: Number               - Response code. Example: 200.
    -- `body`: String                 - Response body. Always a string.
    -- `headers`: Map<String, String> - Response headers.
end
```

```lua
-- Get today's precipitation forecast from Open Meteo
request_url =
    "https://api.open-meteo.com/v1/forecast" ..
    "?latitude=" .. get_device("lat") ..
    "&longitude=" .. get_device("lng") ..
    "&timezone=auto&daily=precipitation_sum"
debug(request_url)
api_response = http({
  url=request_url
})
forecast = json.decode(api_response.body)

-- Display the result
toast("Daily precipitation: " .. forecast.daily.precipitation_sum[1] .. "mm")
```

# json.decode(string)

Converts a JSON encoded string to a Lua table.

```lua
lua_data = json.decode('{"foo":"bar","example":123}')
-- { foo="bar", example=123 }
```

# json.encode(any)

Converts a Lua variable into stringified JSON.

```lua
json_data = json.encode({ foo="bar", example=123 })
-- => '{"foo":"bar","example":123}'
```

# inspect(any)

Alias for [json.encode()](#jsonencodeany).

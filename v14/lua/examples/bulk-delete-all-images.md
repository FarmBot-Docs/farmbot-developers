---
title: "Bulk Delete All Images"
slug: "bulk-delete-all-images"
description: "Clear all images from your account using Lua"
---

{%
include callout.html
type="warning"
title="There is no undo!"
content="Once you clear images from your account, they are gone forever."
%}

All FarmBot resources (points, images, sequences, etc..) can be managed via the [REST API](../../Documentation/web-app/rest-api.md).

Managing REST resources requires an HTTP client and an authorization token. The Lua sandbox exposes an `http()` method to execute HTTP requests. It also provides an `auth_token()` helper so that users do not need to copy/paste passwords into Lua snippets.

By using `http()` and `auth_token()`, it is possible to modify and delete any REST resource.

The example below shows how a user could delete all images associated with their account. This is particularly useful when performing high-throughput operations, such as full garden scans.

**NOTE:** Self-hosted users will need to change the value of `protocol` and `host` in the snippet below.

```lua
-- IMPORTANT: Change these values if you are self hosted:
protocol = "https"
host = "my.farm.bot"

-- BEGIN --

url = protocol .. "://" .. host .. "/api/images/"
headers = {
    Authorization = ("bearer " .. auth_token()),
    Accept = "application/json"
}
response, error = http({url = url, method = "GET", headers = headers})

if error then
    send_message("error", "ERROR: " .. inspect(error), "toast")
    return
end

images = json.decode(response.body)

for k in pairs(images) do
    image = images[k]
    send_message("info", "Delete image #" .. image.id, "toast")
    wait(555)
    http({url = url .. image.id, method = "DELETE", headers = headers})
end
```

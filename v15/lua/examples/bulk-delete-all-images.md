---
title: "Bulk Delete All Images"
slug: "bulk-delete-all-images"
description: "Clear all images from your account using Lua"
---

All FarmBot resources (points, images, sequences, etc..) can be managed via the [REST API](../../docs/web-app/rest-api.md). The Lua sandbox exposes the [api()](../functions/api.md#apioptions) method to execute HTTP requests to the FarmBot API, providing a more convenient alternative to using [http()](../functions/api.md#httpparams) and [auth_token()](../functions/api.md#auth_token).

The example below shows how a user could delete all images associated with their account. This may be particularly useful after performing many high-throughput operations, such as full garden scans for research purposes.

{%
include callout.html
type="warning"
title="There is no undo!"
content="Once you clear images from your account, they are gone forever."
%}

```lua
url = "/api/images/"
images = api({url = url})
job_name = "Deleting " .. tostring(#images) .. " Images"

set_job(job_name)

for k, image in ipairs(images) do
    set_job(job_name, {
      percent = math.floor((k / #images) * 100)
    })
    debug("Deleting image #" .. image.id)
    api({url = url .. image.id, method = "DELETE"})
    wait(500)
end

complete_job(job_name)
```

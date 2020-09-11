---
title: "Publishing Resource Updates via MQTT"
slug: "create-a-resource"
hidden: false
createdAt: "2018-08-20T16:02:57.086Z"
updatedAt: "2019-09-30T23:17:06.712Z"
---
# Send an Update

Send an MQTT message in the format of:

```
bot/device_<id>/resources_v0/<action>/<resource type>/<Transaction UUID>/<resource_id or 0>
```

Example 1-1:

```
bot/device_3/resources_v0/destroy/Sequence/123-456/2
```

NOTES:

 * `<Transaction UUID>` can be any user-defined string. Ensure that the string is unique. We recommend using UUIDs.
 * `<resource_id>` This is the `.id` property of the resource you are deleting.
 * `<action>` Only `destroy` and `save` are supported as of July 2018.
 * `<resource type>` See "resource" column of the table above. **Case sensitive**.
 * `<resource_id or 0>` Use the resource ID for deletion and updates. Use `0` for the creation of new resources.
**For deletion messages** the body of the message is unimportant and is discarded by the server.

# Handling Failed Requests

If your message is malformed or the server was unable to complete the request, you will receive an error message on the following MQTT channel:

```
bot/device_<id>/from_api
```

The message will take the same format as RPC errors:

```
{
  "kind": "rpc_error",
  "args": { "label": "THE UUID YOU GAVE THE SERVER" },
  "body": [
    {
      "kind": "explanation",
      "args": { "message": "Human readable explanation message" }
    }
  ]
}
```

# Confirming a Transaction

If successful, an `rpc_ok` CeleryScript node will be streamed to the following MQTT channel:

```
bot/device_<id>/from_api
```

**This is not a JSON resource.** It is merely an indication that the server has accepted the request and processed it. The resource itself will be streamed over the `auto_sync`* channel. For more information about parsing auto-sync messages, see the documentation entry "[Subscribing to Resource Updates](doc:realtime-updates-auto-sync)".

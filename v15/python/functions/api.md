---
title: "API"
slug: "api"
description: "List of API Python functions in the FarmBot Python library"
---

Perform **HTTP requests to the FarmBot API**.

{%
include callout.html
type="warning"
title="Making requests"
content="Making requests other than GET to the API will permanently alter the data in your account. Be especially careful making DELETE requests and POST requests to singular resources, like the /device endpoint, as the API will destroy data that cannot be recovered. Altering data through the API may cause account instability."
%}

{%
include callout.html
type="success"
title="API endpoint documentation"
content="Not sure which endpoint to access? [Find the list here](../../docs/web-app/api-docs.md)."
%}

# api_get(endpoint, database_id=None)

Get information about a specific endpoint.

```python
# Get info from an endpoint
peripherals = fb.api_get("peripherals")
```

```python
# Get a specific resource by ID
peripheral = fb.api_get("peripherals", 12345)
```

```python
# Get info from a singular endpoint
device = fb.api_get("device")
```

# api_post(endpoint, new_data)

Create new information contained within an endpoint.

```python
# Add a new peripheral
new_peripheral = fb.api_post("peripherals", {
    "label": "LED",
    "pin": 13,
    "mode": 0,
})
```

# api_patch(endpoint, new_data, database_id=None)

Change information contained within an endpoint.

```python
# Update a peripheral
updated_peripheral = fb.api_patch("peripherals", {
    "mode": 1,
}, 12345)
```

# api_delete(endpoint, database_id)

Delete information contained within an endpoint.

```python
# Delete a peripheral
fb.api_delete("peripherals", 12345)
```

# What's next?

 * [Message Broker](./message-broker.md)

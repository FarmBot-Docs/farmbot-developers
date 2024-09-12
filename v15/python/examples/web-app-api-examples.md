---
title: "Web App API Examples"
slug: "web-app-api-examples"
description: "Retrieve and modify data in the FarmBot [Web App](../../docs/web-app.md) using Python"
---

These examples use concepts in [REST API](../../docs/web-app/rest-api.md).

{%
include callout.html
type="info"
title="Authorization required"
content='To get the authorization token required in these examples (`TOKEN`), see [Authorization](../authorization.md).'
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
title="Libraries required"
content='The following examples require either the FarmBot Python library or the Requests library. To install, run `python -m pip install --upgrade farmbot requests` in the command line.'
%}

# GET points

## via FarmBot Python library
```python
from farmbot import Farmbot

# TOKEN = ...

fb = Farmbot()
fb.set_token(TOKEN)

points = fb.api_get('points')
```
You should see a list of your FarmBot Web App account points in the output.

## via Python

```python
import json
import requests

# TOKEN = ...

headers = {'Authorization': 'Bearer ' + TOKEN['token']['encoded'],
           'content-type': "application/json"}
response = requests.get(f'https:{TOKEN['token']['unencoded']['iss']}/api/points', headers=headers)
points = response.json()
print(json.dumps(points, indent=2))
```
You should see a list of your FarmBot Web App account points in the output.

# Add a new plant to your garden

## via FarmBot Python library
```python
from farmbot import Farmbot

# TOKEN = ...

fb = Farmbot()
fb.set_token(TOKEN)

new_cabbage = {
    "name": "Cabbage",              # Point name
    "pointer_type": "Plant",        # Point type
    "x": 400,                       # x-coordinate
    "y": 300,                       # y-coordinate
    "z": 0,                         # z-coordinate
    "openfarm_slug": "cabbage",     # Plant type
    "plant_stage": "planned",       # Point status
}

fb.api_post("points", new_cabbage) # Add plant to endpoint
```

## via Python

```python
import json
import requests

# TOKEN = ...

headers = {'Authorization': 'Bearer ' + TOKEN['token']['encoded'],
           'content-type': 'application/json'}
new_cabbage = {
    "name": "Cabbage",              # Point name
    "pointer_type": "Plant",        # Point type
    "x": 400,                       # x-coordinate
    "y": 300,                       # y-coordinate
    "z": 0,                         # z-coordinate
    "openfarm_slug": "cabbage",     # Plant type
    "plant_stage": "planned",       # Point status
}
response = requests.post(f'https:{TOKEN['token']['unencoded']['iss']}/api/points',
                         headers=headers, json=new_cabbage)
print(json.dumps(response.json(), indent=2))
```

# POST log message

## via FarmBot Python library
```python
from farmbot import Farmbot

# TOKEN = ...

fb = Farmbot()
fb.set_token(TOKEN)

fb.log('Hello!', message_type='info')
```
You should see a copy of the log message now saved in your FarmBot Web App account in the output.

## via Python

```python
import json
import requests

# TOKEN = ...

headers = {'Authorization': 'Bearer ' + TOKEN['token']['encoded'],
           'content-type': 'application/json'}
log = {'message': 'Hello!', 'type': 'info'}
response = requests.post(f'https:{TOKEN['token']['unencoded']['iss']}/api/logs',
                         headers=headers, json=log)
print(json.dumps(response.json(), indent=2))
```
You should see a copy of the log message now saved in your FarmBot Web App account in the output.

For a list of available endpoints, see [the REST API resource list](../../docs/web-app/rest-api.md#resources).

# What's next?

 * [API example requests](../../docs/web-app/api-docs.md)

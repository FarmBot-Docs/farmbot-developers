---
title: "Web App API Examples"
slug: "web-app-api-examples"
description: "Retrieve and modify data in the FarmBot [Web App](../docs/web-app.md) using Python"
---

These examples use concepts in [REST API](../docs/web-app/rest-api.md).

{%
include callout.html
type="info"
title="Authorization required"
content='To get the authorization token required in these examples (`TOKEN`), see [Authorization](authorization.md).'
%}

{%
include callout.html
type="info"
title="Libraries required"
content='The following examples require the Requests library. To install, run `python -m pip install requests` in the command line.'
%}

# GET points

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

# POST log message

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

For a list of available endpoints, see [the REST API resource list](../docs/web-app/rest-api.md#resources) and [API example requests](../docs/web-app/api-docs.md).

---
title: "Web App API Examples"
slug: "web-app-api-examples"
excerpt: "Retrieve and modify data in the FarmBot [Web App](/v6/Documentation/web-app.md) using Python"
hidden: false
createdAt: "2018-05-09T20:39:51.188Z"
updatedAt: "2018-05-31T01:28:14.646Z"
---


__get your token:__

```python
#!/usr/bin/env python

'''Get a token from the FarmBot Web App.'''

import requests

# Inputs:
EMAIL = 'farmbot@account.email'
PASSWORD = 'password'

# Get your FarmBot Web App token.
headers = {'content-type': 'application/json'}
user = {'user': {'email': EMAIL, 'password': PASSWORD}}
response = requests.post('https://my.farmbot.io/api/tokens',
                         headers=headers, json=user)
TOKEN = response.json()['token']['encoded']
```




__GET points:__

```python
import requests

API_TOKEN = 'my token'
headers = {'Authorization': 'Bearer ' + API_TOKEN,
           'content-type': "application/json"}
response = requests.get('https://my.farmbot.io/api/points', headers=headers)
points = response.json()
```




__POST log message:__

```python
import requests

TOKEN = 'paste_token_here'

headers = {'Authorization': 'Bearer ' + TOKEN,
           'content-type': 'application/json'}
log = {'message': 'Hello!', 'type': 'info'}
response = requests.post('https://my.farmbot.io/api/logs',
                         headers=headers, json=log)
```


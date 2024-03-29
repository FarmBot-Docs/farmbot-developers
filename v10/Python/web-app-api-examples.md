---
title: "Web App API Examples"
slug: "web-app-api-examples"
description: "Retrieve and modify data in the FarmBot [Web App](../Documentation/web-app.md) using Python"
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

Use the value of `TOKEN` generated by this first example in the following examples:


__GET points:__

```python
import requests

TOKEN = 'paste_token_here'

headers = {'Authorization': 'Bearer ' + TOKEN,
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


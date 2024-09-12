---
title: "Authorization"
slug: "authorization"
description: "Use Python to get a token for authorizing requests"
---

{%
include callout.html
type="warning"
title="Storing your authorization token"
content="Store your authorization token securely. It grants full access and control over your FarmBot and your FarmBot Web App account."
%}

{%
include callout.html
type="info"
title="Libraries required"
content='The following examples require either the FarmBot Python library or the **Requests** library. To install, run `python -m pip install --upgrade farmbot requests` in the command line. Your system may require you to use `python3` instead of `python`. Using a [virtual environment](https://docs.python.org/3/library/venv.html) is highly recommended.'
%}

{%
include callout.html
type="info"
title="Running python code"
content='You can execute python code by pasting it into a new file such as `run.py` which can be executed via `python run.py` in the command line.'
%}

# Get your token

## via the FarmBot Python library
```python
from farmbot import Farmbot
from getpass import getpass

# inputs
SERVER = input('FarmBot Web App account server (press <Enter> for https://my.farm.bot): ') or 'https://my.farm.bot'
EMAIL = input('FarmBot Web App account login email: ')
PASSWORD = getpass('FarmBot Web App account login password: ')

fb = Farmbot()
TOKEN = fb.get_token(EMAIL, PASSWORD, SERVER)
print(f'{TOKEN = }')
```

## via Python
```python
import json
from getpass import getpass
import requests

# inputs
SERVER = input('FarmBot Web App account server (press <Enter> for https://my.farm.bot): ') or 'https://my.farm.bot'
EMAIL = input('FarmBot Web App account login email: ')
PASSWORD = getpass('FarmBot Web App account login password: ')

# get your FarmBot authorization token
headers = {'content-type': 'application/json'}
user = {'user': {'email': EMAIL, 'password': PASSWORD}}
response = requests.post(f'{SERVER}/api/tokens',
                         headers=headers, json=user)
TOKEN = response.json()
print(f'{TOKEN = }')
```

# Use your token

Use the value of `TOKEN` in examples.
You may either copy and paste the token data in,
or save it to a file and load it when needed.
Consider the security of the approach you choose.

## Copy and paste
Replace the following line when it appears in examples:
```python
# TOKEN = ...
```
with your token data pasted from running the [get your token](#get-your-token) example code above. For example:
```python
TOKEN = {"token": {"unencoded":{"aud":"unknown","sub":123,"iat":1234567890,"jti":"b52b68fb-5cc2-a9be-7aaf-ecc8837a2fa9","iss":"//my.farm.bot:443","exp":1234567890,"mqtt":"abc-def.rmq.cloudamqp.com","bot":"device_456","vhost":"xqigvtsn","mqtt_ws":"wss://abc-def.rmq.cloudamqp.com:443/ws/mqtt"},"encoded":"rFr6edHr11GDLITjaanofZxC4dM6TCC9UuHG.Kzx87wRkKvejWWjuigwX0i3hO8hi97pJ70m1bD2I5JRuksjE6E3gRIOVwoF5f8X4UCtftuVCsGttOayPxKUiuLMKZRJlUEH7ssyXCawVeBUf34B5NAy172aqdm3WGsQkFITOQgCTjKddYXn7Fs2rZow3N9YCkbYhoweoFyndhdF9ST8NmMgpFm3VfocYgNKukGI1gi2LjYoRdyPtdjGK1jwW3KKqyNWuOfkQVNxCg6c9xvQDqnbxiDLRfySn8HOQ9ElsXlN9LIv8PGN07EKKcbkyxsSXmYWHfwn8dOnzeNdL4OFiYNyLyB51YC4cukVROhMKfBbv3Vam6PgObmU4Jq2HF5xEru4MPORt741s8im84oP6.OqDC3SUJ7TSNV1NYii5BOONidacLifUfdaRGwjD05XNXdMCWlulnDCD4CWy7kFEAwA8pqxx9lCfqaA7ezK6054DLhtk0gsWu7gQ3oTjg1fZXinIiI2fLmxXhyisoFrudzwqryhwSmBQMAz3eVkdeyouJTgphFrbXjWnRYEk41iNXT275h68j3EtxSDqOpCZi4kqcuBUPltjS063FEYXa1JKzHThUQFpGVP2wg6doEWaNPAadjBBvOK7Ja6SEIONmiDNa3AfKqYgWoKGRyhQ2fFCZjnx53d7EgVRdBDdVxHhX6P7RghHZcAZ7d5cODz9d7b6IZWbyVDOj4Zd8RkRNQN"}, "user": {}}
```

## Saving to and loading from a file
Add the following to the end of the [get your token](#get-your-token) example code above and run it again with the addition.
```python
# save token to file
with open('farmbot_authorization_token.json', 'w') as f:
    f.write(json.dumps(TOKEN))
    print('token saved to file')
```

Replace the following line when it appears in examples:
```python
# TOKEN = ...
```
with:
```python
# load token from file
with open('farmbot_authorization_token.json', 'r') as f:
    TOKEN = json.load(f)
```

# What's next?

 * [Examples](examples.md)
 * [Functions](functions.md)
 * [Settings](settings.md)

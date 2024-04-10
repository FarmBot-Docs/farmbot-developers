---
title: "Example API requests"
slug: "api-docs"
---

The document that follows is a list of **example API requests**. It serves as a guide for developers who wish to see the schema and existence of particular API endpoints quickly.

# ai

|Field|Type|`GET`|`GET/:id`|`POST`|`PATCH`|`DELETE`|
|---|---|:---:|:---:|:---:|:---:|:---:|
|`prompt`<br>Instructions for model to follow.|string|||📝|||
|`context_key`<br>Type of generation request.|"title" \| "color" \| "description" \| "lua"|||📝|||
|`sequence_id`<br>For sequence "title", "color", and "description" auto-generation requests, the ID of the sequence to summarize.|integer \| null|||📝|||

## POST /api/ai
```python
import json
import requests

# TOKEN = ...

url = f'https:{TOKEN['token']['unencoded']['iss']}/api/ai'
headers = {'Authorization': 'Bearer ' + TOKEN['token']['encoded'],
           'content-type': 'application/json'}
payload = {
    'prompt': 'write code',
    'context_key': 'lua',
    'sequence_id': None,
}
response = requests.post(url, headers=headers, json=payload, stream=True)
for line in response.iter_lines():
    print(line.decode('utf-8'))
```
output:
````
```lua
-- Move FarmBot to the home position for all axes
go_to_home("all")
```
````

# ai_feedbacks

|Field|Type|`GET`|`GET/:id`|`POST`|`PATCH`|`DELETE`|
|---|---|:---:|:---:|:---:|:---:|:---:|
|`id`<br>Unique identifier set by the database.|integer||||||
|`created_at`<br>Date and time of creation set by the database.|timestamp||||||
|`updated_at`<br>Date and time of most recent update set by the database.|timestamp||||||
|`prompt`<br>A copy of the instructions for the auto-generation request.|string|||📝|||
|`reaction`<br>The feedback for the outcome of the prompt.|"good" \| "bad"|||📝|||

## POST /api/ai_feedbacks
```python
import json
import requests

# TOKEN = ...

url = f'https:{TOKEN['token']['unencoded']['iss']}/api/ai_feedbacks'
headers = {'Authorization': 'Bearer ' + TOKEN['token']['encoded'],
           'content-type': 'application/json'}
payload = {
    'prompt': 'write code',
    'reaction': 'good',
}
response = requests.post(url, headers=headers, json=payload)
print(json.dumps(response.json(), indent=2))
```
output:
```json
{
  "id": 1,
  "created_at": "2024-04-10T17:53:37.120Z",
  "updated_at": "2024-04-10T17:53:37.120Z",
  "prompt": "write code",
  "reaction": "good"
}
```

# alerts

|Field|Type|`GET`|`GET/:id`|`POST`|`PATCH`|`DELETE`|
|---|---|:---:|:---:|:---:|:---:|:---:|
|`id`<br>Unique identifier set by the database.|integer|📖||||🗑|
|`created_at`<br>Date and time of creation set by the database.|timestamp|📖||||🗑|
|`updated_at`<br>Date and time of most recent update set by the database.|timestamp|📖||||🗑|
|`problem_tag`<br>Type of alert.|"api.seed_data.missing" \| "api.documentation.unread" \| "api.tour.not_taken" \| "api.user.not_welcomed" \| "api.bulletin.unread" \| "api.demo_account.in_use"|📖||||🗑|
|`slug`<br>Defaults to random UUID.|string|📖||||🗑|
|`priority`<br>Importance for sorting.|integer|📖||||🗑|

## GET /api/alerts
```python
import json
import requests

# TOKEN = ...

url = f'https:{TOKEN['token']['unencoded']['iss']}/api/alerts'
headers = {'Authorization': 'Bearer ' + TOKEN['token']['encoded'],
           'content-type': 'application/json'}
response = requests.get(url, headers=headers)
print(json.dumps(response.json(), indent=2))
```
output:
```json
[
  {
    "id": 1,
    "created_at": 1643843681,
    "updated_at": "2022-02-02T23:14:41.694Z",
    "priority": 100,
    "problem_tag": "api.seed_data.missing",
    "slug": "fc07c4d5-aba0-4782-8c71-e443f88430e9"
  }
]
```

## DELETE /api/alerts/1
```python
import json
import requests

# TOKEN = ...

url = f'https:{TOKEN['token']['unencoded']['iss']}/api/alerts/1'
headers = {'Authorization': 'Bearer ' + TOKEN['token']['encoded'],
           'content-type': 'application/json'}
response = requests.delete(url, headers=headers)
print(json.dumps(response.json(), indent=2))
```
output:
```json
{
  "id": 1,
  "created_at": 1643843681,
  "updated_at": "2022-02-02T23:14:41.694Z",
  "priority": 100,
  "problem_tag": "api.seed_data.missing",
  "slug": "fc07c4d5-aba0-4782-8c71-e443f88430e9"
}
```

# corpus

|Field|Type|`GET`|`GET/:id`|`POST`|`PATCH`|`DELETE`|
|---|---|:---:|:---:|:---:|:---:|:---:|
|*corpus*<br>Celery Script corpus.|object|📖|||||

## GET /api/corpus
```python
import json
import requests

# TOKEN = ...

url = f'https:{TOKEN['token']['unencoded']['iss']}/api/corpus'
headers = {'Authorization': 'Bearer ' + TOKEN['token']['encoded'],
           'content-type': 'application/json'}
response = requests.get(url, headers=headers)
print(json.dumps(response.json(), indent=2))
```
output:
```json
{
  "version": 20180209,
  "enums": [
    {
...
```

# curves

|Field|Type|`GET`|`GET/:id`|`POST`|`PATCH`|`DELETE`|
|---|---|:---:|:---:|:---:|:---:|:---:|
|`id`<br>Unique identifier set by the database.|integer|📖|📖|||🗑|
|`created_at`<br>Date and time of creation set by the database.|timestamp|📖|📖|||🗑|
|`updated_at`<br>Date and time of most recent update set by the database.|timestamp|📖|📖|||🗑|
|`name`<br>Curve name.|string|📖|📖|📝(required)|📝|🗑|
|`type`<br>Curve type.|"water" \| "spread" \| "height"|📖|📖|📝(required)|📝|🗑|
|`data`<br>Curve data.|{[day: string]: value: integer}|📖|📖|📝(required)|📝|🗑|

## GET /api/curves
## GET /api/curves/1
## DELETE /api/curves/1
## PATCH /api/curves/1
## POST /api/curves
```python
import json
import requests

# TOKEN = ...

url = f'https:{TOKEN['token']['unencoded']['iss']}/api/curves'
headers = {'Authorization': 'Bearer ' + TOKEN['token']['encoded'],
           'content-type': 'application/json'}
payload = {
    'name': 'Curve 1',
    'type': 'water',
    'data': {
        '1': 1,
        '100': 100
    }
}
response = requests.post(url, headers=headers, json=payload)
print(json.dumps(response.json(), indent=2))
```
output:
```json
{
  "id": 1,
  "created_at": "2024-04-10T18:10:42.429Z",
  "updated_at": "2024-04-10T18:10:42.429Z",
  "name": "Curve 1",
  "type": "water",
  "data": {
    "1": 1,
    "100": 100
  }
}
```

# demo_account

|Field|Type|`GET`|`GET/:id`|`POST`|`PATCH`|`DELETE`|
|---|---|:---:|:---:|:---:|:---:|:---:|
|`secret`<br>Password.|string|||📝|||
|`product_line`<br>FarmBot model.|"express_1.0" \| "express_1.1" \| "express_1.2" \| "express_xl_1.0" \| "express_xl_1.1" \| "express_xl_1.2" \| "genesis_1.2" \| "genesis_1.3" \| "genesis_1.4" \| "genesis_1.5" \| "genesis_1.6" \| "genesis_1.7" \| "genesis_xl_1.4" \| "genesis_xl_1.5" \| "genesis_xl_1.6" \| "genesis_xl_1.7" \| "none"|||📝|||

## POST /api/demo_account
```python
import json
import requests

# TOKEN = ...

url = f'https:{TOKEN['token']['unencoded']['iss']}/api/demo_account'
headers = {'Authorization': 'Bearer ' + TOKEN['token']['encoded'],
           'content-type': 'application/json'}
payload = {
    'secret': 'password',
    'product_line': 'genesis_1.7',
}
response = requests.post(url, headers=headers, json=payload)
print(json.dumps(response.json(), indent=2))
```
output:
```json
{}
```

# device

|Field|Type|`GET`|`GET/:id`|`POST`|`PATCH`|`DELETE`|
|---|---|:---:|:---:|:---:|:---:|:---:|
|`id`<br>Unique identifier set by the database.|integer|📖||||🗑|
|`created_at`<br>Date and time of creation set by the database.|timestamp|📖||||🗑|
|`updated_at`<br>Date and time of most recent update set by the database.|timestamp|📖||||🗑|
|`fb_order_number`<br>Order number.|string \| null|📖|||📝|🗑|
|`fbos_version`<br>FarmBot OS version.|string|📖||||🗑|
|`indoor`<br>Is your FarmBot indoors?|boolean|📖||📝|📝|🗑|
|`last_saw_api`<br>Datetime of last API visit.|timestamp|📖||||🗑|
|`lat`<br>Latitude.|float|📖||📝|📝|🗑|
|`lng`<br>Longitude.|float|📖||📝|📝|🗑|
|`mounted_tool_id`<br>The ID of the tool currently attached to the UTM.|integer|📖|||📝|🗑|
|`name`<br>FarmBot name.|string|📖||📝|📝|🗑|
|`ota_hour`<br>Over-the-air update local time.|0-23 \| null|📖|||📝|🗑|
|`ota_hour_utc`<br>Over-the-air update UTC time.|0-23 \| null|📖||||🗑|
|`rpi`<br>FarmBot computer model.|"3" \| "4" \| "01" \| "02"|📖||📝|📝|🗑|
|`serial_number`<br>FarmBot serial number.|string|📖||||🗑|
|`setup_completed_at`<br>Datetime device setup completed.|timestamp|📖|||📝|🗑|
|`throttled_at`<br>Datetime device throttle begin.|timestamp|📖||||🗑|
|`throttled_until`<br>Datetime device throttle end.|timestamp|📖||||🗑|
|`timezone`<br>Timezone.|string|📖||📝|📝|🗑|
|`max_log_age_in_days`<br>Logs deleted after __ days.|integer|📖||||🗑|
|`max_sequence_count`<br>Maximum number of allowed sequences.|integer|📖||||🗑|
|`max_sequence_length`<br>Maximum allowed sequence length.|integer|📖||||🗑|
|`tz_offset_hrs`<br>Hours offset from UTC.|integer|📖||||🗑|

## POST /api/device
## DELETE /api/device
## GET /api/device
```python
import json
import requests

# TOKEN = ...

url = f'https:{TOKEN['token']['unencoded']['iss']}/api/device'
headers = {'Authorization': 'Bearer ' + TOKEN['token']['encoded'],
           'content-type': 'application/json'}
response = requests.get(url, headers=headers)
print(json.dumps(response.json(), indent=2))
```
output:
```json
{
  "id": 29,
  "created_at": "2022-02-02T23:14:15.261Z",
  "updated_at": "2022-02-02T23:14:15.261Z",
  "fb_order_number": null,
  "fbos_version": "17.0.0",
  "indoor": false,
  "last_saw_api": null,
  "lat": null,
  "lng": null,
  "mounted_tool_id": null,
  "name": "Okra",
  "ota_hour_utc": 6,
  "ota_hour": 3,
  "rpi": null,
  "serial_number": "0827898855f3f79e81037a4f3a119b00",
  "setup_completed_at": null,
  "throttled_at": null,
  "throttled_until": null,
  "timezone": "W-SU",
  "max_log_age_in_days": 0,
  "max_sequence_count": 0,
  "max_sequence_length": 0,
  "tz_offset_hrs": 3
}
```
## PATCH /api/device
## POST /api/device/reset

|Field|Type|`GET`|`GET/:id`|`POST`|`PATCH`|`DELETE`|
|---|---|:---:|:---:|:---:|:---:|:---:|
|`password`<br>Account password.|string|||📝(required)|||

## POST /api/device/seed

|Field|Type|`GET`|`GET/:id`|`POST`|`PATCH`|`DELETE`|
|---|---|:---:|:---:|:---:|:---:|:---:|
|`product_line`<br>FarmBot model.|"express_1.0" \| "express_1.1" \| "express_1.2" \| "express_xl_1.0" \| "express_xl_1.1" \| "express_xl_1.2" \| "genesis_1.2" \| "genesis_1.3" \| "genesis_1.4" \| "genesis_1.5" \| "genesis_1.6" \| "genesis_1.7" \| "genesis_xl_1.4" \| "genesis_xl_1.5" \| "genesis_xl_1.6" \| "genesis_xl_1.7" \| "none"|||📝(required)|||
|`demo`<br>Seed a demo account.|boolean|||📝|||

## GET /api/device/sync
## POST /api/device

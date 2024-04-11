---
title: "Example API requests"
slug: "api-docs"
---

The document that follows is a list of **example API requests**. It serves as a guide for developers who wish to see the schema and existence of particular API endpoints quickly.

{%
include callout.html
type="warning"
title="Making requests"
content="Making requests other than GET to the API will permanently alter the data in your account. Be especially careful making DELETE requests and POST requests to singular resources, like the /device endpoint, as the API will destroy data that cannot be recovered. Altering data through the API may cause account instability."
%}

# ai

Used for [sequence name and description generation](https://software.farm.bot/v15/app/sequences/building-a-sequence.html#step-6-use-ai-to-write-the-sequence-name-and-description) and [Lua code generation](https://software.farm.bot/v15/app/sequences/sequence-commands/advanced#ai-lua-generation).

|Method|Description|
|---|---|
|`POST` /api/ai|Submit an auto-generation request.|

|Field|Type|`GET`|`GET/:id`|`POST`|`PATCH`|`DELETE`|
|---|---|:---:|:---:|:---:|:---:|:---:|
|`prompt`<br>Instructions for model to follow.|string|||📝|||
|`context_key`<br>Type of generation request.|"title" \| "color" \| "description" \| "lua"|||📝|||
|`sequence_id`<br>For sequence "title", "color", and "description" auto-generation requests, the ID of the sequence to summarize.|integer \| null|||📝|||

__POST /api/ai__
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

Used for [Lua code generation](https://software.farm.bot/v15/app/sequences/sequence-commands/advanced#ai-lua-generation).

|Method|Description|
|---|---|
|`POST` /api/ai_feedbacks|Submit auto-generation feedback.|

|Field|Type|`GET`|`GET/:id`|`POST`|`PATCH`|`DELETE`|
|---|---|:---:|:---:|:---:|:---:|:---:|
|`id`<br>Unique identifier set by the database.|integer||||||
|`created_at`<br>Date and time of creation set by the database.|timestamp||||||
|`updated_at`<br>Date and time of most recent update set by the database.|timestamp||||||
|`prompt`<br>A copy of the instructions for the auto-generation request.|string|||📝|||
|`reaction`<br>The feedback for the outcome of the prompt.|"good" \| "bad"|||📝|||

__POST /api/ai_feedbacks__
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

Used by the [message center](https://software.farm.bot/docs/message-center).

|Method|Description|
|---|---|
|`GET` /api/alerts|Get an array of all alerts.|
|`DELETE` /api/alerts/:id|Delete a single alert by id.|

|Field|Type|`GET`|`GET/:id`|`POST`|`PATCH`|`DELETE`|
|---|---|:---:|:---:|:---:|:---:|:---:|
|`id`<br>Unique identifier set by the database.|integer|📖||||🗑|
|`created_at`<br>Date and time of creation set by the database.|timestamp|📖||||🗑|
|`updated_at`<br>Date and time of most recent update set by the database.|timestamp|📖||||🗑|
|`problem_tag`<br>Type of alert.|"api.seed_data.missing" \| "api.documentation.unread" \| "api.tour.not_taken" \| "api.user.not_welcomed" \| "api.bulletin.unread" \| "api.demo_account.in_use"|📖||||🗑|
|`slug`<br>Defaults to random UUID.|string|📖||||🗑|
|`priority`<br>Importance for sorting.|integer|📖||||🗑|

__GET /api/alerts__
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

__DELETE /api/alerts/1__
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

|Method|Description|
|---|---|
|`GET` /api/corpus|Get the corpus object.|

|Field|Type|`GET`|`GET/:id`|`POST`|`PATCH`|`DELETE`|
|---|---|:---:|:---:|:---:|:---:|:---:|
|*corpus*<br>Celery Script corpus.|object|📖|||||

__GET /api/corpus__
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

See [curves](https://software.farm.bot/docs/curves).

|Method|Description|
|---|---|
|`GET` /api/curves|Get an array of all curves.|
|`GET` /api/curves/:id|Get a single curve by id.|
|`POST` /api/curves|Create a new curve.|
|`PATCH` /api/curves/:id|Edit a single curve by id.|
|`DELETE` /api/curves/:id|Delete a single curve by id.|

|Field|Type|`GET`|`GET/:id`|`POST`|`PATCH`|`DELETE`|
|---|---|:---:|:---:|:---:|:---:|:---:|
|`id`<br>Unique identifier set by the database.|integer|📖|📖|||🗑|
|`created_at`<br>Date and time of creation set by the database.|timestamp|📖|📖|||🗑|
|`updated_at`<br>Date and time of most recent update set by the database.|timestamp|📖|📖|||🗑|
|`name`<br>Curve name.|string|📖|📖|📝(required)|📝|🗑|
|`type`<br>Curve type.|"water" \| "spread" \| "height"|📖|📖|📝(required)|📝|🗑|
|`data`<br>Curve data.|{[day: string]: value: integer}|📖|📖|📝(required)|📝|🗑|

__POST /api/curves__
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

Used for [demo.farm.bot](http://demo.farm.bot).

|Method|Description|
|---|---|
|`POST` /api/demo_account|Create a new demo account.|

|Field|Type|`GET`|`GET/:id`|`POST`|`PATCH`|`DELETE`|
|---|---|:---:|:---:|:---:|:---:|:---:|
|`secret`<br>Password.|string|||📝|||
|`product_line`<br>FarmBot model.|"express_1.0" \| "express_1.1" \| "express_1.2" \| "express_xl_1.0" \| "express_xl_1.1" \| "express_xl_1.2" \| "genesis_1.2" \| "genesis_1.3" \| "genesis_1.4" \| "genesis_1.5" \| "genesis_1.6" \| "genesis_1.7" \| "genesis_xl_1.4" \| "genesis_xl_1.5" \| "genesis_xl_1.6" \| "genesis_xl_1.7" \| "none"|||📝|||

__POST /api/demo_account__
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

See [FarmBot settings](https://software.farm.bot/docs/farmbot-settings).

|Method|Description|
|---|---|
|`GET` /api/device|Get the device object.|
|`POST` /api/device|Create a new device.|
|`PATCH` /api/device|Edit the device object.|
|`DELETE` /api/device|Delete the device object.|

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

__GET /api/device__
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
## device/reset

|Method|Description|
|---|---|
|`POST` /api/device/reset|Reset the device.|

|Field|Type|`GET`|`GET/:id`|`POST`|`PATCH`|`DELETE`|
|---|---|:---:|:---:|:---:|:---:|:---:|
|`password`<br>Account password.|string|||📝(required)|||

## device/seed

|Method|Description|
|---|---|
|`POST` /api/device/seed|Seed the device with standard resources.|

|Field|Type|`GET`|`GET/:id`|`POST`|`PATCH`|`DELETE`|
|---|---|:---:|:---:|:---:|:---:|:---:|
|`product_line`<br>FarmBot model.|"express_1.0" \| "express_1.1" \| "express_1.2" \| "express_xl_1.0" \| "express_xl_1.1" \| "express_xl_1.2" \| "genesis_1.2" \| "genesis_1.3" \| "genesis_1.4" \| "genesis_1.5" \| "genesis_1.6" \| "genesis_1.7" \| "genesis_xl_1.4" \| "genesis_xl_1.5" \| "genesis_xl_1.6" \| "genesis_xl_1.7" \| "none"|||📝(required)|||
|`demo`<br>Seed a demo account.|boolean|||📝|||

## device/sync

|Method|Description|
|---|---|
|`GET` /api/device/sync|Get the sync object.|

# export_data

|Method|Description|
|---|---|
|`POST` /api/export_data|Request account data export.|

__POST /api/export_data__
```python
import json
import requests

# TOKEN = ...

url = f'https:{TOKEN['token']['unencoded']['iss']}/api/export_data'
headers = {'Authorization': 'Bearer ' + TOKEN['token']['encoded'],
           'content-type': 'application/json'}
response = requests.post(url, headers=headers)
print(json.dumps(response.json(), indent=2))
```
output:
```json
{
  "export_created_at": "2022-02-02T23:14:25.688+00:00",
  "server_url": "//192.168.1.112:3000",
  "database_schema": 20211206165259,
  "tools": [

  ],
  "device": {
    "id": 95,
    "created_at": "2022-02-02T23:14:25.664Z",
    "updated_at": "2022-02-02T23:14:25.664Z",
    "fb_order_number": null,
...
```

# farm_events

See [events](https://software.farm.bot/docs/events).

|Method|Description|
|---|---|
|`GET` /api/farm_events|Get an array of all farm events.|
|`GET` /api/farm_events/:id|Get a single farm event by id.|
|`POST` /api/farm_events|Create a new farm event.|
|`PATCH` /api/farm_events/:id|Edit a single farm event by id.|
|`DELETE` /api/farm_events/:id|Delete a single farm event by id.|

|Field|Type|`GET`|`GET/:id`|`POST`|`PATCH`|`DELETE`|
|---|---|:---:|:---:|:---:|:---:|:---:|
|`id`<br>Unique identifier set by the database.|integer|📖|📖|||🗑|
|`created_at`<br>Date and time of creation set by the database.|timestamp|📖|📖|||🗑|
|`updated_at`<br>Date and time of most recent update set by the database.|timestamp|📖|📖|||🗑|
|`start_time`<br>Date and time to begin the farm event.|timestamp|📖|📖|📝|📝|🗑|
|`end_time`<br>Date and time to end the farm event.|timestamp|📖|📖|📝|📝|🗑|
|`repeat`<br>Number of times to repeat the farm event.|integer|📖|📖|📝(required)|📝|🗑|
|`time_unit`<br>Time period for repeat.|"never" \| "minutely" \| "hourly" \| "daily" \| "weekly" \| "monthly" \| "yearly"|📖|📖|📝(required)|📝|🗑|
|`executable_id`<br>The ID of the sequence or regimen to execute.|integer|📖|📖|📝|📝|🗑|
|`executable_type`<br>The type of resource to execute.|"Sequence" \| "Regimen"|📖|📖|📝|📝|🗑|
|`body`<br>Variable data.|Array|📖|📖|📝|📝|🗑|

__GET /api/farm_events__
```python
import json
import requests

# TOKEN = ...

url = f'https:{TOKEN['token']['unencoded']['iss']}/api/farm_events'
headers = {'Authorization': 'Bearer ' + TOKEN['token']['encoded'],
           'content-type': 'application/json'}
response = requests.get(url, headers=headers)
print(json.dumps(response.json(), indent=2))
```
output:
```json
[
  {
    "id": 24,
    "created_at": "2022-02-02T23:14:47.297Z",
    "updated_at": "2022-02-02T23:14:47.300Z",
    "start_time": "2022-02-03T00:14:12.982Z",
    "end_time": "2022-02-03T00:15:12.982Z",
    "repeat": 1,
    "time_unit": "never",
    "executable_id": 13,
    "executable_type": "Regimen",
    "body": [
      {
        "kind": "parameter_application",
        "args": {
          "label": "variable",
          "data_value": {
            "kind": "tool",
            "args": {
              "tool_id": 235
            }
          }
        }
      }
    ]
  }
]
```
# farmware_envs

See [custom settings](https://software.farm.bot/docs/custom-settings).

|Method|Description|
|---|---|
|`GET` /api/farmware_envs|Get an array of all envs.|
|`GET` /api/farmware_envs/:id|Get a single env by id.|
|`POST` /api/farmware_envs|Create a new env.|
|`PATCH` /api/farmware_envs/:id|Edit a single env by id.|
|`DELETE` /api/farmware_envs/:id|Delete a single env by id.|
|`DELETE` /api/farmware_envs/all|Delete all envs.|

|Field|Type|`GET`|`GET/:id`|`POST`|`PATCH`|`DELETE`|
|---|---|:---:|:---:|:---:|:---:|:---:|
|`id`<br>Unique identifier set by the database.|integer|📖|📖|||🗑|
|`device_id`<br>Unique device identifier set by the database.|integer|📖|📖|||🗑|
|`created_at`<br>Date and time of creation set by the database.|timestamp|📖|📖|||🗑|
|`updated_at`<br>Date and time of most recent update set by the database.|timestamp|📖|📖|||🗑|
|`key`<br>Environment variable label.|string|📖|📖|📝(required)|📝|🗑|
|`value`<br>Environment variable value.|string|📖|📖|📝(required)|📝|🗑|

__GET /api/farmware_envs__
```python
import json
import requests

# TOKEN = ...

url = f'https:{TOKEN['token']['unencoded']['iss']}/api/farmware_envs'
headers = {'Authorization': 'Bearer ' + TOKEN['token']['encoded'],
           'content-type': 'application/json'}
response = requests.get(url, headers=headers)
print(json.dumps(response.json(), indent=2))
```
output:
```json
[
  {
    "id": 11,
    "device_id": 295,
    "key": "camera",
    "value": "USB",
    "created_at": "2022-02-02T23:14:50.641Z",
    "updated_at": "2022-02-02T23:14:50.641Z"
  }
]
```

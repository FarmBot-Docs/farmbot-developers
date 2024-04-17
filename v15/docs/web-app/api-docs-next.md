---
title: "Example API requests"
slug: "api-docs"
---

The document that follows is a list of **example API requests**. It serves as a guide for developers who wish to see the schema and existence of particular API endpoints quickly. For a list of resources, see the [quick reference table](rest-api.md#resources).

{%
include callout.html
type="info"
title="Authorization required"
content='To get the authorization token required in these examples (`TOKEN`), see [Authorization](../../python/authorization.md).'
%}

{%
include callout.html
type="warning"
title="Making requests"
content="Making requests other than GET to the API will permanently alter the data in your account. Be especially careful making DELETE requests and POST requests to singular resources, like the /device endpoint, as the API will destroy data that cannot be recovered. Altering data through the API may cause account instability."
%}

{%
include callout.html
type="success"
title="Tip"
content='If you are unsure about how data should look, create a resource in the Web App and then perform a GET request to inspect the data.'
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

# fbos_config

See [FarmBot settings](https://software.farm.bot/docs/farmbot-settings).

|Method|Description|
|---|---|
|`GET` /api/fbos_config|Get the FarmBot OS configuration object.|
|`PATCH` /api/fbos_config|Edit the FarmBot OS configuration object.|
|`DELETE` /api/fbos_config|Delete the FarmBot OS configuration object.|

|Field|Type|`GET`|`GET/:id`|`POST`|`PATCH`|`DELETE`|
|---|---|:---:|:---:|:---:|:---:|:---:|
|`id`<br>Unique identifier set by the database.|integer|📖||||🗑|
|`created_at`<br>Date and time of creation set by the database.|timestamp|📖||||🗑|
|`updated_at`<br>Date and time of most recent update set by the database.|timestamp|📖||||🗑|
|`device_id`<br>Unique device identifier set by the database.|integer|📖||||🗑|
|`disable_factory_reset`<br>Unused.|boolean|📖|||📝|🗑|
|`firmware_input_log`<br>Unused.|boolean|📖|||📝|🗑|
|`firmware_output_log`<br>Unused.|boolean|📖|||📝|🗑|
|`sequence_body_log`<br>Send a log message for each sequence step executed.|boolean|📖|||📝|🗑|
|`sequence_complete_log`<br>Send a log message upon the end of sequence execution.|boolean|📖|||📝|🗑|
|`sequence_init_log`<br>Send a log message upon the start of sequence execution.|boolean|📖|||📝|🗑|
|`network_not_found_timer`<br>Unused.|integer|📖|||📝|🗑|
|`firmware_hardware`<br>Firmware installed on the Farmduino or microcontroller.|"arduino" \| "farmduino" \| "farmduino_k14" \| "farmduino_k15" \| "farmduino_k16" \| "farmduino_k17" \| "express_k10" \| "express_k11" \| "express_k12"|📖|||📝|🗑|
|`os_auto_update`<br>Automatically download and install FarmBot OS over-the-air (OTA) updates.|boolean|📖|||📝|🗑|
|`arduino_debug_messages`<br>Unused.|boolean|📖|||📝|🗑|
|`firmware_path`<br>FarmBot OS system path to the microcontroller.|"ttyUSB0" \| "ttyACM0" \| "ttyAMA0" \| string|📖|||📝|🗑|
|`firmware_debug_log`<br>Unused.|boolean|📖|||📝|🗑|
|`update_channel`<br>FarmBot OS OTA update channel.|"stable" \| "beta" \| "alpha"|📖|||📝|🗑|
|`boot_sequence_id`<br>ID of sequence to run upon boot-up.|integer|📖|||📝|🗑|
|`safe_height`<br>Z axis coordinate (millimeters) to which the z axis should be retracted during Safe Z moves.|integer|📖|||📝|🗑|
|`soil_height`<br>Z axis coordinate (millimeters) of soil level. This value will only be used if there are no soil height measurements available.|integer|📖|||📝|🗑|
|`gantry_height`<br>The distance in millimeters between the bottom of FarmBot's tool head and the bottom of the gantry main beam when the Z-axis is fully raised.|integer|📖|||📝|🗑|

__GET /api/fbos_config__
```python
import json
import requests

# TOKEN = ...

url = f'https:{TOKEN['token']['unencoded']['iss']}/api/fbos_config'
headers = {'Authorization': 'Bearer ' + TOKEN['token']['encoded'],
           'content-type': 'application/json'}
response = requests.get(url, headers=headers)
print(json.dumps(response.json(), indent=2))
```
output:
```json
{
  "id": 43,
  "created_at": "2022-02-02T23:15:36.629Z",
  "updated_at": "2022-02-02T23:15:36.629Z",
  "device_id": 447,
  "disable_factory_reset": true,
  "firmware_input_log": false,
  "firmware_output_log": false,
  "sequence_body_log": false,
  "sequence_complete_log": false,
  "sequence_init_log": false,
  "network_not_found_timer": null,
  "firmware_hardware": null,
  "os_auto_update": true,
  "arduino_debug_messages": false,
  "firmware_path": null,
  "firmware_debug_log": false,
  "update_channel": "stable",
  "boot_sequence_id": null,
  "safe_height": 0,
  "soil_height": 0,
  "gantry_height": 0
}
```

# featured_sequences

See featured sequences [list](https://my.farm.bot/featured) and [docs](https://software.farm.bot/docs/featured-sequences).

|Method|Description|
|---|---|
|`GET` /api/featured_sequences|Get an array of all featured sequences.|

|Field|Type|`GET`|`GET/:id`|`POST`|`PATCH`|`DELETE`|
|---|---|:---:|:---:|:---:|:---:|:---:|
|`id`<br>Unique identifier set by the database.|integer|📖|||||
|`path`<br>Relative link to shared sequence page in the app.|string|📖|||||
|`name`<br>Sequence name.|string|📖|||||
|`description`<br>Sequence description.|string|📖|||||
|`color`<br>Sequence color.|string|📖|||||

__GET /api/featured_sequences__
```python
import json
import requests

# TOKEN = ...

url = f'https:{TOKEN['token']['unencoded']['iss']}/api/featured_sequences'
headers = {'Authorization': 'Bearer ' + TOKEN['token']['encoded'],
           'content-type': 'application/json'}
response = requests.get(url, headers=headers)
print(json.dumps(response.json(), indent=2))
```
output:
```json
[
  {
    "id": 15,
    "path": "/app/shared/sequence/15",
    "name": "Down-sized intangible moratorium",
    "description": "foo,bar,baz",
    "color": "red"
  }
]
```

# feedback

Used by [help](https://software.farm.bot/docs/help) and the [setup wizard](https://my.farm.bot/app/designer/setup).

|Method|Description|
|---|---|
|`POST` /api/feedback|Submit feedback.|

|Field|Type|`GET`|`GET/:id`|`POST`|`PATCH`|`DELETE`|
|---|---|:---:|:---:|:---:|:---:|:---:|
|`message`<br>Feedback content.|string|||📝|||
|`slug`<br>Source of feedback.|string|||📝|||

__POST /api/feedback__
```python
import json
import requests

# TOKEN = ...

url = f'https:{TOKEN['token']['unencoded']['iss']}/api/feedback'
headers = {'Authorization': 'Bearer ' + TOKEN['token']['encoded'],
           'content-type': 'application/json'}
payload = {
    'message': 'feedback',
    'slug': 'intro',
}
response = requests.post(url, headers=headers, json=payload)
print(json.dumps(response.json(), indent=2))
```
output:
```json
{}
```

# firmware_config

Used by [settings](https://software.farm.bot/docs/settings).

|Method|Description|
|---|---|
|`GET` /api/firmware_config|Get the firmware config object.|

|Field|Type|`GET`|`GET/:id`|`POST`|`PATCH`|`DELETE`|
|---|---|:---:|:---:|:---:|:---:|:---:|
|`id`<br>Unique identifier set by the database.|integer|📖||||🗑|
|`device_id`<br>Unique device identifier set by the database.|integer|📖||||🗑|
|`created_at`<br>Date and time of creation set by the database.|timestamp|📖||||🗑|
|`updated_at`<br>Date and time of most recent update set by the database.|timestamp|📖||||🗑|
|`encoder_enabled_x`<br>Firmware setting.|integer|📖|||📝|🗑|
|`encoder_enabled_y`<br>Firmware setting.|integer|📖|||📝|🗑|
|`encoder_enabled_z`<br>Firmware setting.|integer|📖|||📝|🗑|
|`encoder_invert_x`<br>Firmware setting.|integer|📖|||📝|🗑|
|`encoder_invert_y`<br>Firmware setting.|integer|📖|||📝|🗑|
|`encoder_invert_z`<br>Firmware setting.|integer|📖|||📝|🗑|
|`encoder_missed_steps_decay_x`<br>Firmware setting.|integer|📖|||📝|🗑|
|`encoder_missed_steps_decay_y`<br>Firmware setting.|integer|📖|||📝|🗑|
|`encoder_missed_steps_decay_z`<br>Firmware setting.|integer|📖|||📝|🗑|
|`encoder_missed_steps_max_x`<br>Firmware setting.|integer|📖|||📝|🗑|
|`encoder_missed_steps_max_y`<br>Firmware setting.|integer|📖|||📝|🗑|
|`encoder_missed_steps_max_z`<br>Firmware setting.|integer|📖|||📝|🗑|
|`encoder_scaling_x`<br>Firmware setting.|integer|📖|||📝|🗑|
|`encoder_scaling_y`<br>Firmware setting.|integer|📖|||📝|🗑|
|`encoder_scaling_z`<br>Firmware setting.|integer|📖|||📝|🗑|
|`encoder_type_x`<br>Firmware setting.|integer|📖|||📝|🗑|
|`encoder_type_y`<br>Firmware setting.|integer|📖|||📝|🗑|
|`encoder_type_z`<br>Firmware setting.|integer|📖|||📝|🗑|
|`encoder_use_for_pos_x`<br>Firmware setting.|integer|📖|||📝|🗑|
|`encoder_use_for_pos_y`<br>Firmware setting.|integer|📖|||📝|🗑|
|`encoder_use_for_pos_z`<br>Firmware setting.|integer|📖|||📝|🗑|
|`movement_axis_nr_steps_x`<br>Firmware setting.|integer|📖|||📝|🗑|
|`movement_axis_nr_steps_y`<br>Firmware setting.|integer|📖|||📝|🗑|
|`movement_axis_nr_steps_z`<br>Firmware setting.|integer|📖|||📝|🗑|
|`movement_enable_endpoints_x`<br>Firmware setting.|integer|📖|||📝|🗑|
|`movement_enable_endpoints_y`<br>Firmware setting.|integer|📖|||📝|🗑|
|`movement_enable_endpoints_z`<br>Firmware setting.|integer|📖|||📝|🗑|
|`movement_home_at_boot_x`<br>Firmware setting.|integer|📖|||📝|🗑|
|`movement_home_at_boot_y`<br>Firmware setting.|integer|📖|||📝|🗑|
|`movement_home_at_boot_z`<br>Firmware setting.|integer|📖|||📝|🗑|
|`movement_home_spd_x`<br>Firmware setting.|integer|📖|||📝|🗑|
|`movement_home_spd_y`<br>Firmware setting.|integer|📖|||📝|🗑|
|`movement_home_spd_z`<br>Firmware setting.|integer|📖|||📝|🗑|
|`movement_home_up_x`<br>Firmware setting.|integer|📖|||📝|🗑|
|`movement_home_up_y`<br>Firmware setting.|integer|📖|||📝|🗑|
|`movement_home_up_z`<br>Firmware setting.|integer|📖|||📝|🗑|
|`movement_invert_endpoints_x`<br>Firmware setting.|integer|📖|||📝|🗑|
|`movement_invert_endpoints_y`<br>Firmware setting.|integer|📖|||📝|🗑|
|`movement_invert_endpoints_z`<br>Firmware setting.|integer|📖|||📝|🗑|
|`movement_invert_motor_x`<br>Firmware setting.|integer|📖|||📝|🗑|
|`movement_invert_motor_y`<br>Firmware setting.|integer|📖|||📝|🗑|
|`movement_invert_motor_z`<br>Firmware setting.|integer|📖|||📝|🗑|
|`movement_keep_active_x`<br>Firmware setting.|integer|📖|||📝|🗑|
|`movement_keep_active_y`<br>Firmware setting.|integer|📖|||📝|🗑|
|`movement_keep_active_z`<br>Firmware setting.|integer|📖|||📝|🗑|
|`movement_max_spd_x`<br>Firmware setting.|integer|📖|||📝|🗑|
|`movement_max_spd_y`<br>Firmware setting.|integer|📖|||📝|🗑|
|`movement_max_spd_z`<br>Firmware setting.|integer|📖|||📝|🗑|
|`movement_min_spd_x`<br>Firmware setting.|integer|📖|||📝|🗑|
|`movement_min_spd_y`<br>Firmware setting.|integer|📖|||📝|🗑|
|`movement_min_spd_z`<br>Firmware setting.|integer|📖|||📝|🗑|
|`movement_secondary_motor_invert_x`<br>Firmware setting.|integer|📖|||📝|🗑|
|`movement_secondary_motor_x`<br>Firmware setting.|integer|📖|||📝|🗑|
|`movement_step_per_mm_x`<br>Firmware setting.|integer|📖|||📝|🗑|
|`movement_step_per_mm_y`<br>Firmware setting.|integer|📖|||📝|🗑|
|`movement_step_per_mm_z`<br>Firmware setting.|integer|📖|||📝|🗑|
|`movement_steps_acc_dec_x`<br>Firmware setting.|integer|📖|||📝|🗑|
|`movement_steps_acc_dec_y`<br>Firmware setting.|integer|📖|||📝|🗑|
|`movement_steps_acc_dec_z`<br>Firmware setting.|integer|📖|||📝|🗑|
|`movement_stop_at_home_x`<br>Firmware setting.|integer|📖|||📝|🗑|
|`movement_stop_at_home_y`<br>Firmware setting.|integer|📖|||📝|🗑|
|`movement_stop_at_home_z`<br>Firmware setting.|integer|📖|||📝|🗑|
|`movement_stop_at_max_x`<br>Firmware setting.|integer|📖|||📝|🗑|
|`movement_stop_at_max_y`<br>Firmware setting.|integer|📖|||📝|🗑|
|`movement_stop_at_max_z`<br>Firmware setting.|integer|📖|||📝|🗑|
|`movement_timeout_x`<br>Firmware setting.|integer|📖|||📝|🗑|
|`movement_timeout_y`<br>Firmware setting.|integer|📖|||📝|🗑|
|`movement_timeout_z`<br>Firmware setting.|integer|📖|||📝|🗑|
|`param_config_ok`<br>Firmware setting.|integer|📖|||📝|🗑|
|`param_e_stop_on_mov_err`<br>Firmware setting.|integer|📖|||📝|🗑|
|`param_mov_nr_retry`<br>Firmware setting.|integer|📖|||📝|🗑|
|`param_test`<br>Firmware setting.|integer|📖|||📝|🗑|
|`param_use_eeprom`<br>Firmware setting.|integer|📖|||📝|🗑|
|`param_version`<br>Firmware setting.|integer|📖|||📝|🗑|
|`pin_guard_1_active_state`<br>Firmware setting.|integer|📖|||📝|🗑|
|`pin_guard_1_pin_nr`<br>Firmware setting.|integer|📖|||📝|🗑|
|`pin_guard_1_time_out`<br>Firmware setting.|integer|📖|||📝|🗑|
|`pin_guard_2_active_state`<br>Firmware setting.|integer|📖|||📝|🗑|
|`pin_guard_2_pin_nr`<br>Firmware setting.|integer|📖|||📝|🗑|
|`pin_guard_2_time_out`<br>Firmware setting.|integer|📖|||📝|🗑|
|`pin_guard_3_active_state`<br>Firmware setting.|integer|📖|||📝|🗑|
|`pin_guard_3_pin_nr`<br>Firmware setting.|integer|📖|||📝|🗑|
|`pin_guard_3_time_out`<br>Firmware setting.|integer|📖|||📝|🗑|
|`pin_guard_4_active_state`<br>Firmware setting.|integer|📖|||📝|🗑|
|`pin_guard_4_pin_nr`<br>Firmware setting.|integer|📖|||📝|🗑|
|`pin_guard_4_time_out`<br>Firmware setting.|integer|📖|||📝|🗑|
|`pin_guard_5_active_state`<br>Firmware setting.|integer|📖|||📝|🗑|
|`pin_guard_5_pin_nr`<br>Firmware setting.|integer|📖|||📝|🗑|
|`pin_guard_5_time_out`<br>Firmware setting.|integer|📖|||📝|🗑|
|`movement_invert_2_endpoints_x`<br>Firmware setting.|integer|📖|||📝|🗑|
|`movement_invert_2_endpoints_y`<br>Firmware setting.|integer|📖|||📝|🗑|
|`movement_invert_2_endpoints_z`<br>Firmware setting.|integer|📖|||📝|🗑|
|`movement_microsteps_x`<br>Firmware setting.|integer|📖|||📝|🗑|
|`movement_microsteps_y`<br>Firmware setting.|integer|📖|||📝|🗑|
|`movement_microsteps_z`<br>Firmware setting.|integer|📖|||📝|🗑|
|`movement_motor_current_x`<br>Firmware setting.|integer|📖|||📝|🗑|
|`movement_motor_current_y`<br>Firmware setting.|integer|📖|||📝|🗑|
|`movement_motor_current_z`<br>Firmware setting.|integer|📖|||📝|🗑|
|`movement_stall_sensitivity_x`<br>Firmware setting.|integer|📖|||📝|🗑|
|`movement_stall_sensitivity_y`<br>Firmware setting.|integer|📖|||📝|🗑|
|`movement_stall_sensitivity_z`<br>Firmware setting.|integer|📖|||📝|🗑|
|`movement_min_spd_z2`<br>Firmware setting.|integer|📖|||📝|🗑|
|`movement_max_spd_z2`<br>Firmware setting.|integer|📖|||📝|🗑|
|`movement_steps_acc_dec_z2`<br>Firmware setting.|integer|📖|||📝|🗑|
|`movement_calibration_retry_x`<br>Firmware setting.|integer|📖|||📝|🗑|
|`movement_calibration_retry_y`<br>Firmware setting.|integer|📖|||📝|🗑|
|`movement_calibration_retry_z`<br>Firmware setting.|integer|📖|||📝|🗑|
|`movement_calibration_deadzone_x`<br>Firmware setting.|integer|📖|||📝|🗑|
|`movement_calibration_deadzone_y`<br>Firmware setting.|integer|📖|||📝|🗑|
|`movement_calibration_deadzone_z`<br>Firmware setting.|integer|📖|||📝|🗑|
|`movement_axis_stealth_x`<br>Firmware setting.|integer|📖|||📝|🗑|
|`movement_axis_stealth_y`<br>Firmware setting.|integer|📖|||📝|🗑|
|`movement_axis_stealth_z`<br>Firmware setting.|integer|📖|||📝|🗑|
|`movement_calibration_retry_total_x`<br>Firmware setting.|integer|📖|||📝|🗑|
|`movement_calibration_retry_total_y`<br>Firmware setting.|integer|📖|||📝|🗑|
|`movement_calibration_retry_total_z`<br>Firmware setting.|integer|📖|||📝|🗑|
|`pin_report_1_pin_nr`<br>Firmware setting.|integer|📖|||📝|🗑|
|`pin_report_2_pin_nr`<br>Firmware setting.|integer|📖|||📝|🗑|

__GET /api/firmware_config__
```python
import json
import requests

# TOKEN = ...

url = f'https:{TOKEN['token']['unencoded']['iss']}/api/firmware_config'
headers = {'Authorization': 'Bearer ' + TOKEN['token']['encoded'],
           'content-type': 'application/json'}
response = requests.get(url, headers=headers)
print(json.dumps(response.json(), indent=2))
```
output:
```json
{
  "id": 7,
  "created_at": "2022-02-02T23:14:50.199Z",
  "updated_at": "2022-02-02T23:14:50.199Z",
  "device_id": 287,
  "encoder_enabled_x": 1,
  "encoder_enabled_y": 1,
  "encoder_enabled_z": 1,
  "encoder_invert_x": 0,
  "encoder_invert_y": 0,
  "encoder_invert_z": 0,
  "encoder_missed_steps_decay_x": 5,
  "encoder_missed_steps_decay_y": 5,
  "encoder_missed_steps_decay_z": 5,
  "encoder_missed_steps_max_x": 5,
  "encoder_missed_steps_max_y": 5,
  "encoder_missed_steps_max_z": 5,
  "encoder_scaling_x": 5556,
  "encoder_scaling_y": 5556,
  "encoder_scaling_z": 5556,
  "encoder_type_x": 0,
  "encoder_type_y": 0,
  "encoder_type_z": 0,
  "encoder_use_for_pos_x": 0,
  "encoder_use_for_pos_y": 0,
  "encoder_use_for_pos_z": 0,
  "movement_axis_nr_steps_x": 0,
  "movement_axis_nr_steps_y": 0,
  "movement_axis_nr_steps_z": 0,
  "movement_enable_endpoints_x": 0,
  "movement_enable_endpoints_y": 0,
  "movement_enable_endpoints_z": 0,
  "movement_home_at_boot_x": 0,
  "movement_home_at_boot_y": 0,
  "movement_home_at_boot_z": 0,
  "movement_home_spd_x": 400,
  "movement_home_spd_y": 400,
  "movement_home_spd_z": 400,
  "movement_home_up_x": 0,
  "movement_home_up_y": 0,
  "movement_home_up_z": 1,
  "movement_invert_endpoints_x": 0,
  "movement_invert_endpoints_y": 0,
  "movement_invert_endpoints_z": 0,
  "movement_invert_motor_x": 0,
  "movement_invert_motor_y": 0,
  "movement_invert_motor_z": 0,
  "movement_keep_active_x": 0,
  "movement_keep_active_y": 0,
  "movement_keep_active_z": 1,
  "movement_max_spd_x": 400,
  "movement_max_spd_y": 400,
  "movement_max_spd_z": 400,
  "movement_min_spd_x": 50,
  "movement_min_spd_y": 50,
  "movement_min_spd_z": 50,
  "movement_secondary_motor_invert_x": 1,
  "movement_secondary_motor_x": 1,
  "movement_step_per_mm_x": 5.0,
  "movement_step_per_mm_y": 5.0,
  "movement_step_per_mm_z": 25.0,
  "movement_steps_acc_dec_x": 300,
  "movement_steps_acc_dec_y": 300,
  "movement_steps_acc_dec_z": 300,
  "movement_stop_at_home_x": 1,
  "movement_stop_at_home_y": 1,
  "movement_stop_at_home_z": 1,
  "movement_stop_at_max_x": 1,
  "movement_stop_at_max_y": 1,
  "movement_stop_at_max_z": 1,
  "movement_timeout_x": 180,
  "movement_timeout_y": 180,
  "movement_timeout_z": 180,
  "param_config_ok": 0,
  "param_e_stop_on_mov_err": 0,
  "param_mov_nr_retry": 3,
  "param_test": 0,
  "param_use_eeprom": 1,
  "param_version": 1,
  "pin_guard_1_active_state": 1,
  "pin_guard_1_pin_nr": 0,
  "pin_guard_1_time_out": 60,
  "pin_guard_2_active_state": 1,
  "pin_guard_2_pin_nr": 0,
  "pin_guard_2_time_out": 60,
  "pin_guard_3_active_state": 1,
  "pin_guard_3_pin_nr": 0,
  "pin_guard_3_time_out": 60,
  "pin_guard_4_active_state": 1,
  "pin_guard_4_pin_nr": 0,
  "pin_guard_4_time_out": 60,
  "pin_guard_5_active_state": 1,
  "pin_guard_5_pin_nr": 0,
  "pin_guard_5_time_out": 60,
  "movement_invert_2_endpoints_x": 0,
  "movement_invert_2_endpoints_y": 0,
  "movement_invert_2_endpoints_z": 0,
  "movement_microsteps_x": 1,
  "movement_microsteps_y": 1,
  "movement_microsteps_z": 1,
  "movement_motor_current_x": 1823,
  "movement_motor_current_y": 1823,
  "movement_motor_current_z": 1823,
  "movement_stall_sensitivity_x": 63,
  "movement_stall_sensitivity_y": 63,
  "movement_stall_sensitivity_z": 63,
  "movement_min_spd_z2": 50,
  "movement_max_spd_z2": 400,
  "movement_steps_acc_dec_z2": 300,
  "movement_calibration_retry_x": 1,
  "movement_calibration_retry_y": 1,
  "movement_calibration_retry_z": 1,
  "movement_calibration_deadzone_x": 50,
  "movement_calibration_deadzone_y": 50,
  "movement_calibration_deadzone_z": 250,
  "movement_axis_stealth_x": 1,
  "movement_axis_stealth_y": 1,
  "movement_axis_stealth_z": 1,
  "movement_calibration_retry_total_x": 10,
  "movement_calibration_retry_total_y": 10,
  "movement_calibration_retry_total_z": 10,
  "pin_report_1_pin_nr": 0,
  "pin_report_2_pin_nr": 0
}
```

# folders

Used by [sequences](https://software.farm.bot/docs/sequences).

|Method|Description|
|---|---|
|`GET` /api/folders|Get an array of all folders.|
|`GET` /api/folders/:id|Get a single folder by id.|
|`POST` /api/folders|Create a new folder.|
|`PATCH` /api/folders/:id|Edit a single folder by id.|
|`DELETE` /api/folders/:id|Delete a single folder by id.|

|Field|Type|`GET`|`GET/:id`|`POST`|`PATCH`|`DELETE`|
|---|---|:---:|:---:|:---:|:---:|:---:|
|`id`<br>Unique identifier set by the database.|integer|📖|📖|||🗑|
|`created_at`<br>Date and time of creation set by the database.|timestamp|📖|📖|||🗑|
|`updated_at`<br>Date and time of most recent update set by the database.|timestamp|📖|📖|||🗑|
|`parent_id`<br>ID of the parent folder, if any.|integer \| null|📖|📖|📝|📝(required)|🗑|
|`name`<br>Folder name.|string|📖|📖|📝(required)|📝|🗑|
|`color`<br>Folder color.|string|📖|📖|📝(required)|📝|🗑|

__GET /api/folders__
```python
import json
import requests

# TOKEN = ...

url = f'https:{TOKEN['token']['unencoded']['iss']}/api/folders'
headers = {'Authorization': 'Bearer ' + TOKEN['token']['encoded'],
           'content-type': 'application/json'}
response = requests.get(url, headers=headers)
print(json.dumps(response.json(), indent=2))
```
output:
```json
[
  {
    "id": 18,
    "created_at": "2022-02-02T23:15:35.665Z",
    "updated_at": "2022-02-02T23:15:35.665Z",
    "parent_id": null,
    "color": "red",
    "name": "parent"
  }
]
```

# global_bulletins

Used by the [message center](https://software.farm.bot/docs/message-center). To create a bulletin, see [posting to the message center](server-admin.md#posting-to-the-message-center).

|Method|Description|
|---|---|
|`GET` /api/global_bulletins/:slug|Get a single bulletin by slug.|

|Field|Type|`GET`|`GET/:slug`|`POST`|`PATCH`|`DELETE`|
|---|---|:---:|:---:|:---:|:---:|:---:|
|`id`<br>Unique identifier set by the database.|integer||📖||||
|`created_at`<br>Date and time of creation set by the database.|timestamp||📖||||
|`updated_at`<br>Date and time of most recent update set by the database.|timestamp||📖||||
|`href`<br>Link.|string||📖||||
|`href_label`<br>Label for link button.|string||📖||||
|`slug`<br>UUID.|string||📖||||
|`title`<br>Bulletin title.|string||📖||||
|`type`<br>Bulletin type.|"info" \| "success" \| "warn"||📖||||
|`content`<br>Bulletin content.|string||📖||||

__GET /api/global_bulletins/:slug__
```python
import json
import requests

# TOKEN = ...

url = f'https:{TOKEN['token']['unencoded']['iss']}/api/global_bulletins/Okra'
headers = {'Authorization': 'Bearer ' + TOKEN['token']['encoded'],
           'content-type': 'application/json'}
response = requests.get(url, headers=headers)
print(json.dumps(response.json(), indent=2))
```
output:
```json
{
  "id": 1,
  "created_at": "2022-02-02T23:15:35.750Z",
  "updated_at": "2022-02-02T23:15:35.750Z",
  "href": "https://farm.bot/blogs/news/pre-order-farmbot-genesis-xl-v1-5",
  "href_label": "Click here!",
  "slug": "Okra",
  "title": null,
  "type": "info",
  "content": "we're now accepting pre-orders for Genesis XL v1.5!"
}
```

# global_config

|Method|Description|
|---|---|
|`GET` /api/global_config|Get the global config object.|

|Field|Type|`GET`|`GET/:id`|`POST`|`PATCH`|`DELETE`|
|---|---|:---:|:---:|:---:|:---:|:---:|
|`FBOS_END_OF_LIFE_VERSION`<br>FarmBot OS version to give end-of-life warning.|string|📖|||||
|`MINIMUM_FBOS_VERSION`<br>Oldest FarmBot OS version allowed to connect.|string|📖|||||
|`TOS_URL`<br>Terms of service URL.|string|📖|||||
|`PRIV_URL`<br>Privacy policy URL.|string|📖|||||
|`NODE_ENV`<br>Node environment.|"development" \| "production" \| "test"|📖|||||
|`LONG_REVISION`<br>Hash of the current Web App GitHub commit.|string|📖|||||
|`SHORT_REVISION`<br>First 8 characters of the current Web App GitHub commit hash.|string|📖|||||
|`MQTT_WS`<br>MQTT websocket URL.|string|📖|||||
|*any*<br>Any config set by the server.|string|📖|||||

__GET /api/global_config__
```python
import json
import requests

# TOKEN = ...

url = f'https:{TOKEN['token']['unencoded']['iss']}/api/global_config'
headers = {'Authorization': 'Bearer ' + TOKEN['token']['encoded'],
           'content-type': 'application/json'}
response = requests.get(url, headers=headers)
print(json.dumps(response.json(), indent=2))
```
output:
```json
{
  "FBOS_END_OF_LIFE_VERSION": "14.6.0",
  "MINIMUM_FBOS_VERSION": "14.6.0",
  "TOS_URL": "",
  "PRIV_URL": "",
  "NODE_ENV": "production",
  "LONG_REVISION": "c4d419354435be1938a45294666ff8eb5bc61b27",
  "SHORT_REVISION": "c4d41935",
  "MQTT_WS": "wss://abc-def.rmq.cloudamqp.com:443/ws/mqtt",
  "SOME_OTHER_CONFIG": "value"
}
```

# images

Used for [photos](https://software.farm.bot/docs/photos).

|Method|Description|
|---|---|
|`GET` /api/images|Get an array of all images.|
|`GET` /api/images/:id|Get a single image by id.|
|`POST` /api/images|Create a new image.|
|`DELETE` /api/images/:id|Delete a single image by id.|

|Field|Type|`GET`|`GET/:id`|`POST`|`PATCH`|`DELETE`|
|---|---|:---:|:---:|:---:|:---:|:---:|
|`id`<br>Unique identifier set by the database.|integer|📖|📖|||🗑|
|`device_id`<br>Unique device identifier set by the database.|integer|📖|📖|||🗑|
|`created_at`<br>Date and time of creation set by the database.|timestamp|📖|📖|||🗑|
|`updated_at`<br>Date and time of most recent update set by the database.|timestamp|📖|📖|||🗑|
|`attachment_processed_at`<br>Date and time when image was processed.|timestamp|📖|📖|📝||🗑|
|`attachment_url`<br>Image URL.|string|📖|📖|📝(required)||🗑|
|`meta`<br>Image info.|{name: string, x: float, y: float, z: float}|📖|📖|📝||🗑|

__GET /api/images__
```python
import json
import requests

# TOKEN = ...

url = f'https:{TOKEN['token']['unencoded']['iss']}/api/images'
headers = {'Authorization': 'Bearer ' + TOKEN['token']['encoded'],
           'content-type': 'application/json'}
response = requests.get(url, headers=headers)
print(json.dumps(response.json(), indent=2))
```
output:
```json
[
  {
    "id": 10,
    "created_at": "2022-02-02T23:15:48.541Z",
    "updated_at": "2022-02-02T23:15:48.541Z",
    "device_id": 570,
    "attachment_processed_at": null,
    "attachment_url": "http://192.168.1.112:3000/placeholder_farmbot.jpg?text=Processing...",
    "meta": {
      "x": 1,
      "y": 2,
      "z": 3
    }
  }
]
```

# logs

Used for [logs](https://software.farm.bot/docs/jobs-and-logs).

|Method|Description|
|---|---|
|`GET` /api/logs|Get an array of all logs.|
|`POST` /api/logs|Create a new log.|
|`DELETE` /api/logs/:id|Delete a single log by id.|
|`DELETE` /api/logs/all|Delete all logs.|

|Field|Type|`GET`|`GET/:id`|`POST`|`PATCH`|`DELETE`|
|---|---|:---:|:---:|:---:|:---:|:---:|
|`id`<br>Unique identifier set by the database.|integer|📖||||🗑|
|`created_at`<br>Date and time of creation set by the database.|timestamp|📖||||🗑|
|`updated_at`<br>Date and time of most recent update set by the database.|timestamp|📖||||🗑|
|`channels`<br>Array of transmission channels.|("ticker" \| "toast" \| "email" \| "espeak")[]|📖||📝||🗑|
|`message`<br>Log message.|string|📖||📝(required)||🗑|
|`meta`<br>Unused.|null|📖||📝||🗑|
|`major_version`<br>FarmBot OS major version.|string|📖||📝||🗑|
|`minor_version`<br>FarmBot OS minor version.|string|📖||📝||🗑|
|`patch_version`<br>FarmBot OS patch version.|string|📖||📝||🗑|
|`type`<br>Log type.|"assertion" \| "busy" \| "debug" \| "error" \| "fun" \| "info" \| "success" \| "warn"|📖||📝||🗑|
|`verbosity`<br>Log level.|0-3|📖||📝||🗑|
|`x`<br>x coordinate at time of log.|float|📖||📝||🗑|
|`y`<br>y coordinate at time of log.|float|📖||📝||🗑|
|`z`<br>z coordinate at time of log.|float|📖||📝||🗑|

__GET /api/logs__
```python
import json
import requests

# TOKEN = ...

url = f'https:{TOKEN['token']['unencoded']['iss']}/api/logs'
headers = {'Authorization': 'Bearer ' + TOKEN['token']['encoded'],
           'content-type': 'application/json'}
response = requests.get(url, headers=headers)
print(json.dumps(response.json(), indent=2))
```
output:
```json
[
  {
    "id": 13,
    "created_at": 1643843034,
    "updated_at": "2022-02-02T23:14:54.423Z",
    "channels": [
      "toast"
    ],
    "message": "extend global convergence",
    "meta": null,
    "major_version": null,
    "minor_version": null,
    "patch_version": null,
    "type": "success",
    "verbosity": 1,
    "x": -458.0,
    "y": -12.0,
    "z": 765.0
  }
]
```

## logs/search

|Method|Description|
|---|---|
|`GET` /api/logs/search|Get a list of filtered logs.|

|Field|Type|`GET`|`GET/:id`|`POST`|`PATCH`|`DELETE`|
|---|---|:---:|:---:|:---:|:---:|:---:|
|`message`<br>Log message.|string|📝|||||
|`type`<br>Log type.|"assertion" \| "busy" \| "debug" \| "error" \| "fun" \| "info" \| "success" \| "warn"|📝|||||
|`verbosity`<br>Log level.|0-3|📝|||||
|`x`<br>x coordinate at time of log.|float|📝|||||
|`y`<br>y coordinate at time of log.|float|📝|||||
|`z`<br>z coordinate at time of log.|float|📝|||||

# password_resets

## request

|Method|Description|
|---|---|
|`POST` /api/password_resets|Request a password reset.|

|Field|Type|`GET`|`GET/:id`|`POST`|`PATCH`|`DELETE`|
|---|---|:---:|:---:|:---:|:---:|:---:|
|`email`<br>Account email address.|string|||📝(required)|||

## change

|Method|Description|
|---|---|
|`PATCH` /api/password_resets|Change the account password.|

|Field|Type|`GET`|`GET/:id`|`POST`|`PATCH`|`DELETE`|
|---|---|:---:|:---:|:---:|:---:|:---:|
|`password`<br>New account password.|string||||📝(required)||
|`password_confirmation`<br>New account password.|string||||📝(required)||
|`id`<br>Token.|string||||📝(required)||

# peripherals

Used by [peripherals](https://software.farm.bot/docs/peripherals).

|Method|Description|
|---|---|
|`GET` /api/peripherals|Get an array of all peripherals.|
|`GET` /api/peripherals/:id|Get a single peripheral by id.|
|`POST` /api/peripherals|Create a new peripheral.|
|`PATCH` /api/peripherals/:id|Edit a single peripheral by id.|
|`DELETE` /api/peripherals/:id|Delete a single peripheral by id.|

|Field|Type|`GET`|`GET/:id`|`POST`|`PATCH`|`DELETE`|
|---|---|:---:|:---:|:---:|:---:|:---:|
|`id`<br>Unique identifier set by the database.|integer|📖|📖|||🗑|
|`created_at`<br>Date and time of creation set by the database.|timestamp|📖|📖|||🗑|
|`updated_at`<br>Date and time of most recent update set by the database.|timestamp|📖|📖|||🗑|
|`pin`<br>Pin number.|integer|📖|📖|📝(required)|📝|🗑|
|`label`<br>Peripheral name.|string|📖|📖|📝(required)|📝|🗑|
|`mode`<br>Pin mode.|0-1|📖|📖||📝|🗑|

__GET /api/peripherals__
```python
import json
import requests

# TOKEN = ...

url = f'https:{TOKEN['token']['unencoded']['iss']}/api/peripherals'
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
    "created_at": "2022-02-02T23:14:14.106Z",
    "updated_at": "2022-02-02T23:14:14.106Z",
    "pin": 1,
    "label": "MyString",
    "mode": 0
  },
  {
    "id": 2,
    "created_at": "2022-02-02T23:14:14.118Z",
    "updated_at": "2022-02-02T23:14:14.118Z",
    "pin": 2,
    "label": "MyString",
    "mode": 0
  }
]
```

# pin_bindings

Used by [push buttons](https://software.farm.bot/docs/peripherals).

|Method|Description|
|---|---|
|`GET` /api/pin_bindings|Get an array of all pin bindings.|
|`GET` /api/pin_bindings/:id|Get a single pin binding by id.|
|`POST` /api/pin_bindings|Create a new pin binding.|
|`PATCH` /api/pin_bindings/:id|Edit a single pin binding by id.|
|`DELETE` /api/pin_bindings/:id|Delete a single pin binding by id.|

|Field|Type|`GET`|`GET/:id`|`POST`|`PATCH`|`DELETE`|
|---|---|:---:|:---:|:---:|:---:|:---:|
|`id`<br>Unique identifier set by the database.|integer|📖|📖|||🗑|
|`device_id`<br>Unique device identifier set by the database.|integer|📖|📖|||🗑|
|`created_at`<br>Date and time of creation set by the database.|timestamp|📖|📖|||🗑|
|`updated_at`<br>Date and time of most recent update set by the database.|timestamp|📖|📖|||🗑|
|`sequence_id`<br>ID of sequence to execute.|integer \| null|📖|📖|📝|📝|🗑|
|`special_action`<br>Action to perform.|"emergency_lock" \| "emergency_unlock" \| "power_off" \| "read_status" \| "reboot" \| "sync" \| "take_photo" \| null|📖|📖|📝|📝|🗑|
|`pin_num`<br>Button pin number.|integer|📖|📖|📝(required)|📝|🗑|
|`binding_type`<br>"standard": execute a sequence, "special": perform an action.|"standard" \| "special"|📖|📖||||

__GET /api/pin_bindings__
```python
import json
import requests

# TOKEN = ...

url = f'https:{TOKEN['token']['unencoded']['iss']}/api/pin_bindings'
headers = {'Authorization': 'Bearer ' + TOKEN['token']['encoded'],
           'content-type': 'application/json'}
response = requests.get(url, headers=headers)
print(json.dumps(response.json(), indent=2))
```
output:
```json
[
  {
    "id": 46,
    "created_at": "2022-02-02T23:15:50.154Z",
    "updated_at": "2022-02-02T23:15:50.154Z",
    "device_id": 589,
    "sequence_id": 1,
    "special_action": null,
    "pin_num": 16,
    "binding_type": "standard"
  },
  {
    "id": 47,
    "created_at": "2022-02-02T23:15:50.169Z",
    "updated_at": "2022-02-02T23:15:50.169Z",
    "device_id": 589,
    "sequence_id": null,
    "special_action": "sync",
    "pin_num": 1,
    "binding_type": "special"
  }
]
```

# plant_templates

Used by [gardens](https://software.farm.bot/docs/gardens).

|Method|Description|
|---|---|
|`GET` /api/plant_templates|Get an array of all plant templates.|
|`POST` /api/plant_templates|Create a new plant template.|
|`PATCH` /api/plant_templates/:id|Edit a single plant template by id.|
|`DELETE` /api/plant_templates/:id|Delete a single plant template by id.|

|Field|Type|`GET`|`GET/:id`|`POST`|`PATCH`|`DELETE`|
|---|---|:---:|:---:|:---:|:---:|:---:|
|`id`<br>Unique identifier set by the database.|integer|📖|📖|||🗑|
|`device_id`<br>Unique device identifier set by the database.|integer|📖|📖|||🗑|
|`created_at`<br>Date and time of creation set by the database.|timestamp|📖|📖|||🗑|
|`updated_at`<br>Date and time of most recent update set by the database.|timestamp|📖|📖|||🗑|
|`saved_garden_id`<br>ID of the saved garden to which the plant belongs.|integer|📖||📝(required)|📝|🗑|
|`radius`<br>Size of the plant.|float|📖||📝|📝|🗑|
|`x`<br>x coordinate.|float|📖||📝(required)|📝|🗑|
|`y`<br>y coordinate.|float|📖||📝(required)|📝|🗑|
|`z`<br>z coordinate.|float|📖||📝|📝|🗑|
|`name`<br>Plant name.|string|📖||📝|📝|🗑|
|`openfarm_slug`<br>Plant type (from OpenFarm).|string|📖||📝|📝|🗑|

__GET /api/plant_templates__
```python
import json
import requests

# TOKEN = ...

url = f'https:{TOKEN['token']['unencoded']['iss']}/api/plant_templates'
headers = {'Authorization': 'Bearer ' + TOKEN['token']['encoded'],
           'content-type': 'application/json'}
response = requests.get(url, headers=headers)
print(json.dumps(response.json(), indent=2))
```
output:
```json
[
  {
    "id": 7,
    "saved_garden_id": 7,
    "device_id": 160,
    "radius": 1.5,
    "x": 206.0,
    "y": 426.0,
    "z": 23.0,
    "name": "untitled",
    "openfarm_slug": "lettuce",
    "created_at": "2022-02-02T23:14:34.382Z",
    "updated_at": "2022-02-02T23:14:34.382Z"
  }
]
```

# point_groups

Used by [groups](https://software.farm.bot/docs/groups).

|Method|Description|
|---|---|
|`GET` /api/point_groups|Get an array of all point groups.|
|`GET` /api/point_groups/:id|Get a single point group by id.|
|`POST` /api/point_groups|Create a new point group.|
|`PATCH` /api/point_groups/:id|Edit a single point group by id.|
|`DELETE` /api/point_groups/:id|Delete a single point group by id.|

|Field|Type|`GET`|`GET/:id`|`POST`|`PATCH`|`DELETE`|
|---|---|:---:|:---:|:---:|:---:|:---:|
|`id`<br>Unique identifier set by the database.|integer|📖|📖|||🗑|
|`created_at`<br>Date and time of creation set by the database.|timestamp|📖|📖|||🗑|
|`updated_at`<br>Date and time of most recent update set by the database.|timestamp|📖|📖|||🗑|
|`name`<br>Group name.|string|📖|📖|📝(required)|📝|🗑|
|`point_ids`<br>Array of manually included point IDs.|integer[]|📖|📖|📝(required)|📝|🗑|
|`sort_type`<br>Sort type. See [point group sorting](../../other/how-it-works/point-group-sorting.md).|"xy_ascending" \| "xy_descending" \| "yx_ascending" \| "yx_descending" \| "xy_alternating" \| "yx_alternating" \| "nn" \| "random"|📖|📖|📝|📝|🗑|
|`criteria`<br>Point group criteria for automatic point inclusion.|See below and [groups](https://software.farm.bot/docs/groups).|📖|📖|📝|📝|🗑|

__GET /api/point_groups__
```python
import json
import requests

# TOKEN = ...

url = f'https:{TOKEN['token']['unencoded']['iss']}/api/point_groups'
headers = {'Authorization': 'Bearer ' + TOKEN['token']['encoded'],
           'content-type': 'application/json'}
response = requests.get(url, headers=headers)
print(json.dumps(response.json(), indent=2))
```
output:
```json
[
  {
    "id": 15,
    "created_at": "2022-02-02T23:14:32.520Z",
    "updated_at": "2022-02-02T23:14:32.520Z",
    "name": "PG test 0",
    "point_ids": [
      76,
      77,
      78
    ],
    "sort_type": "xy_ascending",
    "criteria": {
      "day": {
        "op": "<",
        "days_ago": 0
      },
      "string_eq": {
        "openfarm_slug": [
          "carrot"
        ]
      },
      "number_eq": {
        "z": [
          24,
          25,
          26
        ]
      },
      "number_lt": {
        "x": 4,
        "y": 4
      },
      "number_gt": {
        "x": 1,
        "y": 1
      }
    }
  }
]
```

# points

Used by [plants](https://software.farm.bot/docs/plants), [points](https://software.farm.bot/docs/points), [weeds](https://software.farm.bot/docs/weeds), and [tool slots](https://software.farm.bot/docs/tools), where the field `pointer_type` determines the resource.

Notes:
* Soft deleted points will be destroyed without warning when the device hits 800 points.
* New points cannot be created once the device hits 1000 points.

|Method|Description|
|---|---|
|`GET` /api/points|Get an array of all points.|
|`GET` /api/points/:id|Get a single point by id.|
|`POST` /api/points|Create a new point.|
|`PATCH` /api/points/:id|Edit a single point by id.|
|`DELETE` /api/points/:id|Delete a single point by id.|

|Field|Type|`GET`|`GET/:id`|`POST`|`PATCH`|`DELETE`|plant|point|weed|tool slot|
|---|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|`id`<br>Unique identifier set by the database.|integer|📖|📖|||🗑|✅|✅|✅|✅|
|`device_id`<br>Unique device identifier set by the database.|integer|📖|📖|||🗑|✅|✅|✅|✅|
|`created_at`<br>Date and time of creation set by the database.|timestamp|📖|📖|||🗑|✅|✅|✅|✅|
|`updated_at`<br>Date and time of most recent update set by the database.|timestamp|📖|📖|||🗑|✅|✅|✅|✅|
|`name`<br>Point name.|string|📖|📖|📝|📝|🗑|✅|✅|✅|✅|
|`pointer_type`<br>Point type.|"GenericPointer" \| "Plant" \| "ToolSlot" \| "Weed"|📖|📖|📝(required)|📝|🗑|✅|✅|✅|✅|
|`meta`<br>Additional properties.|object|📖|📖|📝|📝|🗑|✅|✅|✅|✅|
|`x`<br>x coordinate.|float|📖|📖|📝(required)|📝|🗑|✅|✅|✅|✅|
|`y`<br>y coordinate.|float|📖|📖|📝(required)|📝|🗑|✅|✅|✅|✅|
|`z`<br>z coordinate.|float|📖|📖|📝(required)|📝|🗑|✅|✅|✅|✅|
|`openfarm_slug`<br>Plant type (from OpenFarm).|string|📖|📖|📝|📝|🗑|✅||||
|`plant_stage`<br>Point status.|"planned" \| "planted" \| "harvested" \| "sprouted" \| "active" \| "removed" \| "pending"|📖|📖|📝|📝|🗑|✅||✅||
|`planted_at`<br>Date and time planted in garden.|timestamp|📖|📖|📝|📝|🗑|✅||||
|`discarded_at`<br>Date and time deleted.|timestamp|📖|📖|📝|📝|🗑||✅|✅||
|`radius`<br>Point radius.|float|📖|📖|📝|📝|🗑|✅|✅|✅||
|`depth`<br>Plant depth.|integer|📖|📖|📝|📝|🗑|✅||||
|`water_curve_id`<br>ID of the water curve for the plant.|integer|📖|📖|📝|📝|🗑|✅||||
|`spread_curve_id`<br>ID of the spread curve for the plant.|integer|📖|📖|📝|📝|🗑|✅||||
|`height_curve_id`<br>ID of the height curve for the plant.|integer|📖|📖|📝|📝|🗑|✅||||
|`pullout_direction`<br>Tool slot direction.|0-4|📖|📖|📝|📝|🗑||||✅|
|`tool_id`<br>ID of the tool in the tool slot.|________|📖|📖|📝|📝|🗑||||✅|
|`gantry_mounted`<br>Is the tool slot mounted on the gantry?|boolean|📖|📖|📝|📝|🗑||||✅|
|`filter`<br>Filter points.|"all" \| "old" \| "kept"|📝|||||||||

__GET /api/points__
```python
import json
import requests

# TOKEN = ...

url = f'https:{TOKEN['token']['unencoded']['iss']}/api/points'
headers = {'Authorization': 'Bearer ' + TOKEN['token']['encoded'],
           'content-type': 'application/json'}
response = requests.get(url, headers=headers)
print(json.dumps(response.json(), indent=2))
```
output:
```json
[
  {
    "id": 50,
    "created_at": "2022-02-02T23:14:25.964Z",
    "updated_at": "2022-02-02T23:14:25.964Z",
    "device_id": 99,
    "name": "Cabbage 0",
    "pointer_type": "Plant",
    "meta": {
    },
    "x": 0,
    "y": 0,
    "z": 0,
    "openfarm_slug": "cabbage",
    "plant_stage": "planned",
    "planted_at": "2022-02-02T23:14:25.964Z",
    "radius": 50.0,
    "depth": 0,
    "water_curve_id": null,
    "spread_curve_id": null,
    "height_curve_id": null
  },
  {
    "id": 51,
    "created_at": "2022-02-02T23:14:25.964Z",
    "updated_at": "2022-02-02T23:14:25.964Z",
    "device_id": 99,
    "name": "Point 0",
    "pointer_type": "GenericPointer",
    "meta": {
      "created_by": "plant-detection"
    },
    "x": 1.0,
    "y": 2.0,
    "z": 3.0,
    "radius": 3.0,
    "discarded_at": null
  },
  {
    "id": 52,
    "created_at": "2022-02-02T23:14:25.964Z",
    "updated_at": "2022-02-02T23:14:25.964Z",
    "device_id": 99,
    "name": "test weed",
    "pointer_type": "Weed",
    "meta": {
    },
    "x": 1.0,
    "y": 2.0,
    "z": 3.0,
    "radius": 3.0,
    "discarded_at": null,
    "plant_stage": "active"
  },
  {
    "id": 53,
    "created_at": "2022-02-02T23:14:25.964Z",
    "updated_at": "2022-02-02T23:14:25.964Z",
    "device_id": 99,
    "name": "Slot 0",
    "pointer_type": "ToolSlot",
    "meta": {
    },
    "x": 4.0,
    "y": 5.0,
    "z": 6.0,
    "tool_id": null,
    "pullout_direction": 0,
    "gantry_mounted": false
  }
]
```

## points/search

|Method|Description|
|---|---|
|`GET` /api/points/search|Get a list of filtered points.|

|Field|Type|`GET`|`GET/:id`|`POST`|`PATCH`|`DELETE`|
|---|---|:---:|:---:|:---:|:---:|:---:|
|`radius`<br>Point size.|float|📝|||||
|`depth`<br>Plant depth.|integer|📝|||||
|`name`<br>Point name.|string|📝|||||
|`pointer_type`<br>Point type.|"GenericPointer" \| "Plant" \| "ToolSlot" \| "Weed"|📝|||||
|`meta`<br>Additional properties.|object|📝|||||
|`x`<br>x coordinate.|float|📝|||||
|`y`<br>y coordinate.|float|📝|||||
|`z`<br>z coordinate.|float|📝|||||
|`openfarm_slug`<br>Plant type (from OpenFarm).|string|📝|||||
|`plant_stage`<br>Point status.|"planned" \| "planted" \| "harvested" \| "sprouted" \| "active" \| "removed" \| "pending"|📝|||||

# public_key

|Method|Description|
|---|---|
|`GET` /api/________|Get an array of all ______.|

|Field|Type|`GET`|`GET/:id`|`POST`|`PATCH`|`DELETE`|
|---|---|:---:|:---:|:---:|:---:|:---:|
|`id`<br>Unique identifier set by the database.|integer|📖|📖|||🗑|
|`device_id`<br>Unique device identifier set by the database.|integer|📖|📖|||🗑|
|`created_at`<br>Date and time of creation set by the database.|timestamp|📖|📖|||🗑|
|`updated_at`<br>Date and time of most recent update set by the database.|timestamp|📖|📖|||🗑|
|`_____`<br>____________.|________|📖|📖|📝|📝|🗑|

__GET /api/__
```python
import json
import requests

# TOKEN = ...

url = f'https:{TOKEN['token']['unencoded']['iss']}/api/__________'
headers = {'Authorization': 'Bearer ' + TOKEN['token']['encoded'],
           'content-type': 'application/json'}
response = requests.get(url, headers=headers)
print(json.dumps(response.json(), indent=2))
```
output:
```json
{
  "id": 43,
  "created_at": "2022-02-02T23:15:36.629Z",
  "updated_at": "2022-02-02T23:15:36.629Z",
  "device_id": 447,

}
```

# regimens

|Method|Description|
|---|---|
|`GET` /api/________|Get an array of all ______.|

|Field|Type|`GET`|`GET/:id`|`POST`|`PATCH`|`DELETE`|
|---|---|:---:|:---:|:---:|:---:|:---:|
|`id`<br>Unique identifier set by the database.|integer|📖|📖|||🗑|
|`device_id`<br>Unique device identifier set by the database.|integer|📖|📖|||🗑|
|`created_at`<br>Date and time of creation set by the database.|timestamp|📖|📖|||🗑|
|`updated_at`<br>Date and time of most recent update set by the database.|timestamp|📖|📖|||🗑|
|`_____`<br>____________.|________|📖|📖|📝|📝|🗑|

__GET /api/__
```python
import json
import requests

# TOKEN = ...

url = f'https:{TOKEN['token']['unencoded']['iss']}/api/__________'
headers = {'Authorization': 'Bearer ' + TOKEN['token']['encoded'],
           'content-type': 'application/json'}
response = requests.get(url, headers=headers)
print(json.dumps(response.json(), indent=2))
```
output:
```json
{
  "id": 43,
  "created_at": "2022-02-02T23:15:36.629Z",
  "updated_at": "2022-02-02T23:15:36.629Z",
  "device_id": 447,

}
```

# releases

|Method|Description|
|---|---|
|`GET` /api/________|Get an array of all ______.|

|Field|Type|`GET`|`GET/:id`|`POST`|`PATCH`|`DELETE`|
|---|---|:---:|:---:|:---:|:---:|:---:|
|`id`<br>Unique identifier set by the database.|integer|📖|📖|||🗑|
|`device_id`<br>Unique device identifier set by the database.|integer|📖|📖|||🗑|
|`created_at`<br>Date and time of creation set by the database.|timestamp|📖|📖|||🗑|
|`updated_at`<br>Date and time of most recent update set by the database.|timestamp|📖|📖|||🗑|
|`_____`<br>____________.|________|📖|📖|📝|📝|🗑|

__GET /api/__
```python
import json
import requests

# TOKEN = ...

url = f'https:{TOKEN['token']['unencoded']['iss']}/api/__________'
headers = {'Authorization': 'Bearer ' + TOKEN['token']['encoded'],
           'content-type': 'application/json'}
response = requests.get(url, headers=headers)
print(json.dumps(response.json(), indent=2))
```
output:
```json
{
  "id": 43,
  "created_at": "2022-02-02T23:15:36.629Z",
  "updated_at": "2022-02-02T23:15:36.629Z",
  "device_id": 447,

}
```

# rmq

|Method|Description|
|---|---|
|`GET` /api/________|Get an array of all ______.|

|Field|Type|`GET`|`GET/:id`|`POST`|`PATCH`|`DELETE`|
|---|---|:---:|:---:|:---:|:---:|:---:|
|`id`<br>Unique identifier set by the database.|integer|📖|📖|||🗑|
|`device_id`<br>Unique device identifier set by the database.|integer|📖|📖|||🗑|
|`created_at`<br>Date and time of creation set by the database.|timestamp|📖|📖|||🗑|
|`updated_at`<br>Date and time of most recent update set by the database.|timestamp|📖|📖|||🗑|
|`_____`<br>____________.|________|📖|📖|📝|📝|🗑|

__GET /api/__
```python
import json
import requests

# TOKEN = ...

url = f'https:{TOKEN['token']['unencoded']['iss']}/api/__________'
headers = {'Authorization': 'Bearer ' + TOKEN['token']['encoded'],
           'content-type': 'application/json'}
response = requests.get(url, headers=headers)
print(json.dumps(response.json(), indent=2))
```
output:
```json
{
  "id": 43,
  "created_at": "2022-02-02T23:15:36.629Z",
  "updated_at": "2022-02-02T23:15:36.629Z",
  "device_id": 447,

}
```

# saved_gardens

|Method|Description|
|---|---|
|`GET` /api/________|Get an array of all ______.|

|Field|Type|`GET`|`GET/:id`|`POST`|`PATCH`|`DELETE`|
|---|---|:---:|:---:|:---:|:---:|:---:|
|`id`<br>Unique identifier set by the database.|integer|📖|📖|||🗑|
|`device_id`<br>Unique device identifier set by the database.|integer|📖|📖|||🗑|
|`created_at`<br>Date and time of creation set by the database.|timestamp|📖|📖|||🗑|
|`updated_at`<br>Date and time of most recent update set by the database.|timestamp|📖|📖|||🗑|
|`_____`<br>____________.|________|📖|📖|📝|📝|🗑|

__GET /api/__
```python
import json
import requests

# TOKEN = ...

url = f'https:{TOKEN['token']['unencoded']['iss']}/api/__________'
headers = {'Authorization': 'Bearer ' + TOKEN['token']['encoded'],
           'content-type': 'application/json'}
response = requests.get(url, headers=headers)
print(json.dumps(response.json(), indent=2))
```
output:
```json
{
  "id": 43,
  "created_at": "2022-02-02T23:15:36.629Z",
  "updated_at": "2022-02-02T23:15:36.629Z",
  "device_id": 447,

}
```

# sensor_readings

|Method|Description|
|---|---|
|`GET` /api/________|Get an array of all ______.|

|Field|Type|`GET`|`GET/:id`|`POST`|`PATCH`|`DELETE`|
|---|---|:---:|:---:|:---:|:---:|:---:|
|`id`<br>Unique identifier set by the database.|integer|📖|📖|||🗑|
|`device_id`<br>Unique device identifier set by the database.|integer|📖|📖|||🗑|
|`created_at`<br>Date and time of creation set by the database.|timestamp|📖|📖|||🗑|
|`updated_at`<br>Date and time of most recent update set by the database.|timestamp|📖|📖|||🗑|
|`_____`<br>____________.|________|📖|📖|📝|📝|🗑|

__GET /api/__
```python
import json
import requests

# TOKEN = ...

url = f'https:{TOKEN['token']['unencoded']['iss']}/api/__________'
headers = {'Authorization': 'Bearer ' + TOKEN['token']['encoded'],
           'content-type': 'application/json'}
response = requests.get(url, headers=headers)
print(json.dumps(response.json(), indent=2))
```
output:
```json
{
  "id": 43,
  "created_at": "2022-02-02T23:15:36.629Z",
  "updated_at": "2022-02-02T23:15:36.629Z",
  "device_id": 447,

}
```

# sensors

|Method|Description|
|---|---|
|`GET` /api/________|Get an array of all ______.|

|Field|Type|`GET`|`GET/:id`|`POST`|`PATCH`|`DELETE`|
|---|---|:---:|:---:|:---:|:---:|:---:|
|`id`<br>Unique identifier set by the database.|integer|📖|📖|||🗑|
|`device_id`<br>Unique device identifier set by the database.|integer|📖|📖|||🗑|
|`created_at`<br>Date and time of creation set by the database.|timestamp|📖|📖|||🗑|
|`updated_at`<br>Date and time of most recent update set by the database.|timestamp|📖|📖|||🗑|
|`_____`<br>____________.|________|📖|📖|📝|📝|🗑|

__GET /api/__
```python
import json
import requests

# TOKEN = ...

url = f'https:{TOKEN['token']['unencoded']['iss']}/api/__________'
headers = {'Authorization': 'Bearer ' + TOKEN['token']['encoded'],
           'content-type': 'application/json'}
response = requests.get(url, headers=headers)
print(json.dumps(response.json(), indent=2))
```
output:
```json
{
  "id": 43,
  "created_at": "2022-02-02T23:15:36.629Z",
  "updated_at": "2022-02-02T23:15:36.629Z",
  "device_id": 447,

}
```

# sequence_versions

|Method|Description|
|---|---|
|`GET` /api/________|Get an array of all ______.|

|Field|Type|`GET`|`GET/:id`|`POST`|`PATCH`|`DELETE`|
|---|---|:---:|:---:|:---:|:---:|:---:|
|`id`<br>Unique identifier set by the database.|integer|📖|📖|||🗑|
|`device_id`<br>Unique device identifier set by the database.|integer|📖|📖|||🗑|
|`created_at`<br>Date and time of creation set by the database.|timestamp|📖|📖|||🗑|
|`updated_at`<br>Date and time of most recent update set by the database.|timestamp|📖|📖|||🗑|
|`_____`<br>____________.|________|📖|📖|📝|📝|🗑|

__GET /api/__
```python
import json
import requests

# TOKEN = ...

url = f'https:{TOKEN['token']['unencoded']['iss']}/api/__________'
headers = {'Authorization': 'Bearer ' + TOKEN['token']['encoded'],
           'content-type': 'application/json'}
response = requests.get(url, headers=headers)
print(json.dumps(response.json(), indent=2))
```
output:
```json
{
  "id": 43,
  "created_at": "2022-02-02T23:15:36.629Z",
  "updated_at": "2022-02-02T23:15:36.629Z",
  "device_id": 447,

}
```

# sequences

|Method|Description|
|---|---|
|`GET` /api/________|Get an array of all ______.|

|Field|Type|`GET`|`GET/:id`|`POST`|`PATCH`|`DELETE`|
|---|---|:---:|:---:|:---:|:---:|:---:|
|`id`<br>Unique identifier set by the database.|integer|📖|📖|||🗑|
|`device_id`<br>Unique device identifier set by the database.|integer|📖|📖|||🗑|
|`created_at`<br>Date and time of creation set by the database.|timestamp|📖|📖|||🗑|
|`updated_at`<br>Date and time of most recent update set by the database.|timestamp|📖|📖|||🗑|
|`_____`<br>____________.|________|📖|📖|📝|📝|🗑|

__GET /api/__
```python
import json
import requests

# TOKEN = ...

url = f'https:{TOKEN['token']['unencoded']['iss']}/api/__________'
headers = {'Authorization': 'Bearer ' + TOKEN['token']['encoded'],
           'content-type': 'application/json'}
response = requests.get(url, headers=headers)
print(json.dumps(response.json(), indent=2))
```
output:
```json
{
  "id": 43,
  "created_at": "2022-02-02T23:15:36.629Z",
  "updated_at": "2022-02-02T23:15:36.629Z",
  "device_id": 447,

}
```

# storage_auth

|Method|Description|
|---|---|
|`GET` /api/________|Get an array of all ______.|

|Field|Type|`GET`|`GET/:id`|`POST`|`PATCH`|`DELETE`|
|---|---|:---:|:---:|:---:|:---:|:---:|
|`id`<br>Unique identifier set by the database.|integer|📖|📖|||🗑|
|`device_id`<br>Unique device identifier set by the database.|integer|📖|📖|||🗑|
|`created_at`<br>Date and time of creation set by the database.|timestamp|📖|📖|||🗑|
|`updated_at`<br>Date and time of most recent update set by the database.|timestamp|📖|📖|||🗑|
|`_____`<br>____________.|________|📖|📖|📝|📝|🗑|

__GET /api/__
```python
import json
import requests

# TOKEN = ...

url = f'https:{TOKEN['token']['unencoded']['iss']}/api/__________'
headers = {'Authorization': 'Bearer ' + TOKEN['token']['encoded'],
           'content-type': 'application/json'}
response = requests.get(url, headers=headers)
print(json.dumps(response.json(), indent=2))
```
output:
```json
{
  "id": 43,
  "created_at": "2022-02-02T23:15:36.629Z",
  "updated_at": "2022-02-02T23:15:36.629Z",
  "device_id": 447,

}
```

# telemetries

|Method|Description|
|---|---|
|`GET` /api/________|Get an array of all ______.|

|Field|Type|`GET`|`GET/:id`|`POST`|`PATCH`|`DELETE`|
|---|---|:---:|:---:|:---:|:---:|:---:|
|`id`<br>Unique identifier set by the database.|integer|📖|📖|||🗑|
|`device_id`<br>Unique device identifier set by the database.|integer|📖|📖|||🗑|
|`created_at`<br>Date and time of creation set by the database.|timestamp|📖|📖|||🗑|
|`updated_at`<br>Date and time of most recent update set by the database.|timestamp|📖|📖|||🗑|
|`_____`<br>____________.|________|📖|📖|📝|📝|🗑|

__GET /api/__
```python
import json
import requests

# TOKEN = ...

url = f'https:{TOKEN['token']['unencoded']['iss']}/api/__________'
headers = {'Authorization': 'Bearer ' + TOKEN['token']['encoded'],
           'content-type': 'application/json'}
response = requests.get(url, headers=headers)
print(json.dumps(response.json(), indent=2))
```
output:
```json
{
  "id": 43,
  "created_at": "2022-02-02T23:15:36.629Z",
  "updated_at": "2022-02-02T23:15:36.629Z",
  "device_id": 447,

}
```

# tokens

|Method|Description|
|---|---|
|`GET` /api/________|Get an array of all ______.|

|Field|Type|`GET`|`GET/:id`|`POST`|`PATCH`|`DELETE`|
|---|---|:---:|:---:|:---:|:---:|:---:|
|`id`<br>Unique identifier set by the database.|integer|📖|📖|||🗑|
|`device_id`<br>Unique device identifier set by the database.|integer|📖|📖|||🗑|
|`created_at`<br>Date and time of creation set by the database.|timestamp|📖|📖|||🗑|
|`updated_at`<br>Date and time of most recent update set by the database.|timestamp|📖|📖|||🗑|
|`_____`<br>____________.|________|📖|📖|📝|📝|🗑|

__GET /api/__
```python
import json
import requests

# TOKEN = ...

url = f'https:{TOKEN['token']['unencoded']['iss']}/api/__________'
headers = {'Authorization': 'Bearer ' + TOKEN['token']['encoded'],
           'content-type': 'application/json'}
response = requests.get(url, headers=headers)
print(json.dumps(response.json(), indent=2))
```
output:
```json
{
  "id": 43,
  "created_at": "2022-02-02T23:15:36.629Z",
  "updated_at": "2022-02-02T23:15:36.629Z",
  "device_id": 447,

}
```

# tools

|Method|Description|
|---|---|
|`GET` /api/________|Get an array of all ______.|

|Field|Type|`GET`|`GET/:id`|`POST`|`PATCH`|`DELETE`|
|---|---|:---:|:---:|:---:|:---:|:---:|
|`id`<br>Unique identifier set by the database.|integer|📖|📖|||🗑|
|`device_id`<br>Unique device identifier set by the database.|integer|📖|📖|||🗑|
|`created_at`<br>Date and time of creation set by the database.|timestamp|📖|📖|||🗑|
|`updated_at`<br>Date and time of most recent update set by the database.|timestamp|📖|📖|||🗑|
|`_____`<br>____________.|________|📖|📖|📝|📝|🗑|

__GET /api/__
```python
import json
import requests

# TOKEN = ...

url = f'https:{TOKEN['token']['unencoded']['iss']}/api/__________'
headers = {'Authorization': 'Bearer ' + TOKEN['token']['encoded'],
           'content-type': 'application/json'}
response = requests.get(url, headers=headers)
print(json.dumps(response.json(), indent=2))
```
output:
```json
{
  "id": 43,
  "created_at": "2022-02-02T23:15:36.629Z",
  "updated_at": "2022-02-02T23:15:36.629Z",
  "device_id": 447,

}
```

# users

|Method|Description|
|---|---|
|`GET` /api/________|Get an array of all ______.|

|Field|Type|`GET`|`GET/:id`|`POST`|`PATCH`|`DELETE`|
|---|---|:---:|:---:|:---:|:---:|:---:|
|`id`<br>Unique identifier set by the database.|integer|📖|📖|||🗑|
|`device_id`<br>Unique device identifier set by the database.|integer|📖|📖|||🗑|
|`created_at`<br>Date and time of creation set by the database.|timestamp|📖|📖|||🗑|
|`updated_at`<br>Date and time of most recent update set by the database.|timestamp|📖|📖|||🗑|
|`_____`<br>____________.|________|📖|📖|📝|📝|🗑|

__GET /api/__
```python
import json
import requests

# TOKEN = ...

url = f'https:{TOKEN['token']['unencoded']['iss']}/api/__________'
headers = {'Authorization': 'Bearer ' + TOKEN['token']['encoded'],
           'content-type': 'application/json'}
response = requests.get(url, headers=headers)
print(json.dumps(response.json(), indent=2))
```
output:
```json
{
  "id": 43,
  "created_at": "2022-02-02T23:15:36.629Z",
  "updated_at": "2022-02-02T23:15:36.629Z",
  "device_id": 447,

}
```

# web_app_config

|Method|Description|
|---|---|
|`GET` /api/________|Get an array of all ______.|

|Field|Type|`GET`|`GET/:id`|`POST`|`PATCH`|`DELETE`|
|---|---|:---:|:---:|:---:|:---:|:---:|
|`id`<br>Unique identifier set by the database.|integer|📖|📖|||🗑|
|`device_id`<br>Unique device identifier set by the database.|integer|📖|📖|||🗑|
|`created_at`<br>Date and time of creation set by the database.|timestamp|📖|📖|||🗑|
|`updated_at`<br>Date and time of most recent update set by the database.|timestamp|📖|📖|||🗑|
|`_____`<br>____________.|________|📖|📖|📝|📝|🗑|

__GET /api/__
```python
import json
import requests

# TOKEN = ...

url = f'https:{TOKEN['token']['unencoded']['iss']}/api/__________'
headers = {'Authorization': 'Bearer ' + TOKEN['token']['encoded'],
           'content-type': 'application/json'}
response = requests.get(url, headers=headers)
print(json.dumps(response.json(), indent=2))
```
output:
```json
{
  "id": 43,
  "created_at": "2022-02-02T23:15:36.629Z",
  "updated_at": "2022-02-02T23:15:36.629Z",
  "device_id": 447,

}
```

# webcam_feeds

|Method|Description|
|---|---|
|`GET` /api/________|Get an array of all ______.|

|Field|Type|`GET`|`GET/:id`|`POST`|`PATCH`|`DELETE`|
|---|---|:---:|:---:|:---:|:---:|:---:|
|`id`<br>Unique identifier set by the database.|integer|📖|📖|||🗑|
|`device_id`<br>Unique device identifier set by the database.|integer|📖|📖|||🗑|
|`created_at`<br>Date and time of creation set by the database.|timestamp|📖|📖|||🗑|
|`updated_at`<br>Date and time of most recent update set by the database.|timestamp|📖|📖|||🗑|
|`_____`<br>____________.|________|📖|📖|📝|📝|🗑|

__GET /api/__
```python
import json
import requests

# TOKEN = ...

url = f'https:{TOKEN['token']['unencoded']['iss']}/api/__________'
headers = {'Authorization': 'Bearer ' + TOKEN['token']['encoded'],
           'content-type': 'application/json'}
response = requests.get(url, headers=headers)
print(json.dumps(response.json(), indent=2))
```
output:
```json
{
  "id": 43,
  "created_at": "2022-02-02T23:15:36.629Z",
  "updated_at": "2022-02-02T23:15:36.629Z",
  "device_id": 447,

}
```

# wizard_step_results

|Method|Description|
|---|---|
|`GET` /api/________|Get an array of all ______.|

|Field|Type|`GET`|`GET/:id`|`POST`|`PATCH`|`DELETE`|
|---|---|:---:|:---:|:---:|:---:|:---:|
|`id`<br>Unique identifier set by the database.|integer|📖|📖|||🗑|
|`device_id`<br>Unique device identifier set by the database.|integer|📖|📖|||🗑|
|`created_at`<br>Date and time of creation set by the database.|timestamp|📖|📖|||🗑|
|`updated_at`<br>Date and time of most recent update set by the database.|timestamp|📖|📖|||🗑|
|`_____`<br>____________.|________|📖|📖|📝|📝|🗑|

__GET /api/__
```python
import json
import requests

# TOKEN = ...

url = f'https:{TOKEN['token']['unencoded']['iss']}/api/__________'
headers = {'Authorization': 'Bearer ' + TOKEN['token']['encoded'],
           'content-type': 'application/json'}
response = requests.get(url, headers=headers)
print(json.dumps(response.json(), indent=2))
```
output:
```json
{
  "id": 43,
  "created_at": "2022-02-02T23:15:36.629Z",
  "updated_at": "2022-02-02T23:15:36.629Z",
  "device_id": 447,

}
```

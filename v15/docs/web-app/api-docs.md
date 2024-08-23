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
|`name`<br>Curve name.|string|📖|📖|📝<br>(required)|📝|🗑|
|`type`<br>Curve type.|"water" \| "spread" \| "height"|📖|📖|📝<br>(required)|📝|🗑|
|`data`<br>Curve data.|{[day: string]: value: integer}|📖|📖|📝<br>(required)|📝|🗑|

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
|`PATCH` /api/device|Edit the device object.|

|Field|Type|`GET`|`GET/:id`|`POST`|`PATCH`|`DELETE`|
|---|---|:---:|:---:|:---:|:---:|:---:|
|`id`<br>Unique identifier set by the database.|integer|📖|||||
|`created_at`<br>Date and time of creation set by the database.|timestamp|📖|||||
|`updated_at`<br>Date and time of most recent update set by the database.|timestamp|📖|||||
|`fb_order_number`<br>Order number.|string \| null|📖|||📝||
|`fbos_version`<br>FarmBot OS version.|string|📖|||||
|`indoor`<br>Is your FarmBot indoors?|boolean|📖|||📝||
|`last_saw_api`<br>Datetime of last API visit.|timestamp|📖|||||
|`lat`<br>Latitude.|float|📖|||📝||
|`lng`<br>Longitude.|float|📖|||📝||
|`mounted_tool_id`<br>The ID of the tool currently attached to the UTM.|integer|📖|||📝||
|`name`<br>FarmBot name.|string|📖|||📝||
|`ota_hour`<br>Over-the-air update local time.|0-23 \| null|📖|||📝||
|`ota_hour_utc`<br>Over-the-air update UTC time.|0-23 \| null|📖|||||
|`rpi`<br>FarmBot computer model.|"3" \| "4" \| "01" \| "02"|📖|||📝||
|`serial_number`<br>FarmBot serial number.|string|📖|||||
|`setup_completed_at`<br>Datetime device setup completed.|timestamp|📖|||📝||
|`throttled_at`<br>Datetime device throttle begin.|timestamp|📖|||||
|`throttled_until`<br>Datetime device throttle end.|timestamp|📖|||||
|`timezone`<br>Timezone.|string|📖|||📝||
|`max_log_age_in_days`<br>Logs deleted after __ days.|integer|📖|||||
|`max_sequence_count`<br>Maximum number of allowed sequences.|integer|📖|||||
|`max_sequence_length`<br>Maximum allowed sequence length.|integer|📖|||||
|`tz_offset_hrs`<br>Hours offset from UTC.|integer|📖|||||

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
|`password`<br>Account password.|string|||📝<br>(required)|||

## device/seed

|Method|Description|
|---|---|
|`POST` /api/device/seed|Seed the device with standard resources.|

|Field|Type|`GET`|`GET/:id`|`POST`|`PATCH`|`DELETE`|
|---|---|:---:|:---:|:---:|:---:|:---:|
|`product_line`<br>FarmBot model.|"express_1.0" \| "express_1.1" \| "express_1.2" \| "express_xl_1.0" \| "express_xl_1.1" \| "express_xl_1.2" \| "genesis_1.2" \| "genesis_1.3" \| "genesis_1.4" \| "genesis_1.5" \| "genesis_1.6" \| "genesis_1.7" \| "genesis_xl_1.4" \| "genesis_xl_1.5" \| "genesis_xl_1.6" \| "genesis_xl_1.7" \| "none"|||📝<br>(required)|||
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
|`repeat`<br>Number of times to repeat the farm event.|integer|📖|📖|📝<br>(required)|📝|🗑|
|`time_unit`<br>Time period for repeat.|"never" \| "minutely" \| "hourly" \| "daily" \| "weekly" \| "monthly" \| "yearly"|📖|📖|📝<br>(required)|📝|🗑|
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
|`key`<br>Environment variable label.|string|📖|📖|📝<br>(required)|📝|🗑|
|`value`<br>Environment variable value.|string|📖|📖|📝<br>(required)|📝|🗑|

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
|`PATCH` /api/firmware_config|Edit the firmware configuration object.|
|`DELETE` /api/firmware_config|Delete the firmware configuration object.|

|Field|Type|`GET`|`GET/:id`|`POST`|`PATCH`|`DELETE`|
|---|---|:---:|:---:|:---:|:---:|:---:|
|`id`<br>Unique identifier set by the database.|integer|📖||||🗑|
|`device_id`<br>Unique device identifier set by the database.|integer|📖||||🗑|
|`created_at`<br>Date and time of creation set by the database.|timestamp|📖||||🗑|
|`updated_at`<br>Date and time of most recent update set by the database.|timestamp|📖||||🗑|
|`encoder_enabled_x`<br>Enable encoders or stall detection for the x axis.|0 \| 1|📖|||📝|🗑|
|`encoder_enabled_y`<br>Enable encoders or stall detection for the y axis.|0 \| 1|📖|||📝|🗑|
|`encoder_enabled_z`<br>Enable encoders or stall detection for the z axis.|0 \| 1|📖|||📝|🗑|
|`encoder_invert_x`<br>Invert the encoders on the x axis.|0 \| 1|📖|||📝|🗑|
|`encoder_invert_y`<br>Invert the encoders on the y axis.|0 \| 1|📖|||📝|🗑|
|`encoder_invert_z`<br>Invert the encoders on the z axis.|0 \| 1|📖|||📝|🗑|
|`encoder_missed_steps_decay_x`<br>Reduction to missed step total for every good step for the x axis.|integer|📖|||📝|🗑|
|`encoder_missed_steps_decay_y`<br>Reduction to missed step total for every good step for the y axis.|integer|📖|||📝|🗑|
|`encoder_missed_steps_decay_z`<br>Reduction to missed step total for every good step for the z axis.|integer|📖|||📝|🗑|
|`encoder_missed_steps_max_x`<br>Number of steps before the motor is considered to have stalled for the x axis.|integer|📖|||📝|🗑|
|`encoder_missed_steps_max_y`<br>Number of steps before the motor is considered to have stalled for the y axis.|integer|📖|||📝|🗑|
|`encoder_missed_steps_max_z`<br>Number of steps before the motor is considered to have stalled for the z axis.|integer|📖|||📝|🗑|
|`encoder_scaling_x`<br>10000 * (motor resolution) / (encoder resolution).|integer|📖|||📝|🗑|
|`encoder_scaling_y`<br>10000 * (motor resolution) / (encoder resolution).|integer|📖|||📝|🗑|
|`encoder_scaling_z`<br>10000 * (motor resolution) / (encoder resolution).|integer|📖|||📝|🗑|
|`encoder_type_x`<br>.Unused|0 \| 1|📖|||📝|🗑|
|`encoder_type_y`<br>.Unused|0 \| 1|📖|||📝|🗑|
|`encoder_type_z`<br>.Unused|0 \| 1|📖|||📝|🗑|
|`encoder_use_for_pos_x`<br>.Use the encoders for calculating movements on the x axis.|0 \| 1|📖|||📝|🗑|
|`encoder_use_for_pos_y`<br>.Use the encoders for calculating movements on the y axis.|0 \| 1|📖|||📝|🗑|
|`encoder_use_for_pos_z`<br>.Use the encoders for calculating movements on the z axis.|0 \| 1|📖|||📝|🗑|
|`movement_axis_nr_steps_x`<br>X axis length in steps.|integer|📖|||📝|🗑|
|`movement_axis_nr_steps_y`<br>Y axis length in steps.|integer|📖|||📝|🗑|
|`movement_axis_nr_steps_z`<br>Z axis length in steps.|integer|📖|||📝|🗑|
|`movement_enable_endpoints_x`<br>Enable endstops for the x axis.|0 \| 1|📖|||📝|🗑|
|`movement_enable_endpoints_y`<br>Enable endstops for the y axis.|0 \| 1|📖|||📝|🗑|
|`movement_enable_endpoints_z`<br>Enable endstops for the z axis.|0 \| 1|📖|||📝|🗑|
|`movement_home_at_boot_x`<br>Find home upon startup for the x axis.|0 \| 1|📖|||📝|🗑|
|`movement_home_at_boot_y`<br>Find home upon startup for the y axis.|0 \| 1|📖|||📝|🗑|
|`movement_home_at_boot_z`<br>Find home upon startup for the z axis.|0 \| 1|📖|||📝|🗑|
|`movement_home_spd_x`<br>X axis homing speed in steps per second.|integer|📖|||📝|🗑|
|`movement_home_spd_y`<br>Y axis homing speed in steps per second.|integer|📖|||📝|🗑|
|`movement_home_spd_z`<br>Z axis homing speed in steps per second.|integer|📖|||📝|🗑|
|`movement_home_up_x`<br>Restrict travel to negative coordinate locations for the x axis.|0 \| 1|📖|||📝|🗑|
|`movement_home_up_y`<br>Restrict travel to negative coordinate locations for the y axis.|0 \| 1|📖|||📝|🗑|
|`movement_home_up_z`<br>Restrict travel to negative coordinate locations for the z axis.|0 \| 1|📖|||📝|🗑|
|`movement_invert_endpoints_x`<br>Swap the min and max limit switches for the x axis.|0 \| 1|📖|||📝|🗑|
|`movement_invert_endpoints_y`<br>Swap the min and max limit switches for the y axis.|0 \| 1|📖|||📝|🗑|
|`movement_invert_endpoints_z`<br>Swap the min and max limit switches for the z axis.|0 \| 1|📖|||📝|🗑|
|`movement_invert_motor_x`<br>Invert motor direction for the x axis.|0 \| 1|📖|||📝|🗑|
|`movement_invert_motor_y`<br>Invert motor direction for the y axis.|0 \| 1|📖|||📝|🗑|
|`movement_invert_motor_z`<br>Invert motor direction for the z axis.|0 \| 1|📖|||📝|🗑|
|`movement_keep_active_x`<br>Always power motors on the x axis.|0 \| 1|📖|||📝|🗑|
|`movement_keep_active_y`<br>Always power motors on the y axis.|0 \| 1|📖|||📝|🗑|
|`movement_keep_active_z`<br>Always power motors on the z axis.|0 \| 1|📖|||📝|🗑|
|`movement_max_spd_x`<br>Max speed in steps per second for the x axis.|integer|📖|||📝|🗑|
|`movement_max_spd_y`<br>Max speed in steps per second for the y axis.|integer|📖|||📝|🗑|
|`movement_max_spd_z`<br>Max speed in steps per second for the z axis.|integer|📖|||📝|🗑|
|`movement_min_spd_x`<br>Minimum speed in steps per second for the x axis.|integer|📖|||📝|🗑|
|`movement_min_spd_y`<br>Minimum speed in steps per second for the y axis.|integer|📖|||📝|🗑|
|`movement_min_spd_z`<br>Minimum speed in steps per second for the z axis.|integer|📖|||📝|🗑|
|`movement_secondary_motor_invert_x`<br>Invert the direction of the 2nd x axis motor.|0 \| 1|📖|||📝|🗑|
|`movement_secondary_motor_x`<br>Enable the 2nd x axis motor.|0 \| 1|📖|||📝|🗑|
|`movement_step_per_mm_x`<br>Number of steps per millimeter on the x axis.|integer|📖|||📝|🗑|
|`movement_step_per_mm_y`<br>Number of steps per millimeter on the y axis.|integer|📖|||📝|🗑|
|`movement_step_per_mm_z`<br>Number of steps per millimeter on the z axis.|integer|📖|||📝|🗑|
|`movement_steps_acc_dec_x`<br>Number of steps used to accelerate for the x axis.|integer|📖|||📝|🗑|
|`movement_steps_acc_dec_y`<br>Number of steps used to accelerate for the y axis.|integer|📖|||📝|🗑|
|`movement_steps_acc_dec_z`<br>Number of steps used to accelerate for the z axis.|integer|📖|||📝|🗑|
|`movement_stop_at_home_x`<br>Enable stop at home for the x axis.|0 \| 1|📖|||📝|🗑|
|`movement_stop_at_home_y`<br>Enable stop at home for the y axis.|0 \| 1|📖|||📝|🗑|
|`movement_stop_at_home_z`<br>Enable stop at home for the z axis.|0 \| 1|📖|||📝|🗑|
|`movement_stop_at_max_x`<br>Enable stop at max for the x axis.|0 \| 1|📖|||📝|🗑|
|`movement_stop_at_max_y`<br>Enable stop at max for the y axis.|0 \| 1|📖|||📝|🗑|
|`movement_stop_at_max_z`<br>Enable stop at max for the z axis.|0 \| 1|📖|||📝|🗑|
|`movement_timeout_x`<br>Amount of time to wait for a command to execute before stopping in seconds for the x axis.|integer|📖|||📝|🗑|
|`movement_timeout_y`<br>Amount of time to wait for a command to execute before stopping in seconds for the y axis.|integer|📖|||📝|🗑|
|`movement_timeout_z`<br>Amount of time to wait for a command to execute before stopping in seconds for the z axis.|integer|📖|||📝|🗑|
|`param_config_ok`<br>Unused.|integer|📖|||📝|🗑|
|`param_e_stop_on_mov_err`<br>E-Stop upon movement error.|0 \| 1|📖|||📝|🗑|
|`param_mov_nr_retry`<br>Number of times to retry a movement.|integer|📖|||📝|🗑|
|`param_test`<br>Unused.|integer|📖|||📝|🗑|
|`param_use_eeprom`<br>Unused.|0 \| 1|📖|||📝|🗑|
|`param_version`<br>Unused.|integer|📖|||📝|🗑|
|`pin_guard_1_active_state`<br>Pin guard 1 active state.|0 \| 1|📖|||📝|🗑|
|`pin_guard_1_pin_nr`<br>Pin guard 1 pin number.|0-69|📖|||📝|🗑|
|`pin_guard_1_time_out`<br>Pin guard 1 number of seconds before turning the pin to the inactive state.|integer|📖|||📝|🗑|
|`pin_guard_2_active_state`<br>Pin guard 2 active state.|0 \| 1|📖|||📝|🗑|
|`pin_guard_2_pin_nr`<br>Pin guard 2 pin number.|0-69|📖|||📝|🗑|
|`pin_guard_2_time_out`<br>Pin guard 2 number of seconds before turning the pin to the inactive state.|integer|📖|||📝|🗑|
|`pin_guard_3_active_state`<br>Pin guard 3 active state.|0 \| 1|📖|||📝|🗑|
|`pin_guard_3_pin_nr`<br>Pin guard 3 pin number.|0-69|📖|||📝|🗑|
|`pin_guard_3_time_out`<br>Pin guard 3 number of seconds before turning the pin to the inactive state.|integer|📖|||📝|🗑|
|`pin_guard_4_active_state`<br>Pin guard 4 active state.|0 \| 1|📖|||📝|🗑|
|`pin_guard_4_pin_nr`<br>Pin guard 4 pin number.|0-69|📖|||📝|🗑|
|`pin_guard_4_time_out`<br>Pin guard 4 number of seconds before turning the pin to the inactive state.|integer|📖|||📝|🗑|
|`pin_guard_5_active_state`<br>Pin guard 5 active state.|0 \| 1|📖|||📝|🗑|
|`pin_guard_5_pin_nr`<br>Pin guard 5 pin number.|0-69|📖|||📝|🗑|
|`pin_guard_5_time_out`<br>Pin guard 5 number of seconds before turning the pin to the inactive state.|integer|📖|||📝|🗑|
|`movement_invert_2_endpoints_x`<br>Enable for normally closed (NC), disable for normally open (NO).|0 \| 1|📖|||📝|🗑|
|`movement_invert_2_endpoints_y`<br>Enable for normally closed (NC), disable for normally open (NO).|0 \| 1|📖|||📝|🗑|
|`movement_invert_2_endpoints_z`<br>Enable for normally closed (NC), disable for normally open (NO).|0 \| 1|📖|||📝|🗑|
|`movement_microsteps_x`<br>Number of microsteps per step on the x axis.|integer|📖|||📝|🗑|
|`movement_microsteps_y`<br>Number of microsteps per step on the y axis.|integer|📖|||📝|🗑|
|`movement_microsteps_z`<br>Number of microsteps per step on the z axis.|integer|📖|||📝|🗑|
|`movement_motor_current_x`<br>Motor current on the x axis.|0-1823|📖|||📝|🗑|
|`movement_motor_current_y`<br>Motor current on the y axis.|0-1823|📖|||📝|🗑|
|`movement_motor_current_z`<br>Motor current on the z axis.|0-1823|📖|||📝|🗑|
|`movement_stall_sensitivity_x`<br>Stall sensitivity on the x axis. Lower is more sensitive.|-63-63|📖|||📝|🗑|
|`movement_stall_sensitivity_y`<br>Stall sensitivity on the y axis. Lower is more sensitive.|-63-63|📖|||📝|🗑|
|`movement_stall_sensitivity_z`<br>Stall sensitivity on the z axis. Lower is more sensitive.|-63-63|📖|||📝|🗑|
|`movement_min_spd_z2`<br>Min speed in steps per second for z axis movements towards home.|integer|📖|||📝|🗑|
|`movement_max_spd_z2`<br>Maximum speed in steps per second for z axis movements towards home.|integer|📖|||📝|🗑|
|`movement_steps_acc_dec_z2`<br>Number of steps used for acceleration for z axis movements towards home.|integer|📖|||📝|🗑|
|`movement_calibration_retry_x`<br>Number of times to retry calibration for the x axis.|integer|📖|||📝|🗑|
|`movement_calibration_retry_y`<br>Number of times to retry calibration for the y axis.|integer|📖|||📝|🗑|
|`movement_calibration_retry_z`<br>Number of times to retry calibration for the z axis.|integer|📖|||📝|🗑|
|`movement_calibration_deadzone_x`<br>Distance in steps to group calibration retries for the x axis.|integer|📖|||📝|🗑|
|`movement_calibration_deadzone_y`<br>Distance in steps to group calibration retries for the y axis.|integer|📖|||📝|🗑|
|`movement_calibration_deadzone_z`<br>Distance in steps to group calibration retries for the z axis.|integer|📖|||📝|🗑|
|`movement_axis_stealth_x`<br>Enable quiet mode for the x axis.|0 \| 1|📖|||📝|🗑|
|`movement_axis_stealth_y`<br>Enable quiet mode for the y axis.|0 \| 1|📖|||📝|🗑|
|`movement_axis_stealth_z`<br>Enable quiet mode for the z axis.|0 \| 1|📖|||📝|🗑|
|`movement_calibration_retry_total_x`<br>Total number of times to retry calibration for the x axis.|integer|📖|||📝|🗑|
|`movement_calibration_retry_total_y`<br>Total number of times to retry calibration for the y axis.|integer|📖|||📝|🗑|
|`movement_calibration_retry_total_z`<br>Total number of times to retry calibration for the z axis.|integer|📖|||📝|🗑|
|`pin_report_1_pin_nr`<br>Report values of the pin periodically.|0-69|📖|||📝|🗑|
|`pin_report_2_pin_nr`<br>Report values of the pin periodically.|0-69|📖|||📝|🗑|

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
|`parent_id`<br>ID of the parent folder, if any.|integer \| null|📖|📖|📝|📝<br>(required)|🗑|
|`name`<br>Folder name.|string|📖|📖|📝<br>(required)|📝|🗑|
|`color`<br>Folder color.|string|📖|📖|📝<br>(required)|📝|🗑|

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
|`attachment_url`<br>Image URL.|string|📖|📖|📝<br>(required)||🗑|
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
|`message`<br>Log message.|string|📖||📝<br>(required)||🗑|
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

__POST /api/logs__
```python
import json
import requests

# TOKEN = ...

url = f'https:{TOKEN['token']['unencoded']['iss']}/api/logs'
headers = {'Authorization': 'Bearer ' + TOKEN['token']['encoded'],
           'content-type': 'application/json'}
payload = {
    'message': 'Hello World!',
    'type': 'success',
    'channels': ['toast'],
}
response = requests.post(url, headers=headers, json=payload)
print(json.dumps(response.json(), indent=2))
```
output:
```json
{
  "id": 1234567,
  "created_at": 1643843034,
  "updated_at": "2022-02-02T23:14:54.423Z",
  "channels": [
    "toast"
  ],
  "message": "Hello World!",
  "meta": null,
  "major_version": null,
  "minor_version": null,
  "patch_version": null,
  "type": "success",
  "verbosity": 1,
  "x": null,
  "y": null,
  "z": null
}
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
|`email`<br>Account email address.|string|||📝<br>(required)|||

## change

|Method|Description|
|---|---|
|`PATCH` /api/password_resets|Change the account password.|

|Field|Type|`GET`|`GET/:id`|`POST`|`PATCH`|`DELETE`|
|---|---|:---:|:---:|:---:|:---:|:---:|
|`password`<br>New account password.|string||||📝<br>(required)||
|`password_confirmation`<br>New account password.|string||||📝<br>(required)||
|`id`<br>Token.|string||||📝<br>(required)||

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
|`pin`<br>Pin number.|integer|📖|📖|📝<br>(required)|📝|🗑|
|`label`<br>Peripheral name.|string|📖|📖|📝<br>(required)|📝|🗑|
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
|`pin_num`<br>Button pin number.|integer|📖|📖|📝<br>(required)|📝|🗑|
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
|`saved_garden_id`<br>ID of the saved garden to which the plant belongs.|integer|📖||📝<br>(required)|📝|🗑|
|`radius`<br>Size of the plant.|float|📖||📝|📝|🗑|
|`x`<br>x coordinate.|float|📖||📝<br>(required)|📝|🗑|
|`y`<br>y coordinate.|float|📖||📝<br>(required)|📝|🗑|
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
|`name`<br>Group name.|string|📖|📖|📝<br>(required)|📝|🗑|
|`point_ids`<br>Array of manually included point IDs.|integer[]|📖|📖|📝<br>(required)|📝|🗑|
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
|`pointer_type`<br>Point type.|"GenericPointer" \| "Plant" \| "ToolSlot" \| "Weed"|📖|📖|📝<br>(required)|📝|🗑|✅|✅|✅|✅|
|`meta`<br>Additional properties.|object|📖|📖|📝|📝|🗑|✅|✅|✅|✅|
|`x`<br>x coordinate.|float|📖|📖|📝<br>(required)|📝|🗑|✅|✅|✅|✅|
|`y`<br>y coordinate.|float|📖|📖|📝<br>(required)|📝|🗑|✅|✅|✅|✅|
|`z`<br>z coordinate.|float|📖|📖|📝<br>(required)|📝|🗑|✅|✅|✅|✅|
|`openfarm_slug`<br>Plant type (from OpenFarm).|string|📖|📖|📝|📝|🗑|✅||||
|`plant_stage`<br>Point status.|"planned" \| "planted" \| "harvested" \| "sprouted" \| "active" \| "removed" \| "pending"|📖|📖|📝|📝|🗑|✅||✅||
|`planted_at`<br>Date and time planted in garden.|timestamp|📖|📖|📝|📝|🗑|✅||||
|`discarded_at`<br>Date and time deleted.|timestamp|📖|📖|||🗑||✅|✅||
|`radius`<br>Point radius.|float|📖|📖|📝|📝|🗑|✅|✅|✅||
|`depth`<br>Plant depth.|integer|📖|📖|📝|📝|🗑|✅||||
|`water_curve_id`<br>ID of the water curve for the plant.|integer|📖|📖|📝|📝|🗑|✅||||
|`spread_curve_id`<br>ID of the spread curve for the plant.|integer|📖|📖|📝|📝|🗑|✅||||
|`height_curve_id`<br>ID of the height curve for the plant.|integer|📖|📖|📝|📝|🗑|✅||||
|`pullout_direction`<br>Tool slot direction.|0-4|📖|📖|📝|📝|🗑||||✅|
|`tool_id`<br>ID of the tool in the tool slot.|integer|📖|📖|📝|📝|🗑||||✅|
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

__POST /api/points__
```python
import json
import requests

# TOKEN = ...

url = f'https:{TOKEN['token']['unencoded']['iss']}/api/points'
headers = {'Authorization': 'Bearer ' + TOKEN['token']['encoded'],
           'content-type': 'application/json'}
payload = {
    'pointer_type': 'Plant',
    'name': 'Strawberry',
    'openfarm_slug': 'strawberry',
    'x': 1,
    'y': 2,
    'z': 3,
}
response = requests.post(url, headers=headers, json=payload)
print(json.dumps(response.json(), indent=2))
```
output:
```json
{
  "id": 123,
  "created_at": "2022-02-02T23:14:25.964Z",
  "updated_at": "2022-02-02T23:14:25.964Z",
  "device_id": 99,
  "name": "Strawberry",
  "pointer_type": "Plant",
  "meta": {},
  "x": 1,
  "y": 2,
  "z": 3,
  "openfarm_slug": "strawberry",
  "plant_stage": "planned",
  "planted_at": null,
  "radius": 25.0,
  "depth": 0,
  "water_curve_id": null,
  "spread_curve_id": null,
  "height_curve_id": null
}
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
|`GET` /api/public_key|Get the public key.|

__GET /api/public_key__
```python
import json
import requests

# TOKEN = ...

url = f'https:{TOKEN['token']['unencoded']['iss']}/api/public_key'
response = requests.get(url)
print(response.text)
```
output:
```
-----BEGIN PUBLIC KEY-----
2pVjj0NP5GNGzSqz8OVZUDJceDlsYpY24tUzJEtEzBJdN32zKM7PEkjiSZKqE3Uq
lWKTxcArHrk/VPVp53dRhP0dza8dluHHlbsC19FmOWjcBRk2d1QUmhfVQMxc+EVE
Hv5RSjtY40tB5NXRpXmbTOz7yejh2DsagCMTTyR8tQ/HYESXWama4s/MpRcVGHPY
6rZbv3a67/yqsrxNsqnmG+JrAvKsQd86p7upbo4jEQQ2SatXSuzYCCl8wOL6wkz2
E+qJNUTbyfTjyegBkUw6PEFnMhSUvzmBsWmy6X12vK9Too8qBhOYzYIPtN4oB9eY
v4oT7LUFYK5agv2lVG6Z1UvoB16T+moOfba/l1xkgG3xGqI/LYzxIM74h5ppjtkw
DmhdoWLZ
-----END PUBLIC KEY-----
```

# regimens

See [regimens](https://software.farm.bot/docs/regimens).

|Method|Description|
|---|---|
|`GET` /api/regimens|Get an array of all regimens.|
|`GET` /api/regimens/:id|Get a single regimen by id.|
|`POST` /api/regimens|Create a new regimen.|
|`PATCH` /api/regimens/:id|Edit a single regimen by id.|
|`DELETE` /api/regimens/:id|Delete a single regimen by id.|

|Field|Type|`GET`|`GET/:id`|`POST`|`PATCH`|`DELETE`|
|---|---|:---:|:---:|:---:|:---:|:---:|
|`id`<br>Unique identifier set by the database.|integer|📖|📖|||🗑|
|`device_id`<br>Unique device identifier set by the database.|integer|📖|📖|||🗑|
|`created_at`<br>Date and time of creation set by the database.|timestamp|📖|📖|||🗑|
|`updated_at`<br>Date and time of most recent update set by the database.|timestamp|📖|📖|||🗑|
|`name`<br>Regimen name.|string|📖|📖|📝<br>(required)|📝|🗑|
|`color`<br>Regimen color.|"blue" \| "green" \| "yellow" \| "orange" \| "purple" \| "pink" \| "gray" \| "red"|📖|📖|📝<br>(required)|📝|🗑|
|`body`<br>Variable data.|Array|📖|📖|📝|📝|🗑|
|`regimen_items`<br>Sequence executions scheduled in the regimen.|Array (`time_offset` is in milliseconds)|📖|📖|📝<br>(required)|📝|🗑|

__GET /api/regimens__
```python
import json
import requests

# TOKEN = ...

url = f'https:{TOKEN['token']['unencoded']['iss']}/api/regimens'
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
    "created_at": "2022-02-02T23:15:50.695Z",
    "updated_at": "2022-02-02T23:15:50.766Z",
    "name": "specs",
    "color": "red",
    "device_id": 234,
    "body": [
      {
        "kind": "parameter_application",
        "args": {
          "label": "parent",
          "data_value": {
            "kind": "coordinate",
            "args": {
              "x": 0,
              "y": 0,
              "z": 0
            }
          }
        }
      }
    ],
    "regimen_items": [
      {
        "id": 6,
        "created_at": "2022-02-02T23:15:50.695Z",
        "updated_at": "2022-02-02T23:15:50.766Z",
        "regimen_id": 15,
        "sequence_id": 70,
        "time_offset": 100
      }
    ]
  }
]
```

# releases

Used by the [FarmBot OS download page](https://os.farm.bot) and FarmBot OS OTA updates.

|Method|Description|
|---|---|
|`GET` /api/releases|Get a release.|

|Field|Type|`GET`|`GET/:id`|`POST`|`PATCH`|`DELETE`|
|---|---|:---:|:---:|:---:|:---:|:---:|
|`id`<br>Unique identifier set by the database.|integer|📖|||||
|`created_at`<br>Date and time of creation set by the database.|timestamp|📖|||||
|`updated_at`<br>Date and time of most recent update set by the database.|timestamp|📖|||||
|`image_url`<br>URL of FarmBot OS release .fw file.|string|📖|||||
|`version`<br>FarmBot OS release version.|string|📖|||||
|`platform`<br>FarmBot OS computer model.|"rpi" \| "rpi3" \| "rpi4"|📖|||||
|`channel`<br>Release channel.|"stable" \| "beta" \| "alpha"|📖|||||
|`dot_img_url`<br>URL of FarmBot OS release .img file.|string|📖|||||

__GET /api/releases__
```python
import json
import requests

# TOKEN = ...

url = f'https:{TOKEN['token']['unencoded']['iss']}/api/releases'
headers = {'Authorization': 'Bearer ' + TOKEN['token']['encoded'],
           'content-type': 'application/json'}
payload = {
    'channel': 'stable',
    'platform': 'rpi3',
}
response = requests.get(url, headers=headers, json=payload)
print(json.dumps(response.json(), indent=2))
```
output:
```json
{
  "id": 2,
  "created_at": "2022-02-02T23:14:27.277Z",
  "updated_at": "2022-02-02T23:14:27.277Z",
  "image_url": "gopher://localhost:3000/b",
  "version": "1.2.3-rc7",
  "platform": "rpi3",
  "channel": "stable",
  "dot_img_url": null
}
```

# saved_gardens

Used by [gardens](https://software.farm.bot/docs/gardens).

|Method|Description|
|---|---|
|`GET` /api/saved_gardens|Get an array of all saved gardens.|
|`POST` /api/saved_gardens|Create a new saved garden.|
|`PATCH` /api/saved_gardens/:id|Edit a single saved garden by id.|
|`DELETE` /api/saved_gardens/:id|Delete a single saved garden by id.|

|Field|Type|`GET`|`GET/:id`|`POST`|`PATCH`|`DELETE`|
|---|---|:---:|:---:|:---:|:---:|:---:|
|`id`<br>Unique identifier set by the database.|integer|📖||||🗑|
|`device_id`<br>Unique device identifier set by the database.|integer|📖||||🗑|
|`created_at`<br>Date and time of creation set by the database.|timestamp|📖||||🗑|
|`updated_at`<br>Date and time of most recent update set by the database.|timestamp|📖||||🗑|
|`name`<br>Saved garden name.|string|📖||📝<br>(required)|📝|🗑|
|`notes`<br>Notes.|string|📖||📝|📝|🗑|

__GET /api/saved_gardens__
```python
import json
import requests

# TOKEN = ...

url = f'https:{TOKEN['token']['unencoded']['iss']}/api/saved_gardens'
headers = {'Authorization': 'Bearer ' + TOKEN['token']['encoded'],
           'content-type': 'application/json'}
response = requests.get(url, headers=headers)
print(json.dumps(response.json(), indent=2))
```
output:
```json
[
  {
    "id": 32,
    "name": "Garden 0",
    "device_id": 384,
    "created_at": "2022-02-02T23:15:33.978Z",
    "updated_at": "2022-02-02T23:15:33.978Z",
    "notes": "notes"
  }
]
```

## saved_gardens/:id/apply

|Method|Description|
|---|---|
|`POST` /api/saved_gardens/:id/apply|Apply a saved garden, destroying existing plants.|
|`PATCH` /api/saved_gardens/:id/apply|Apply a saved garden. Errors if plants exist.|

## saved_gardens/snapshot

|Method|Description|
|---|---|
|`POST` /api/saved_gardens/snapshot|Copy the current garden to a new saved garden.|

# sensor_readings

|Method|Description|
|---|---|
|`GET` /api/sensor_readings|Get an array of all sensor readings.|
|`GET` /api/sensor_readings/:id|Get a single sensor reading by id.|
|`POST` /api/sensor_readings|Create a new sensor reading.|
|`DELETE` /api/sensor_readings/:id|Delete a single sensor reading by id.|

|Field|Type|`GET`|`GET/:id`|`POST`|`PATCH`|`DELETE`|
|---|---|:---:|:---:|:---:|:---:|:---:|
|`id`<br>Unique identifier set by the database.|integer|📖|📖|||🗑|
|`created_at`<br>Date and time of creation set by the database.|timestamp|📖|📖|||🗑|
|`updated_at`<br>Date and time of most recent update set by the database.|timestamp|📖|📖|||🗑|
|`mode`<br>Sensor pin read mode, `0` for digital, `1` for analog.|0 \| 1|📖|📖|📝||🗑|
|`pin`<br>Sensor pin number.|0-69|📖|📖|📝<br>(required)||🗑|
|`value`<br>Sensor value.|0-1023|📖|📖|📝<br>(required)||🗑|
|`x`<br>x coordinate.|float|📖|📖|📝<br>(required)||🗑|
|`y`<br>y coordinate.|float|📖|📖|📝<br>(required)||🗑|
|`z`<br>z coordinate.|float|📖|📖|📝<br>(required)||🗑|
|`read_at`<br>Date and time of sensor reading.|timestamp|📖|📖|📝||🗑|

__GET /api/sensor_readings__
```python
import json
import requests

# TOKEN = ...

url = f'https:{TOKEN['token']['unencoded']['iss']}/api/sensor_readings'
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
    "created_at": "2022-02-02T23:14:15.819Z",
    "updated_at": "2022-02-02T23:14:15.819Z",
    "mode": 1,
    "pin": 66,
    "value": 80,
    "x": 281.0,
    "y": 205.0,
    "z": 76.0,
    "read_at": "2022-02-02T23:14:15.819Z"
  }
]
```

# sensors

See [sensors](https://software.farm.bot/docs/sensors).

|Method|Description|
|---|---|
|`GET` /api/sensors|Get an array of all sensors.|
|`GET` /api/sensors/:id|Get a single sensor by id.|
|`POST` /api/sensors|Create a new sensor.|
|`PATCH` /api/sensors/:id|Edit a single sensor by id.|
|`DELETE` /api/sensors/:id|Delete a single sensor by id.|

|Field|Type|`GET`|`GET/:id`|`POST`|`PATCH`|`DELETE`|
|---|---|:---:|:---:|:---:|:---:|:---:|
|`id`<br>Unique identifier set by the database.|integer|📖|📖|||🗑|
|`created_at`<br>Date and time of creation set by the database.|timestamp|📖|📖|||🗑|
|`updated_at`<br>Date and time of most recent update set by the database.|timestamp|📖|📖|||🗑|
|`mode`<br>Sensor pin read mode, `0` for digital, `1` for analog.|0 \| 1|📖|📖|📝<br>(required)|📝|🗑|
|`pin`<br>Sensor pin number.|0-69|📖|📖|📝<br>(required)|📝|🗑|
|`label`<br>Sensor name.|string|📖|📖|📝<br>(required)|📝|🗑|

__GET /api/sensors__
```python
import json
import requests

# TOKEN = ...

url = f'https:{TOKEN['token']['unencoded']['iss']}/api/sensors'
headers = {'Authorization': 'Bearer ' + TOKEN['token']['encoded'],
           'content-type': 'application/json'}
response = requests.get(url, headers=headers)
print(json.dumps(response.json(), indent=2))
```
output:
```json
[
  {
    "id": 4,
    "created_at": "2022-02-02T23:14:40.839Z",
    "updated_at": "2022-02-02T23:14:40.839Z",
    "pin": 3,
    "label": "My Sensor",
    "mode": 1
  }
]
```

# sequence_versions

Sequence versions are created when a sequence is published for sharing. Also see [featured sequences](#featured_sequences).

|Method|Description|
|---|---|
|`GET` /api/sequence_versions/:id|Get a sequence version.|

|Field|Type|`GET`|`GET/:id`|`POST`|`PATCH`|`DELETE`|
|---|---|:---:|:---:|:---:|:---:|:---:|
|`id`<br>Unique identifier set by the database.|integer||📖||||
|`created_at`<br>Date and time of creation set by the database.|timestamp||📖||||
|`description`<br>Sequence description.|string||📖||||
|`copyright`<br>Copyright holder.|string||📖||||
|`name`<br>Sequence name.|string||📖||||
|`color`<br>Sequence color.|"blue" \| "green" \| "yellow" \| "orange" \| "purple" \| "pink" \| "gray" \| "red"||📖||||
|`kind`<br>"sequence".|"sequence"||📖||||
|`args`<br>Scope declaration.|Object||📖||||
|`body`<br>Sequence steps.|Array||📖||||

__GET /api/sequence_versions/8__
```python
import json
import requests

# TOKEN = ...

url = f'https:{TOKEN['token']['unencoded']['iss']}/api/sequence_versions/8'
headers = {'Authorization': 'Bearer ' + TOKEN['token']['encoded'],
           'content-type': 'application/json'}
response = requests.get(url, headers=headers)
print(json.dumps(response.json(), indent=2))
```
output:
```json
{
  "id": 8,
  "created_at": "2022-02-02T23:14:33.054Z",
  "description": "An SV with comments",
  "copyright": "FarmBot, Inc. 2021",
  "name": "Operative multimedia success",
  "kind": "sequence",
  "args": {
    "version": 20180209,
    "locals": {
      "kind": "scope_declaration",
      "args": {
      }
    }
  },
  "body": [
    {
      "comment": "This is a comment",
      "kind": "send_message",
      "args": {
        "message": "Hello, world!",
        "message_type": "warn"
      }
    }
  ]
}
```

# sequences

See [sequences](https://software.farm.bot/docs/sequences).

|Method|Description|
|---|---|
|`GET` /api/sequences|Get an array of all sequences.|
|`GET` /api/sequences/:id|Get a single sequence by id.|
|`POST` /api/sequences|Create a new sequence.|
|`PATCH` /api/sequences/:id|Edit a single sequence by id.|
|`DELETE` /api/sequences/:id|Delete a single sequence by id.|

|Field|Type|`GET`|`GET/:id`|`POST`|`PATCH`|`DELETE`|
|---|---|:---:|:---:|:---:|:---:|:---:|
|`id`<br>Unique identifier set by the database.|integer|📖|📖|||🗑|
|`created_at`<br>Date and time of creation set by the database.|timestamp|📖|📖|||🗑|
|`updated_at`<br>Date and time of most recent update set by the database.|timestamp|📖|📖|||🗑|
|`args`<br>Scope declaration.|Object|📖|📖|📝|📝<br>(required)|🗑|
|`color`<br>Sequence color.|"blue" \| "green" \| "yellow" \| "orange" \| "purple" \| "pink" \| "gray" \| "red"|📖|📖|📝|📝|🗑|
|`folder_id`<br>ID of the parent folder.|integer|📖|📖|📝|📝|🗑|
|`forked`<br>Local changes to a shared sequence.|boolean|📖|📖|📝|📝|🗑|
|`name`<br>Sequence name.|string|📖|📖|📝<br>(required)|📝<br>(required)|🗑|
|`pinned`<br>Add the sequence to the pinned sequence list.|boolean|📖|📖|📝|📝|🗑|
|`copyright`<br>Copyright holder.|string|📖|📖|📝|📝|🗑|
|`description`<br>Sequence description (markdown).|string|📖|📖|📝|📝|🗑|
|`sequence_versions`<br>A list of published versions of the sequence.|integer[]|📖|📖|📝|📝|🗑|
|`sequence_version_id`<br>ID of the sequence version the sequence was imported from.|integer|📖|📖|📝|📝|🗑|
|`kind`<br>"sequence"|"sequence"|📖|📖|📝|📝|🗑|
|`body`<br>Sequence steps.|Array|📖|📖|📝<br>(required)|📝<br>(required)|🗑|

__GET /api/sequences__
```python
import json
import requests

# TOKEN = ...

url = f'https:{TOKEN['token']['unencoded']['iss']}/api/sequences'
headers = {'Authorization': 'Bearer ' + TOKEN['token']['encoded'],
           'content-type': 'application/json'}
response = requests.get(url, headers=headers)
print(json.dumps(response.json(), indent=2))
```
output:
```json
[
  {
    "id": 36,
    "created_at": "2022-02-02T23:14:31.607Z",
    "updated_at": "2022-02-02T23:14:31.645Z",
    "args": {
      "version": 20180209,
      "locals": {
        "kind": "scope_declaration",
        "args": {
        },
        "body": [
          {
            "kind": "parameter_declaration",
            "args": {
              "label": "parent",
              "default_value": {
                "kind": "coordinate",
                "args": {
                  "x": 9,
                  "y": 9,
                  "z": 9
                }
              }
            }
          }
        ]
      }
    },
    "color": "green",
    "folder_id": null,
    "forked": false,
    "name": "My Sequence",
    "pinned": false,
    "copyright": null,
    "description": null,
    "sequence_versions": [

    ],
    "sequence_version_id": null,
    "kind": "sequence",
    "body": [
      {
        "kind": "execute",
        "args": {
          "sequence_id": 23
        }
      }
    ]
  }
]
```

## sequences/:id/upgrade/:sequence_version_id

|Method|Description|
|---|---|
|`POST` /api/sequences/:id/upgrade/:sequence_version_id|Upgrade a sequence that already uses a sequence version.|

## sequences/:sequence_version_id/install

|Method|Description|
|---|---|
|`POST` /api/sequences/:sequence_version_id/install|Install someone else's sequence.|

## sequences/:id/publish

|Method|Description|
|---|---|
|`POST` /api/sequences/:id/publish|Share your sequence with other people.|

|Field|Type|`GET`|`GET/:id`|`POST`|`PATCH`|`DELETE`|
|---|---|:---:|:---:|:---:|:---:|:---:|
|`copyright`<br>Copyright holder.|string|||📝<br>(required)|||

## sequences/:id/unpublish

|Method|Description|
|---|---|
|`POST` /api/sequences/:id/unpublish|Unlist your sequence.|

# storage_auth

Used for [photos](https://software.farm.bot/docs/photos).

|Method|Description|
|---|---|
|`GET` /api/storage_auth|Get the image storage policy object.|

__GET /api/storage_auth__
```python
import json
import requests

# TOKEN = ...

url = f'https:{TOKEN['token']['unencoded']['iss']}/api/storage_auth'
headers = {'Authorization': 'Bearer ' + TOKEN['token']['encoded'],
           'content-type': 'application/json'}
response = requests.get(url, headers=headers)
print(json.dumps(response.json(), indent=2))
```
output:
```json
{
  "verb": "POST",
  "url": "//storage.googleapis.com/YOU_MUST_CONFIG_GOOGLE_CLOUD_STORAGE/",
  "form_data": {
    "key": "temp1/517227e6-4d91-43c1-a0f2-69dd4dbf612c.jpg",
    "acl": "public-read",
    "Content-Type": "image/jpeg",
    "policy": "GCS NOT SETUP!",
    "signature": "GCS NOT SETUP!",
    "GoogleAccessId": "GCS NOT SETUP!",
    "file": "REPLACE_THIS_WITH_A_BINARY_JPEG_FILE"
  },
  "instructions": "Send a 'form-data' request to the URL provided. Then POST the resulting URL as an 'attachment_url' (json) to api/images/."
}
```

# telemetries

Used by [the history tab of the connectivity pop-up](https://software.farm.bot/docs/connectivity).

|Method|Description|
|---|---|
|`GET` /api/telemetries|Get an array of all telemetries.|
|`POST` /api/telemetries|Create a new telemetry.|
|`DELETE` /api/telemetries/:id|Delete a single telemetry by id.|
|`DELETE` /api/telemetries/all|Delete all telemetries.|

|Field|Type|`GET`|`GET/:id`|`POST`|`PATCH`|`DELETE`|
|---|---|:---:|:---:|:---:|:---:|:---:|
|`id`<br>Unique identifier set by the database.|integer|📖||||🗑|
|`created_at`<br>Date and time of creation set by the database.|timestamp|📖||||🗑|
|`updated_at`<br>Date and time of most recent update set by the database.|timestamp|📖||||🗑|
|`target`<br>FarmBot OS computer model.|"rpi" \| "rpi3" \| "rpi4"|📖||📝<br>(required)||🗑|
|`soc_temp`<br>CPU temperature.|integer|📖||📝||🗑|
|`throttled`<br>RPi throttle state.|"0x#####"|📖||📝||🗑|
|`wifi_level_percent`<br>WiFi signal strength percent.|0-100|📖||📝||🗑|
|`uptime`<br>Time in seconds since boot.|integer|📖||📝||🗑|
|`memory_usage`<br>Memory usage in MB.|integer|📖||📝||🗑|
|`disk_usage`<br>Disk usage in percent.|0-100|📖||📝||🗑|
|`cpu_usage`<br>CPU usage in percent.|0-100|📖||📝||🗑|
|`fbos_version`<br>FarmBot OS semver version string.|string|📖||📝||🗑|
|`firmware_hardware`<br>Firmware installed on the Farmduino or microcontroller.|"arduino" \| "farmduino" \| "farmduino_k14" \| "farmduino_k15" \| "farmduino_k16" \| "farmduino_k17" \| "express_k10" \| "express_k11" \| "express_k12"|📖||📝||🗑|

__GET /api/telemetries__
```python
import json
import requests

# TOKEN = ...

url = f'https:{TOKEN['token']['unencoded']['iss']}/api/telemetries'
headers = {'Authorization': 'Bearer ' + TOKEN['token']['encoded'],
           'content-type': 'application/json'}
response = requests.get(url, headers=headers)
print(json.dumps(response.json(), indent=2))
```
output:
```json
[
  {
    "id": 9,
    "created_at": 1712360174,
    "updated_at": "2024-04-05T23:36:14.413Z",
    "soc_temp": 62,
    "throttled": "0x0",
    "wifi_level_percent": 54,
    "uptime": 832,
    "memory_usage": 22,
    "disk_usage": 4,
    "cpu_usage": 61,
    "target": "rpi",
    "fbos_version": "17.0.0",
    "firmware_hardware": null
  }
]
```

# tokens

Used for user authentication. Also see [authorization](../../python/authorization.md).

|Method|Description|
|---|---|
|`GET` /api/tokens|Use your token to refresh your token, except for the expiration.|
|`POST` /api/tokens|Provide your account login to request a new token.|
|`DELETE` /api/tokens|Delete your token.|

|Field|Type|`GET`|`GET/:id`|`POST`|`PATCH`|`DELETE`|
|---|---|:---:|:---:|:---:|:---:|:---:|
|`token`<br>Token.|Object. (see below)|📖||📝||🗑|
|`user`<br>User.|Object. (see [users](#users))|||📝||🗑|

__Token__

|Field|Type|
|---|---|
|`unencoded`<br>Unencoded token information.|Object. (see below)|
|`encoded`<br>Encoded token to use in request header.|string|

__Unencoded Token__

|Field|Type|
|---|---|
|`aud`<br>Audience.|string|
|`sub`<br>User ID.|integer|
|`iat`<br>Created at timestamp.|integer|
|`jti`<br>JTI.|string|
|`iss`<br>API address.|string|
|`exp`<br>Expiration.|integer|
|`mqtt`<br>MQTT URL.|string|
|`bot`<br>Device ID string (username).|string|
|`vhost`<br>vhost.|string|
|`mqtt_ws`<br>MQTT WS URL.|string|

__GET /api/tokens__
```python
import json
import requests

# TOKEN = ...

url = f'https:{TOKEN['token']['unencoded']['iss']}/api/tokens'
headers = {'Authorization': 'Bearer ' + TOKEN['token']['encoded'],
           'content-type': 'application/json'}
response = requests.get(url, headers=headers)
print(json.dumps(response.json(), indent=2))
```
output:
```json
{
  "token": {
    "unencoded": {
      "aud": "unknown",
      "sub": 134,
      "iat": 1643843680,
      "jti": "22deacf3-cb7c-4b42-9727-24d4d964a9d2",
      "iss": "//192.168.1.112:3000",
      "exp": 1649027679,
      "mqtt": "blooper.io",
      "bot": "device_214",
      "vhost": "/",
      "mqtt_ws": "ws://blooper.io:3002/ws"
    },
    "encoded": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJhdWQiOiJ1bmtub3duIiwic3ViIjoxMzQsImlhdCI6MTY0Mzg0MzY4MCwianRpIjoiMjJkZWFjZjMtY2I3Yy00YjQyLTk3MjctMjRkNG"
  }
}
```

# tools

Used for [tools](https://software.farm.bot/docs/tools).

|Method|Description|
|---|---|
|`GET` /api/tools|Get an array of all tools.|
|`GET` /api/tools/:id|Get a single tool by id.|
|`POST` /api/tools|Create a new tool.|
|`PATCH` /api/tools/:id|Edit a single tool by id.|
|`DELETE` /api/tools/:id|Delete a single tool by id.|

|Field|Type|`GET`|`GET/:id`|`POST`|`PATCH`|`DELETE`|
|---|---|:---:|:---:|:---:|:---:|:---:|
|`id`<br>Unique identifier set by the database.|integer|📖|📖|||🗑|
|`created_at`<br>Date and time of creation set by the database.|timestamp|📖|📖|||🗑|
|`updated_at`<br>Date and time of most recent update set by the database.|timestamp|📖|📖|||🗑|
|`name`<br>Tool name.|string|📖|📖|📝<br>(required)|📝|🗑|
|`status`<br>Whether a tool is assigned to a slot or not. Does not indicate if a tool is currently mounted by the UTM. Use `device.mounted_tool_id` to check if the tool is mounted or not.|"active" \| "inactive"|📖|📖|||🗑|
|`flow_rate_ml_per_s`<br>Watering nozzle flow rate in mL per second. Field only shown in the frontend if tool name includes "Watering Nozzle".|integer|📖|📖|📝|📝|🗑|

__GET /api/tools__
```python
import json
import requests

# TOKEN = ...

url = f'https:{TOKEN['token']['unencoded']['iss']}/api/tools'
headers = {'Authorization': 'Bearer ' + TOKEN['token']['encoded'],
           'content-type': 'application/json'}
response = requests.get(url, headers=headers)
print(json.dumps(response.json(), indent=2))
```
output:
```json
{
  "id": 42,
  "created_at": "2022-02-02T23:14:39.322Z",
  "updated_at": "2022-02-02T23:14:39.322Z",
  "name": "Watering Nozzle",
  "status": "active",
  "flow_rate_ml_per_s": 0
}
```

# users

Account user information.

|Method|Description|
|---|---|
|`GET` /api/users|Get an array including the user object.|
|`POST` /api/users|Create a new user.|
|`PATCH` /api/users|Edit the user object.|
|`DELETE` /api/users|Delete the user object.|

|Field|Type|`GET`|`GET/:id`|`POST`|`PATCH`|`DELETE`|
|---|---|:---:|:---:|:---:|:---:|:---:|
|`id`<br>Unique identifier set by the database.|integer|📖||||🗑|
|`created_at`<br>Date and time of creation set by the database.|timestamp|📖||||🗑|
|`updated_at`<br>Date and time of most recent update set by the database.|timestamp|📖||||🗑|
|`name`<br>User name.|string|📖||📝<br>(required)|📝||
|`email`<br>Email address.|string|📖||📝<br>(required)|📝||
|`password`<br>Password.|string|||📝<br>(required)|||
|`password_confirmation`<br>Password.|string|||📝<br>(required)|||
|`new_password`<br>Password.|string|||||📝|
|`new_password_confirmation`<br>Password.|string|||||📝|
|`agree_to_terms`<br>Agreed to terms?.|boolean|||📝|||
|`language`<br>User language (used for [auto-generation](#ai)).|string|📖||📝|📝|🗑|

__GET /api/users__
```python
import json
import requests

# TOKEN = ...

url = f'https:{TOKEN['token']['unencoded']['iss']}/api/users'
headers = {'Authorization': 'Bearer ' + TOKEN['token']['encoded'],
           'content-type': 'application/json'}
response = requests.get(url, headers=headers)
print(json.dumps(response.json(), indent=2))
```
output:
```json
[
  {
    "id": 234,
    "created_at": "2022-02-02T23:14:56.988Z",
    "updated_at": "2022-02-02T23:14:56.988Z",
    "name": "Susana Bogan",
    "email": "suzy@hirthe.name",
  "language": "English"
  }
]
```

## users/control_certificate

|Method|Description|
|---|---|
|`POST` /api/users/control_certificate|Generate a control certificate.|

|Field|Type|`GET`|`GET/:id`|`POST`|`PATCH`|`DELETE`|
|---|---|:---:|:---:|:---:|:---:|:---:|
|`email`<br>Email address.|string|||📝<br>(required)|||
|`password`<br>Password.|string|||📝<br>(required)|||

## users/resend_verification

|Method|Description|
|---|---|
|`POST` /api/users/resend_verification|Resend the account verification email.|

|Field|Type|`GET`|`GET/:id`|`POST`|`PATCH`|`DELETE`|
|---|---|:---:|:---:|:---:|:---:|:---:|
|`email`<br>Email address.|string|||📝<br>(required)|||

# web_app_config

See [settings](https://software.farm.bot/docs/settings).

|Method|Description|
|---|---|
|`GET` /api/web_app_config|Get the web app config object.|
|`PATCH` /api/web_app_config|Edit the web app configuration object.|
|`DELETE` /api/web_app_config|Delete the web app configuration object.|

|Field|Type|`GET`|`GET/:id`|`POST`|`PATCH`|`DELETE`|
|---|---|:---:|:---:|:---:|:---:|:---:|
|`id`<br>Unique identifier set by the database.|integer|📖||||🗑|
|`device_id`<br>Unique device identifier set by the database.|integer|📖||||🗑|
|`created_at`<br>Date and time of creation set by the database.|timestamp|📖||||🗑|
|`updated_at`<br>Date and time of most recent update set by the database.|timestamp|📖||||🗑|
|`confirm_step_deletion`<br>Show a confirmation dialog when deleting a sequence step.|boolean|📖|||📝|🗑|
|`disable_animations`<br>Disable plant animations in the garden map.|boolean|📖|||📝|🗑|
|`disable_i18n`<br>Set the Web App to English.|boolean|📖|||📝|🗑|
|`display_trail`<br>Display a virtual trail for FarmBot in the garden map to show movement and watering history while the map is open. Toggling this setting will clear data for the current trail.|boolean|📖|||📝|🗑|
|`dynamic_map`<br>Change the garden map size based on axis length. A value must be input in AXIS LENGTH and STOP AT MAX must be enabled in `firmware_config`. Overrides MAP SIZE values.|boolean|📖|||📝|🗑|
|`encoder_figure`<br>Show a virtual farmbot in the garden map at the encoder position as well as motor position.|boolean|📖|||📝|🗑|
|`hide_webcam_widget`<br>Unused.|boolean|📖|||📝|🗑|
|`legend_menu_open`<br>Show the garden map legend.|boolean|📖|||📝|🗑|
|`raw_encoders`<br>Show raw encoder values.|boolean|📖|||📝|🗑|
|`scaled_encoders`<br>Show scaled encoder values.|boolean|📖|||📝|🗑|
|`show_spread`<br>Show plant spread in the garden map.|boolean|📖|||📝|🗑|
|`show_farmbot`<br>Show FarmBot in the garden map.|boolean|📖|||📝|🗑|
|`show_plants`<br>Show plants in the garden map.|boolean|📖|||📝|🗑|
|`show_points`<br>Show map points in the garden ma.|boolean|📖|||📝|🗑|
|`x_axis_inverted`<br>Invert x axis jog buttons.|boolean|📖|||📝|🗑|
|`y_axis_inverted`<br>Invert y axis jog buttons.|boolean|📖|||📝|🗑|
|`z_axis_inverted`<br>Invert z axis jog buttons.|boolean|📖|||📝|🗑|
|`bot_origin_quadrant`<br>Select a map origin by clicking on one of the four quadrants to adjust the garden map to your viewing angle.|1-4|📖|||📝|🗑|
|`zoom_level`<br>Garden map zoom level.|-9-3|📖|||📝|🗑|
|`success_log`<br>Success log verbosity setting.|0-3|📖|||📝|🗑|
|`busy_log`<br>Busy log verbosity setting.|0-3|📖|||📝|🗑|
|`warn_log`<br>Warning log verbosity setting.|0-3|📖|||📝|🗑|
|`error_log`<br>Error log verbosity setting.|0-3|📖|||📝|🗑|
|`info_log`<br>Info log verbosity setting.|0-3|📖|||📝|🗑|
|`fun_log`<br>Fun log verbosity setting.|0-3|📖|||📝|🗑|
|`debug_log`<br>Debug log verbosity setting.|0-3|📖|||📝|🗑|
|`stub_config`<br>Sub config.|boolean|📖|||📝|🗑|
|`show_first_party_farmware`<br>Unused.|boolean|📖|||📝|🗑|
|`enable_browser_speak`<br>Have the browser also read aloud log messages on the "Speak" channel that are spoken by FarmBot.|boolean|📖|||📝|🗑|
|`show_images`<br>Show photos in the garden map.|boolean|📖|||📝|🗑|
|`photo_filter_begin`<br>Show photos after this date and time.|timestamp \| null|📖|||📝|🗑|
|`photo_filter_end`<br>Show photos before this date and time.|timestamp \| null|📖|||📝|🗑|
|`discard_unsaved`<br>Don't ask about saving work before closing browser tab. Warning: may cause loss of data.|boolean|📖|||📝|🗑|
|`xy_swap`<br>Swap map X and Y axes, making the Y axis horizontal and X axis vertical. This setting will also swap the X and Y jog control buttons in the Move widget.|boolean|📖|||📝|🗑|
|`home_button_homing`<br>Configure the home button to find home instead of moving to home.|boolean|📖|||📝|🗑|
|`show_motor_plot`<br>Show motor position graph.|boolean|📖|||📝|🗑|
|`show_historic_points`<br>Show removed weeds in the garden map.|boolean|📖|||📝|🗑|
|`show_sensor_readings`<br>Show sensor readings in the garden map.|boolean|📖|||📝|🗑|
|`show_dev_menu`<br>Unused.|boolean|📖|||📝|🗑|
|`internal_use`<br>Developer setting storage.|string|📖|||📝|🗑|
|`time_format_24_hour`<br>Display times using the 24-hour format.|boolean|📖|||📝|🗑|
|`show_pins`<br>Show raw pin lists in Read Sensor, Control Peripheral, and If Statement steps.|boolean|📖|||📝|🗑|
|`disable_emergency_unlock_confirmation`<br>Don't confirm when unlocking FarmBot after an emergency stop.|boolean|📖|||📝|🗑|
|`map_size_x`<br>Custom x map dimension (in millimeters). These values set the size of the garden map unless `dynamic_map` is enabled.|integer|📖|||📝|🗑|
|`map_size_y`<br>Custom y map dimension (in millimeters). These values set the size of the garden map unless `dynamic_map` is enabled.|integer|📖|||📝|🗑|
|`expand_step_options`<br>Choose whether advanced step options are open or closed by default.|boolean|📖|||📝|🗑|
|`hide_sensors`<br>Hide the sensors panel.|boolean|📖|||📝|🗑|
|`confirm_plant_deletion`<br>Show a confirmation dialog when deleting a plant.|boolean|📖|||📝|🗑|
|`confirm_sequence_deletion`<br>Show a confirmation dialog when deleting a sequence.|boolean|📖|||📝|🗑|
|`discard_unsaved_sequences`<br>Don't ask about saving sequence work before closing browser tab. Warning: may cause loss of data.|boolean|📖|||📝|🗑|
|`user_interface_read_only_mode`<br>Disallow account data changes. This does not prevent Lua or FarmBot OS from changing settings.|boolean|📖|||📝|🗑|
|`assertion_log`<br>Assertion log verbosity setting.|0-3|📖|||📝|🗑|
|`show_zones`<br>Show point group location areas in the garden map.|boolean|📖|||📝|🗑|
|`show_weeds`<br>Show weeds in the garden map.|boolean|📖|||📝|🗑|
|`display_map_missed_steps`<br>Display high motor load warning indicators in map. Requires `display_trail` and stall detection to be enabled.|boolean|📖|||📝|🗑|
|`time_format_seconds`<br>Add seconds to time displays.|boolean|📖|||📝|🗑|
|`crop_images`<br>Crop images displayed in the garden map to remove black borders from image rotation. Crop amount determined by CAMERA ROTATION value.|boolean|📖|||📝|🗑|
|`show_camera_view_area`<br>Show the camera's field of view in the garden map.|boolean|📖|||📝|🗑|
|`view_celery_script`<br>View raw data representation of sequence steps.|boolean|📖|||📝|🗑|
|`highlight_modified_settings`<br>Highlight settings that have been changed from their default values.|boolean|📖|||📝|🗑|
|`show_advanced_settings`<br>Show advanced settings.|boolean|📖|||📝|🗑|
|`show_soil_interpolation_map`<br>Show soil height interpolation map in the garden map.|boolean|📖|||📝|🗑|
|`show_moisture_interpolation_map`<br>Show soil moisture interpolation map in the garden map.|boolean|📖|||📝|🗑|
|`clip_image_layer`<br>Remove portions of images that extend beyond the garden map boundaries.|boolean|📖|||📝|🗑|
|`beep_verbosity`<br>Beep upon log message verbosity level.|0-3|📖|||📝|🗑|
|`landing_page`<br>Panel to show upon loading the app.|string|📖|||📝|🗑|
|`go_button_axes`<br>Default axes to move when a GO TO LOCATION button is pressed.|"X" \| "Y" \| "Z" \| "XY" \| "XYZ"|📖|||📝|🗑|
|`show_uncropped_camera_view_area`<br>Show the camera's uncropped and unrotated field of view in the garden map when `clip_image_layer` is enabled.|boolean|📖|||📝|🗑|
|`default_plant_depth`<br>When adding plants to the map from the web app, set each new plant's depth to this value (in millimeters).|integer|📖|||📝|🗑|
|`show_missed_step_plot`<br>Show motor load graph.|boolean|📖|||📝|🗑|
|`enable_3d_electronics_box_top`<br>Show the push buttons in 3D instead of 2D.|boolean|📖|||📝|🗑|

__GET /api/web_app_config__
```python
import json
import requests

# TOKEN = ...

url = f'https:{TOKEN['token']['unencoded']['iss']}/api/web_app_config'
headers = {'Authorization': 'Bearer ' + TOKEN['token']['encoded'],
           'content-type': 'application/json'}
response = requests.get(url, headers=headers)
print(json.dumps(response.json(), indent=2))
```
output:
```json
{
  "id": 2,
  "created_at": "2022-02-02T23:14:24.408Z",
  "updated_at": "2022-02-02T23:14:24.426Z",
  "device_id": 86,
  "confirm_step_deletion": false,
  "disable_animations": false,
  "disable_i18n": false,
  "display_trail": true,
  "dynamic_map": false,
  "encoder_figure": false,
  "hide_webcam_widget": false,
  "legend_menu_open": true,
  "raw_encoders": false,
  "scaled_encoders": false,
  "show_spread": true,
  "show_farmbot": true,
  "show_plants": true,
  "show_points": true,
  "x_axis_inverted": false,
  "y_axis_inverted": false,
  "z_axis_inverted": false,
  "bot_origin_quadrant": 2,
  "zoom_level": -2,
  "success_log": 1,
  "busy_log": 1,
  "warn_log": 1,
  "error_log": 1,
  "info_log": 1,
  "fun_log": 1,
  "debug_log": 1,
  "stub_config": false,
  "show_first_party_farmware": false,
  "enable_browser_speak": false,
  "show_images": true,
  "photo_filter_begin": null,
  "photo_filter_end": null,
  "discard_unsaved": false,
  "xy_swap": false,
  "home_button_homing": true,
  "show_motor_plot": false,
  "show_historic_points": false,
  "show_sensor_readings": false,
  "show_dev_menu": false,
  "internal_use": null,
  "time_format_24_hour": false,
  "show_pins": false,
  "disable_emergency_unlock_confirmation": true,
  "map_size_x": 2900,
  "map_size_y": 1400,
  "expand_step_options": false,
  "hide_sensors": false,
  "confirm_plant_deletion": true,
  "confirm_sequence_deletion": true,
  "discard_unsaved_sequences": false,
  "user_interface_read_only_mode": false,
  "assertion_log": 1,
  "show_zones": false,
  "show_weeds": true,
  "display_map_missed_steps": false,
  "time_format_seconds": false,
  "crop_images": true,
  "show_camera_view_area": true,
  "view_celery_script": false,
  "highlight_modified_settings": true,
  "show_advanced_settings": false,
  "show_soil_interpolation_map": false,
  "show_moisture_interpolation_map": false,
  "clip_image_layer": true,
  "beep_verbosity": 0,
  "landing_page": "plants",
  "go_button_axes": "XY",
  "show_uncropped_camera_view_area": false,
  "default_plant_depth": 5,
  "show_missed_step_plot": false,
  "enable_3d_electronics_box_top": true
}
```

# webcam_feeds

See [webcam feeds](https://software.farm.bot/docs/webcam-feeds).

|Method|Description|
|---|---|
|`GET` /api/webcam_feeds|Get an array of all webcam feeds.|
|`GET` /api/webcam_feeds/:id|Get a single webcam feed by id.|
|`POST` /api/webcam_feeds|Create a new webcam feed.|
|`PATCH` /api/webcam_feeds/:id|Edit a single webcam feed by id.|
|`DELETE` /api/webcam_feeds/:id|Delete a single webcam feed by id.|

|Field|Type|`GET`|`GET/:id`|`POST`|`PATCH`|`DELETE`|
|---|---|:---:|:---:|:---:|:---:|:---:|
|`id`<br>Unique identifier set by the database.|integer|📖|📖|||🗑|
|`created_at`<br>Date and time of creation set by the database.|timestamp|📖|📖|||🗑|
|`updated_at`<br>Date and time of most recent update set by the database.|timestamp|📖|📖|||🗑|
|`name`<br>Webcam feed label.|string|📖|📖|📝<br>(required)|📝|🗑|
|`url`<br>Webcam feed URL.|string|📖|📖|📝<br>(required)|📝|🗑|

__GET /api/webcam_feeds__
```python
import json
import requests

# TOKEN = ...

url = f'https:{TOKEN['token']['unencoded']['iss']}/api/webcam_feeds'
headers = {'Authorization': 'Bearer ' + TOKEN['token']['encoded'],
           'content-type': 'application/json'}
response = requests.get(url, headers=headers)
print(json.dumps(response.json(), indent=2))
```
output:
```json
[
  {
    "id": 14,
    "created_at": "2022-02-02T23:14:53.317Z",
    "updated_at": "2022-02-02T23:14:53.317Z",
    "url": "0",
    "name": "feed 0"
  }
]
```

# wizard_step_results

Used by [setup wizard](https://my.farm.bot/app/designer/setup).

|Method|Description|
|---|---|
|`GET` /api/wizard_step_results|Get an array of all wizard step results.|
|`POST` /api/wizard_step_results|Create a new wizard step result.|
|`PATCH` /api/wizard_step_results/:id|Edit a single wizard step result by id.|
|`DELETE` /api/wizard_step_results/:id|Delete a single wizard step result by id.|

|Field|Type|`GET`|`GET/:id`|`POST`|`PATCH`|`DELETE`|
|---|---|:---:|:---:|:---:|:---:|:---:|
|`id`<br>Unique identifier set by the database.|integer|📖||||🗑|
|`created_at`<br>Date and time of creation set by the database.|timestamp|📖||||🗑|
|`updated_at`<br>Date and time of most recent update set by the database.|timestamp|📖||||🗑|
|`answer`<br>Wizard step success?|boolean|📖||📝|📝|🗑|
|`outcome`<br>Error message.|string|📖||📝|📝|🗑|
|`slug`<br>Wizard step UUID.|string|📖||📝|📝|🗑|

__GET /api/wizard_step_results__
```python
import json
import requests

# TOKEN = ...

url = f'https:{TOKEN['token']['unencoded']['iss']}/api/wizard_step_results'
headers = {'Authorization': 'Bearer ' + TOKEN['token']['encoded'],
           'content-type': 'application/json'}
response = requests.get(url, headers=headers)
print(json.dumps(response.json(), indent=2))
```
output:
```json
[
  {
    "id": 5,
    "created_at": "2022-02-02T23:15:34.279Z",
    "updated_at": "2022-02-02T23:15:34.279Z",
    "answer": false,
    "outcome": "error",
    "slug": "intro"
  }
]
```

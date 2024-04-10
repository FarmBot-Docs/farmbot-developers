---
title: "Example API requests"
slug: "api-docs"
---

The document that follows is a list of **example API requests**. It serves as a guide for developers who wish to see the schema and existence of particular API endpoints quickly.

# ai

|Field|Type|`GET`|`GET/:id`|`POST`|`PATCH`|`DELETE`|
|---|---|:---:|:---:|:---:|:---:|:---:|
|`prompt`<br>Instructions for model to follow.|string|⬜|⬜|✅|⬜|⬜|
|`context_key`<br>Type of generation request.|"title" \| "color" \| "description" \| "lua"|⬜|⬜|✅|⬜|⬜|
|`sequence_id`<br>For sequence "title", "color", and "description" auto-generation requests, the ID of the sequence to summarize.|integer \| null|⬜|⬜|✅|⬜|⬜|

## POST /api/ai
```json
{
  "prompt": "write code",
  "context_key": "lua",
  "sequence_id": null
}
```
# ai_feedbacks

|Field|Type|`GET`|`GET/:id`|`POST`|`PATCH`|`DELETE`|
|---|---|:---:|:---:|:---:|:---:|:---:|
|`id`<br>Unique identifier set by the database.|integer|⬜|⬜|❌|⬜|⬜|
|`created_at`<br>Date and time of creation set by the database.|timestamp|⬜|⬜|❌|⬜|⬜|
|`updated_at`<br>Date and time of most recent update set by the database.|timestamp|⬜|⬜|❌|⬜|⬜|
|`prompt`<br>A copy of the instructions for the auto-generation request.|string|⬜|⬜|✅|⬜|⬜|
|`reaction`<br>The feedback for the outcome of the prompt.|"good" \| "bad"|⬜|⬜|✅|⬜|⬜|

## POST /api/ai_feedbacks
```json
{
  "prompt": "write code",
  "reaction": "good"
}
```
# alerts

|Field|Type|`GET`|`GET/:id`|`POST`|`PATCH`|`DELETE`|
|---|---|:---:|:---:|:---:|:---:|:---:|
|`id`<br>Unique identifier set by the database.|integer|✅|⬜|⬜|⬜|✅|
|`created_at`<br>Date and time of creation set by the database.|timestamp|✅|⬜|⬜|⬜|✅|
|`updated_at`<br>Date and time of most recent update set by the database.|timestamp|✅|⬜|⬜|⬜|✅|
|`problem_tag`<br>Type of alert.|"api.seed_data.missing" \| "api.documentation.unread" \| "api.tour.not_taken" \| "api.user.not_welcomed" \| "api.bulletin.unread" \| "api.demo_account.in_use"|✅|⬜|⬜|⬜|✅|
|`slug`<br>Defaults to random UUID.|string|✅|⬜|⬜|⬜|✅|
|`priority`<br>Importance for sorting.|integer|✅|⬜|⬜|⬜|✅|

## GET /api/alerts
```json
[
  {
    "id": 1,
    "created_at": 1712360179,
    "updated_at": "2024-04-05T23:36:19.470Z",
    "priority": 100,
    "problem_tag": "api.documentation.unread",
    "slug": "720ca94b-eb4d-48c4-a53e-36978299e55e"
  }
]
```

# corpus

|Field|Type|`GET`|`GET/:id`|`POST`|`PATCH`|`DELETE`|
|---|---|:---:|:---:|:---:|:---:|:---:|
|*corpus*<br>Celery Script corpus.|object|✅|⬜|⬜|⬜|⬜|

## GET /api/corpus

# curves

|Field|Type|`GET`|`GET/:id`|`POST`|`PATCH`|`DELETE`|
|---|---|:---:|:---:|:---:|:---:|:---:|
|`id`<br>Unique identifier set by the database.|integer|✅|✅|❌|❌|✅|
|`created_at`<br>Date and time of creation set by the database.|timestamp|✅|✅|❌|❌|✅|
|`updated_at`<br>Date and time of most recent update set by the database.|timestamp|✅|✅|❌|❌|✅|
|`name`<br>Curve name.|string|✅|✅|✅(required)|✅|✅|
|`type`<br>Curve type.|"water" \| "spread" \| "height"|✅|✅|✅(required)|✅|✅|
|`data`<br>Curve data.|{[day: string]: value: integer}|✅|✅|✅(required)|✅|✅|

## GET /api/curves
## GET /api/curves/1
## DELETE /api/curves/1
## PATCH /api/curves/1
## POST /api/curves
```json
{
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
|`secret`<br>Password.|string|⬜|⬜|✅|⬜|⬜|
|`product_line`<br>FarmBot model.|"express_1.0" \| "express_1.1" \| "express_1.2" \| "express_xl_1.0" \| "express_xl_1.1" \| "express_xl_1.2" \| "genesis_1.2" \| "genesis_1.3" \| "genesis_1.4" \| "genesis_1.5" \| "genesis_1.6" \| "genesis_1.7" \| "genesis_xl_1.4" \| "genesis_xl_1.5" \| "genesis_xl_1.6" \| "genesis_xl_1.7" \| "none"|⬜|⬜|✅|⬜|⬜|

## POST /api/demo_account
```json
{
  "secret": "secret",
  "product_line": "genesis_1.7"
}
```

# device

|Field|Type|`GET`|`GET/:id`|`POST`|`PATCH`|`DELETE`|
|---|---|:---:|:---:|:---:|:---:|:---:|
|`id`<br>Unique identifier set by the database.|integer|✅|❌|❌|❌|✅|
|`created_at`<br>Date and time of creation set by the database.|timestamp|✅|❌|❌|❌|✅|
|`updated_at`<br>Date and time of most recent update set by the database.|timestamp|✅|❌|❌|❌|✅|
|`fb_order_number`<br>Order number.|string \| null|✅|❌|❌|✅|✅|
|`fbos_version`<br>FarmBot OS version.|string|✅|❌|❌|❌|✅|
|`indoor`<br>Is your FarmBot indoors?|boolean|✅|❌|✅|✅|✅|
|`last_saw_api`<br>Datetime of last API visit.|timestamp|✅|❌|❌|❌|✅|
|`lat`<br>Latitude.|float|✅|❌|✅|✅|✅|
|`lng`<br>Longitude.|float|✅|❌|✅|✅|✅|
|`mounted_tool_id`<br>The ID of the tool currently attached to the UTM.|integer|✅|❌|❌|✅|✅|
|`name`<br>FarmBot name.|string|✅|❌|✅|✅|✅|
|`ota_hour`<br>Over-the-air update local time.|0-23 \| null|✅|❌|❌|✅|✅|
|`ota_hour_utc`<br>Over-the-air update UTC time.|0-23 \| null|✅|❌|❌|❌|✅|
|`rpi`<br>FarmBot computer model.|"3" \| "4" \| "01" \| "02"|✅|❌|✅|✅|✅|
|`serial_number`<br>FarmBot serial number.|string|✅|❌|❌|❌|✅|
|`setup_completed_at`<br>Datetime device setup completed.|timestamp|✅|❌|❌|✅|✅|
|`throttled_at`<br>Datetime device throttle begin.|timestamp|✅|❌|❌|❌|✅|
|`throttled_until`<br>Datetime device throttle end.|timestamp|✅|❌|❌|❌|✅|
|`timezone`<br>Timezone.|string|✅|❌|✅|✅|✅|
|`max_log_age_in_days`<br>Logs deleted after __ days.|integer|✅|❌|❌|❌|✅|
|`max_sequence_count`<br>Maximum number of allowed sequences.|integer|✅|❌|❌|❌|✅|
|`max_sequence_length`<br>Maximum allowed sequence length.|integer|✅|❌|❌|❌|✅|
|`tz_offset_hrs`<br>Hours offset from UTC.|integer|✅|❌|❌|❌|✅|

## POST /api/device
## DELETE /api/device
## GET /api/device
```json
{
  "id": 1,
  "created_at": "2024-04-05T23:36:31.846Z",
  "updated_at": "2024-04-05T23:36:31.861Z",
  "fb_order_number": null,
  "fbos_version": "14.0.0",
  "indoor": false,
  "last_saw_api": null,
  "lat": null,
  "lng": null,
  "mounted_tool_id": null,
  "name": "FarmBot",
  "ota_hour_utc": 22,
  "ota_hour": 3,
  "rpi": null,
  "serial_number": "",
  "setup_completed_at": null,
  "throttled_at": null,
  "throttled_until": null,
  "timezone": "Asia/Ashgabat",
  "max_log_age_in_days": 0,
  "max_sequence_count": 0,
  "max_sequence_length": 0,
  "tz_offset_hrs": 5
}
```
## PATCH /api/device
## POST /api/device/reset
```json
{
  "password": "password"
}
```
## POST /api/device/seed
```json
{
  "product_line": "none"
}
```
## GET /api/device/sync
## POST /api/device

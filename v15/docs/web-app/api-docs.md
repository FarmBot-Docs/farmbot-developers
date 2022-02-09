---
title: "Example API requests"
slug: "api-docs"
description: "Example HTTP requests"
---

* toc
{:toc}

The document that follows is a list of example API requests. It serves as a guide for developers who wish to see the schema and existence of particular API endpoints quickly. The application's test suite generates this document automatically.

Many browsers offer a text search feature (usually via CTRL+F) that allows readers to search the document for relevant keywords.

#  GET /

**Response**

```
Empty Response
```

#  GET /api/alerts

**Response**

```
[
  {
    "id": 25,
    "created_at": 1643843681,
    "updated_at": "2022-02-02T23:14:41.694Z",
    "priority": 100,
    "problem_tag": "api.seed_data.missing",
    "slug": "fc07c4d5-aba0-4782-8c71-e443f88430e9"
  }
]
```

#  GET /api/alerts/26

**Response**

```
{
  "id": 26,
  "created_at": 1643843681,
  "updated_at": "2022-02-02T23:14:41.733Z",
  "priority": 100,
  "problem_tag": "api.seed_data.missing",
  "slug": "12f3517b-08d2-4745-a505-a3958045cdff"
}
```

#  GET /api/corpus

**Response**

```
{
  "version": 20180209,
  "enums": [
    {
      "name": "ALLOWED_AXIS",
      "allowed_values": [
        "x",
        "y",
        "z",
        "all"
      ]
    },
    {
      "name": "ALLOWED_SPECIAL_VALUE",
      "allowed_values": [
        "current_location",
        "safe_height",
        "soil_height"
      ]
    },
    {
      "name": "ALLOWED_CHANNEL_NAMES",
      "allowed_values": [
        "ticker",
        "toast",
        "email",
        "espeak"
      ]
    },
    {
      "name"
```

#  POST /api/demo_account

**Request**

```
{
  "secret": "gg0v7olg0mantxj9"
}
```

**Response**

```
{
}
```

#  GET /api/device

**Response**

```
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
  "serial_number": "0827898855f3f79e81037a4f3a119b00",
  "setup_completed_at": null,
  "throttled_at": null,
  "throttled_until": null,
  "timezone": "W-SU",
  "tz_offset_hrs": 3
}
```

#  DELETE /api/device

**Response**

```
Empty Response
```

#  GET /api/device

**Response**

```
{
  "id": 421,
  "created_at": "2022-02-02T23:15:35.803Z",
  "updated_at": "2022-02-02T23:15:35.803Z",
  "fb_order_number": null,
  "fbos_version": "17.0.0",
  "indoor": false,
  "last_saw_api": null,
  "lat": null,
  "lng": null,
  "mounted_tool_id": null,
  "name": "Fresh Chillies",
  "ota_hour_utc": 14,
  "ota_hour": 3,
  "serial_number": "41a2f640c051c4c2f49201c535bc3029",
  "setup_completed_at": null,
  "throttled_at": null,
  "throttled_until": null,
  "timezone": "Pacific/Ponape",
  "tz_o
```

#  POST /api/device

**Request**

```
{
  "user_id": 341,
  "name": "Squash"
}
```

**Response**

```
{
  "id": 496,
  "created_at": "2022-02-02T23:15:39.800Z",
  "updated_at": "2022-02-02T23:15:39.800Z",
  "fb_order_number": null,
  "fbos_version": null,
  "indoor": false,
  "last_saw_api": null,
  "lat": null,
  "lng": null,
  "mounted_tool_id": null,
  "name": "Squash",
  "ota_hour_utc": null,
  "ota_hour": null,
  "serial_number": null,
  "setup_completed_at": null,
  "throttled_at": null,
  "throttled_until": null,
  "timezone": null,
  "tz_offset_hrs": 0
}
```

#  POST /api/device

**Request**

```
{
  "user_id": 343
}
```

**Response**

```
{
  "id": 499,
  "created_at": "2022-02-02T23:15:39.888Z",
  "updated_at": "2022-02-02T23:15:39.888Z",
  "fb_order_number": null,
  "fbos_version": null,
  "indoor": false,
  "last_saw_api": null,
  "lat": null,
  "lng": null,
  "mounted_tool_id": null,
  "name": "FarmBot",
  "ota_hour_utc": null,
  "ota_hour": null,
  "serial_number": null,
  "setup_completed_at": null,
  "throttled_at": null,
  "throttled_until": null,
  "timezone": null,
  "tz_offset_hrs": 0
}
```

#  PUT /api/device

**Request**

```
{
  "id": 575,
  "mounted_tool_id": 0
}
```

**Response**

```
{
  "id": 575,
  "created_at": "2022-02-02T23:15:49.276Z",
  "updated_at": "2022-02-02T23:15:49.316Z",
  "fb_order_number": null,
  "fbos_version": "17.0.0",
  "indoor": false,
  "last_saw_api": null,
  "lat": null,
  "lng": null,
  "mounted_tool_id": null,
  "name": "Kale",
  "ota_hour_utc": 8,
  "ota_hour": 3,
  "serial_number": "a9b50d2969ed7da70781590364137a34",
  "setup_completed_at": null,
  "throttled_at": null,
  "throttled_until": null,
  "timezone": "Asia/Qyzylorda",
  "tz_offset_hrs":
```

#  PUT /api/device

**Request**

```
{
  "id": 579,
  "name": "Wendell Oberbrunner"
}
```

**Response**

```
{
  "id": 579,
  "created_at": "2022-02-02T23:15:49.431Z",
  "updated_at": "2022-02-02T23:15:49.456Z",
  "fb_order_number": null,
  "fbos_version": "17.0.0",
  "indoor": false,
  "last_saw_api": null,
  "lat": null,
  "lng": null,
  "mounted_tool_id": null,
  "name": "Wendell Oberbrunner",
  "ota_hour_utc": 7,
  "ota_hour": 3,
  "serial_number": "de6263b28eea01928ef7048bb3d92494",
  "setup_completed_at": null,
  "throttled_at": null,
  "throttled_until": null,
  "timezone": "Etc/GMT-4",
  "tz_of
```

#  PUT /api/device

**Request**

```
{
  "id": 580,
  "ota_hour": null
}
```

**Response**

```
{
  "id": 580,
  "created_at": "2022-02-02T23:15:49.478Z",
  "updated_at": "2022-02-02T23:15:49.502Z",
  "fb_order_number": null,
  "fbos_version": "17.0.0",
  "indoor": false,
  "last_saw_api": null,
  "lat": null,
  "lng": null,
  "mounted_tool_id": null,
  "name": "Cabbage",
  "ota_hour_utc": null,
  "ota_hour": null,
  "serial_number": "66f882edb5ced6c4f1a967fa60471296",
  "setup_completed_at": null,
  "throttled_at": null,
  "throttled_until": null,
  "timezone": "Mexico/BajaSur",
  "tz_off
```

#  PUT /api/device

**Request**

```
{
  "id": 581,
  "mounted_tool_id": 145
}
```

**Response**

```
{
  "id": 581,
  "created_at": "2022-02-02T23:15:49.526Z",
  "updated_at": "2022-02-02T23:15:49.558Z",
  "fb_order_number": null,
  "fbos_version": "17.0.0",
  "indoor": false,
  "last_saw_api": null,
  "lat": null,
  "lng": null,
  "mounted_tool_id": 145,
  "name": "Potatoes",
  "ota_hour_utc": 20,
  "ota_hour": 3,
  "serial_number": "972dea96d634d21c475571d213016bb6",
  "setup_completed_at": null,
  "throttled_at": null,
  "throttled_until": null,
  "timezone": "America/Boise",
  "tz_offset_hr
```

#  PUT /api/device

**Request**

```
{
  "id": 582,
  "timezone": "America/North_Dakota/Beulah"
}
```

**Response**

```
{
  "id": 582,
  "created_at": "2022-02-02T23:15:49.576Z",
  "updated_at": "2022-02-02T23:15:49.599Z",
  "fb_order_number": null,
  "fbos_version": "17.0.0",
  "indoor": false,
  "last_saw_api": null,
  "lat": null,
  "lng": null,
  "mounted_tool_id": null,
  "name": "Pumpkin",
  "ota_hour_utc": 21,
  "ota_hour": 3,
  "serial_number": "2bedb4073e6052bd98f4e10a3c7036a8",
  "setup_completed_at": null,
  "throttled_at": null,
  "throttled_until": null,
  "timezone": "America/North_Dakota/Beulah",

```

#  PUT /api/device

**Request**

```
{
  "id": 583,
  "ota_hour": 12
}
```

**Response**

```
{
  "id": 583,
  "created_at": "2022-02-02T23:15:49.618Z",
  "updated_at": "2022-02-02T23:15:49.641Z",
  "fb_order_number": null,
  "fbos_version": "17.0.0",
  "indoor": false,
  "last_saw_api": null,
  "lat": null,
  "lng": null,
  "mounted_tool_id": null,
  "name": "Capers",
  "ota_hour_utc": 15,
  "ota_hour": 12,
  "serial_number": "089ef3e448130b18e2eb048b593c64be",
  "setup_completed_at": null,
  "throttled_at": null,
  "throttled_until": null,
  "timezone": "Asia/Aden",
  "tz_offset_hrs":
```

#  POST /api/device/reset

**Request**

```
{
  "password": "password456"
}
```

**Response**

```
{
  "ok": "OK"
}
```

#  POST /api/device/seed

**Request**

```
{
  "product_line": "express_1.0"
}
```

**Response**

```
{
  "done": "Loading resources now."
}
```

#  POST /api/device/seed

**Request**

```
{
  "product_line": "none"
}
```

**Response**

```
{
  "done": "Loading resources now."
}
```

#  POST /api/device/seed

**Request**

```
{
  "product_line": "demo_account"
}
```

**Response**

```
{
  "done": "Loading resources now."
}
```

#  GET /api/device/sync

**Response**

```
{
  "devices": [
    [
      556,
      "2022-02-02T23:15:47.130Z"
    ]
  ],
  "farm_events": [
    [
      34,
      "2022-02-02T23:15:46.945Z"
    ]
  ],
  "farmware_envs": [
    [
      318,
      "2022-02-02T23:15:46.955Z"
    ]
  ],
  "farmware_installations": [
    [
      20,
      "2022-02-02T23:15:46.965Z"
    ]
  ],
  "peripherals": [
    [
      75,
      "2022-02-02T23:15:46.980Z"
    ]
  ],
  "pin_bindings": [
    [
      36,
      "2022-02-02T23:15:46.988Z"
    ]
  ],
  "points":
```

#  POST /api/export_data

**Response**

```
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
    "fbos_version": "17.0.0",
    "indoor": false,
    "last_saw_api": null,
    "lat": null,
    "lng": null,
    "mounted_tool_id": null,
    "name": "Swiss Chard",
    "ota_hour_utc": 22,
    "o
```

#  POST /api/export_data

**Response**

```
null
```

#  POST /api/farm_events

**Notes:** This is how you could create a FarmEvent that fires every 4 days.

**Request**

```
{
  "executable_id": 101,
  "executable_type": "Sequence",
  "start_time": "2022-02-02T23:15:46.627+00:00",
  "end_time": "2022-03-04T23:14:46.627+00:00",
  "repeat": 4,
  "time_unit": "daily"
}
```

**Response**

```
{
  "id": 18,
  "created_at": "2022-02-02T23:14:46.637Z",
  "updated_at": "2022-02-02T23:14:46.640Z",
  "start_time": "2022-02-02T23:15:46.627Z",
  "end_time": "2022-03-04T23:14:46.627Z",
  "repeat": 4,
  "time_unit": "daily",
  "executable_id": 101,
  "executable_type": "Sequence",
  "body": [

  ]
}
```

#  POST /api/farm_events

**Request**

```
{
  "start_time": "2022-02-03T00:14:12.982+00:00",
  "next_time": "2017-06-05T18:33:04.342Z",
  "time_unit": "never",
  "executable_id": 8,
  "executable_type": "Regimen",
  "end_time": "2017-06-05T18:34:00.000Z",
  "repeat": 1,
  "body": [
    {
      "kind": "parameter_application",
      "args": {
        "label": "wow",
        "data_value": {
          "kind": "tool",
          "args": {
            "tool_id": 44
          }
        }
      }
    }
  ]
}
```

**Response**

```
{
  "id": 20,
  "created_at": "2022-02-02T23:14:46.744Z",
  "updated_at": "2022-02-02T23:14:46.808Z",
  "start_time": "2022-02-03T00:14:12.982Z",
  "end_time": "2022-02-03T00:15:12.982Z",
  "repeat": 1,
  "time_unit": "never",
  "executable_id": 8,
  "executable_type": "Regimen",
  "body": [
    {
      "kind": "parameter_application",
      "args": {
        "label": "wow",
        "data_value": {
          "kind": "tool",
          "args": {
            "tool_id": 44
          }
        }

```

# (NOT OK) POST /api/farm_events

**Notes:** This is how you could create a FarmEvent that fires every 4 minutes.

**Request**

```
{
  "executable_id": 102,
  "executable_type": "Sequence",
  "start_time": "2022-02-02T23:15:46.922+00:00",
  "end_time": "2029-02-17T18:19:20.000Z",
  "repeat": 4,
  "time_unit": "minutely"
}
```

**Response**

```
{
  "occurrences": "Farm events can't have more than 500 occurrences (925846 occurrences detected)."
}
```

#  POST /api/farm_events

**Request**

```
{
  "end_time": "2022-02-02T23:14:47.059+00:00",
  "time_unit": "never",
  "executable_id": 103,
  "executable_type": "Sequence",
  "repeat": 1
}
```

**Response**

```
{
  "id": 21,
  "created_at": "2022-02-02T23:14:47.066Z",
  "updated_at": "2022-02-02T23:14:47.069Z",
  "start_time": "2022-02-02T23:14:06.931Z",
  "end_time": "2022-02-02T23:15:06.931Z",
  "repeat": 1,
  "time_unit": "never",
  "executable_id": 103,
  "executable_type": "Sequence",
  "body": [

  ]
}
```

#  POST /api/farm_events

**Request**

```
{
  "start_time": "2022-01-19T23:14:47.187+00:00",
  "time_unit": "never",
  "executable_id": 11,
  "executable_type": "Regimen",
  "end_time": "2017-06-05T18:34:00.000Z",
  "repeat": 1
}
```

**Response**

```
{
  "id": 22,
  "created_at": "2022-02-02T23:14:47.195Z",
  "updated_at": "2022-02-02T23:14:47.198Z",
  "start_time": "2022-01-19T23:14:47.187Z",
  "end_time": "2022-01-19T23:15:47.187Z",
  "repeat": 1,
  "time_unit": "never",
  "executable_id": 11,
  "executable_type": "Regimen",
  "body": [

  ]
}
```

#  GET /api/farm_events

**Response**

```
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

    ]
  }
]
```

#  GET /api/farm_events

**Response**

```
[
  {
    "id": 35,
    "created_at": "2022-02-02T23:15:47.370Z",
    "updated_at": "2022-02-02T23:15:47.370Z",
    "start_time": "2022-01-29T00:00:00.000Z",
    "end_time": "2024-02-02T23:15:47.312Z",
    "repeat": 10,
    "time_unit": "hourly",
    "executable_id": 251,
    "executable_type": "Sequence",
    "body": [

    ]
  },
  {
    "id": 36,
    "created_at": "2022-02-02T23:15:47.436Z",
    "updated_at": "2022-02-02T23:15:47.436Z",
    "start_time": "2022-01-28T00:00:00.000Z",
    "end_t
```

#  GET /api/farm_events

**Response**

```
[

]
```

#  PATCH /api/farm_events/11

**Request**

```
{
  "body": null
}
```

**Response**

```
{
  "id": 11,
  "created_at": "2022-02-02T23:14:43.985Z",
  "updated_at": "2022-02-02T23:14:44.052Z",
  "start_time": "2022-01-29T00:00:00.000Z",
  "end_time": "2022-02-04T00:01:00.000Z",
  "repeat": 5,
  "time_unit": "weekly",
  "executable_id": 94,
  "executable_type": "Sequence",
  "body": [
    {
      "kind": "parameter_application",
      "args": {
        "label": "foo",
        "data_value": {
          "kind": "coordinate",
          "args": {
            "x": 0,
            "y": 0,

```

#  PATCH /api/farm_events/12

**Request**

```
{
  "id": 12,
  "repeat": 1,
  "time_unit": "never"
}
```

**Response**

```
{
  "id": 12,
  "created_at": "2022-02-02T23:14:44.177Z",
  "updated_at": "2022-02-02T23:14:44.196Z",
  "start_time": "2022-01-29T00:00:00.000Z",
  "end_time": "2022-01-29T00:01:00.000Z",
  "repeat": 1,
  "time_unit": "never",
  "executable_id": 95,
  "executable_type": "Sequence",
  "body": [

  ]
}
```

#  PATCH /api/farm_events/13

**Request**

```
{
  "body": [
    {
      "kind": "parameter_application",
      "args": {
        "label": "bar",
        "data_value": {
          "kind": "coordinate",
          "args": {
            "x": 1,
            "y": 2,
            "z": 3
          }
        }
      }
    }
  ]
}
```

**Response**

```
{
  "id": 13,
  "created_at": "2022-02-02T23:14:44.280Z",
  "updated_at": "2022-02-02T23:14:44.351Z",
  "start_time": "2022-01-30T00:00:00.000Z",
  "end_time": "2022-02-04T00:01:00.000Z",
  "repeat": 10,
  "time_unit": "weekly",
  "executable_id": 96,
  "executable_type": "Sequence",
  "body": [
    {
      "kind": "parameter_application",
      "args": {
        "label": "bar",
        "data_value": {
          "kind": "coordinate",
          "args": {
            "x": 1,
            "y": 2,

```

#  DELETE /api/farm_events/31

**Response**

```
Empty Response
```

#  GET /api/farm_events/6

**Response**

```
{
  "id": 6,
  "created_at": "2022-02-02T23:14:41.866Z",
  "updated_at": "2022-02-02T23:14:41.866Z",
  "start_time": "2022-01-28T00:00:00.000Z",
  "end_time": "2024-02-02T23:14:41.801Z",
  "repeat": 10,
  "time_unit": "daily",
  "executable_id": 86,
  "executable_type": "Sequence",
  "body": [

  ]
}
```

#  PATCH /api/farm_events/8

**Request**

```
{
  "id": 8,
  "farm_event": {
    "repeat": 66
  }
}
```

**Response**

```
{
  "id": 8,
  "created_at": "2022-02-02T23:14:43.591Z",
  "updated_at": "2022-02-02T23:14:43.610Z",
  "start_time": "2022-01-29T00:00:00.000Z",
  "end_time": "2022-02-07T00:01:00.000Z",
  "repeat": 7,
  "time_unit": "weekly",
  "executable_id": 91,
  "executable_type": "Sequence",
  "body": [

  ]
}
```

#  PATCH /api/farm_events/9

**Request**

```
{
  "body": [

  ]
}
```

**Response**

```
{
  "id": 9,
  "created_at": "2022-02-02T23:14:43.696Z",
  "updated_at": "2022-02-02T23:14:43.809Z",
  "start_time": "2022-01-28T00:00:00.000Z",
  "end_time": "2022-02-07T00:01:00.000Z",
  "repeat": 7,
  "time_unit": "hourly",
  "executable_id": 92,
  "executable_type": "Sequence",
  "body": [

  ]
}
```

#  POST /api/farmware_envs

**Request**

```
{
  "key": "Coffee Emoji",
  "value": "☕"
}
```

**Response**

```
{
  "id": 9,
  "device_id": 293,
  "key": "Coffee Emoji",
  "value": "☕",
  "created_at": "2022-02-02T23:14:50.566Z",
  "updated_at": "2022-02-02T23:14:50.566Z"
}
```

#  POST /api/farmware_envs

**Request**

```
{
  "key": "compund_data",
  "value": {
    "x": "y",
    "z": 300
  }
}
```

**Response**

```
{
  "id": 10,
  "device_id": 294,
  "key": "compund_data",
  "value": {
    "x": "y",
    "z": 300
  },
  "created_at": "2022-02-02T23:14:50.610Z",
  "updated_at": "2022-02-02T23:14:50.610Z"
}
```

#  GET /api/farmware_envs

**Response**

```
[
  {
    "id": 11,
    "device_id": 295,
    "key": "Stun Sporeda56",
    "value": "Wrap",
    "created_at": "2022-02-02T23:14:50.641Z",
    "updated_at": "2022-02-02T23:14:50.641Z"
  },
  {
    "id": 12,
    "device_id": 295,
    "key": "Supersonic0959",
    "value": "Flash",
    "created_at": "2022-02-02T23:14:50.650Z",
    "updated_at": "2022-02-02T23:14:50.650Z"
  },
  {
    "id": 13,
    "device_id": 295,
    "key": "Guillotineee35",
    "value": "Poison Gas",
    "created_at": "2022-02-02
```

#  DELETE /api/farmware_envs/316

**Response**

```
Empty Response
```

#  GET /api/farmware_envs/317

**Response**

```
{
  "id": 317,
  "device_id": 298,
  "key": "Fire Blast559f",
  "value": "Fury Attack",
  "created_at": "2022-02-02T23:14:53.281Z",
  "updated_at": "2022-02-02T23:14:53.281Z"
}
```

#  PUT /api/farmware_envs/8

**Request**

```
{
  "key": "20e8ytiligA",
  "value": "eralG"
}
```

**Response**

```
{
  "device_id": 292,
  "key": "20e8ytiligA",
  "value": "eralG",
  "id": 8,
  "created_at": "2022-02-02T23:14:50.511Z",
  "updated_at": "2022-02-02T23:14:50.528Z"
}
```

#  DELETE /api/farmware_envs/all

**Response**

```
Empty Response
```

#  GET /api/farmware_installations

**Response**

```
[
  {
    "id": 2,
    "created_at": "2022-02-02T23:14:17.940Z",
    "updated_at": "2022-02-02T23:14:17.940Z",
    "url": "http://auer.co/angel/manifest.json",
    "package": null,
    "package_error": null
  },
  {
    "id": 3,
    "created_at": "2022-02-02T23:14:17.951Z",
    "updated_at": "2022-02-02T23:14:17.951Z",
    "url": "http://mcclure-hessel.co/theron/manifest.json",
    "package": null,
    "package_error": null
  },
  {
    "id": 4,
    "created_at": "2022-02-02T23:14:17.960Z",

```

#  POST /api/farmware_installations

**Request**

```
{
  "url": "http://boyle-mosciski.io/dewitt/manifest.json"
}
```

**Response**

```
{
  "id": 5,
  "created_at": "2022-02-02T23:14:18.055Z",
  "updated_at": "2022-02-02T23:14:18.055Z",
  "url": "http://boyle-mosciski.io/dewitt/manifest.json",
  "package": null,
  "package_error": null
}
```

#  POST /api/farmware_installations/1/refresh

**Response**

```
{
  "id": 1,
  "created_at": "2022-02-02T23:14:17.880Z",
  "updated_at": "2022-02-02T23:14:17.880Z",
  "url": "http://abbott.com/kendra/manifest.json",
  "package": null,
  "package_error": null
}
```

#  DELETE /api/farmware_installations/6

**Response**

```
Empty Response
```

#  GET /api/farmware_installations/7

**Response**

```
{
  "id": 7,
  "created_at": "2022-02-02T23:14:18.170Z",
  "updated_at": "2022-02-02T23:14:18.170Z",
  "url": "http://quitzon-fay.co/octavio/manifest.json",
  "package": null,
  "package_error": null
}
```

#  GET /api/fbos_config

**Response**

```
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
  "upda
```

#  DELETE /api/fbos_config

**Response**

```
Empty Response
```

#  PUT /api/fbos_config

**Request**

```
{
  "device_id": 99
}
```

**Response**

```
{
  "id": 46,
  "created_at": "2022-02-02T23:15:36.708Z",
  "updated_at": "2022-02-02T23:15:36.708Z",
  "device_id": 449,
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
  "upda
```

#  PUT /api/fbos_config

**Request**

```
{
  "firmware_path": "null"
}
```

**Response**

```
{
  "id": 47,
  "created_at": "2022-02-02T23:15:36.747Z",
  "updated_at": "2022-02-02T23:15:36.759Z",
  "device_id": 450,
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
  "firmware_path": "null",
  "firmware_debug_log": false,
  "up
```

#  PUT /api/fbos_config

**Request**

```
{
  "blah_blah_blah": true
}
```

**Response**

```
{
  "id": 48,
  "created_at": "2022-02-02T23:15:36.794Z",
  "updated_at": "2022-02-02T23:15:36.794Z",
  "device_id": 451,
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
  "upda
```

#  PUT /api/fbos_config

**Request**

```
{
  "disable_factory_reset": false
}
```

**Response**

```
{
  "id": 50,
  "created_at": "2022-02-02T23:15:36.866Z",
  "updated_at": "2022-02-02T23:15:36.878Z",
  "device_id": 453,
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
  "upda
```

#  PUT /api/fbos_config

**Request**

```
{
  "updated_at": "2022-01-31T23:15:36.914Z",
  "network_not_found_timer": 20
}
```

**Response**

```
{
  "id": 51,
  "created_at": "2022-02-02T23:15:36.910Z",
  "updated_at": "2022-01-31T23:15:36.914Z",
  "device_id": 454,
  "disable_factory_reset": true,
  "firmware_input_log": false,
  "firmware_output_log": false,
  "sequence_body_log": false,
  "sequence_complete_log": false,
  "sequence_init_log": false,
  "network_not_found_timer": 20,
  "firmware_hardware": null,
  "os_auto_update": true,
  "arduino_debug_messages": false,
  "firmware_path": null,
  "firmware_debug_log": false,
  "update
```

#  GET /api/featured_sequences

**Response**

```
[
  {
    "id": 15,
    "path": "/app/shared/sequence/15",
    "name": "Down-sized intangible moratorium",
    "description": "foo,bar,baz"
  }
]
```

#  POST /api/feedback

**Request**

```
{
  "message": "Example message",
  "slug": "Example slug"
}
```

**Response**

```
{
}
```

#  GET /api/firmware_config

**Response**

```
{
  "id": 7,
  "created_at": "2022-02-02T23:14:50.199Z",
  "updated_at": "2022-02-02T23:14:50.199Z",
  "device_id": 287,
  "encoder_enabled_x": 0,
  "encoder_enabled_y": 0,
  "encoder_enabled_z": 0,
  "encoder_invert_x": 0,
  "encoder_invert_y": 0,
  "encoder_invert_z": 0,
  "encoder_missed_steps_decay_x": 5,
  "encoder_missed_steps_decay_y": 5,
  "encoder_missed_steps_decay_z": 5,
  "encoder_missed_steps_max_x": 5,
  "encoder_missed_steps_max_y": 5,
  "encoder_missed_steps_max_z": 5,
  "encoder
```

#  DELETE /api/firmware_config

**Response**

```
Empty Response
```

#  PUT /api/firmware_config

**Request**

```
{
  "device_id": 99
}
```

**Response**

```
{
  "id": 10,
  "created_at": "2022-02-02T23:14:50.311Z",
  "updated_at": "2022-02-02T23:14:50.311Z",
  "device_id": 289,
  "encoder_enabled_x": 0,
  "encoder_enabled_y": 0,
  "encoder_enabled_z": 0,
  "encoder_invert_x": 0,
  "encoder_invert_y": 0,
  "encoder_invert_z": 0,
  "encoder_missed_steps_decay_x": 5,
  "encoder_missed_steps_decay_y": 5,
  "encoder_missed_steps_decay_z": 5,
  "encoder_missed_steps_max_x": 5,
  "encoder_missed_steps_max_y": 5,
  "encoder_missed_steps_max_z": 5,
  "encode
```

#  PUT /api/firmware_config

**Request**

```
{
  "pin_guard_5_time_out": 23,
  "firmware_debug_log": true,
  "firmware_input_log": true,
  "firmware_output_log": true
}
```

**Response**

```
{
  "id": 11,
  "created_at": "2022-02-02T23:14:50.360Z",
  "updated_at": "2022-02-02T23:14:50.377Z",
  "device_id": 290,
  "encoder_enabled_x": 0,
  "encoder_enabled_y": 0,
  "encoder_enabled_z": 0,
  "encoder_invert_x": 0,
  "encoder_invert_y": 0,
  "encoder_invert_z": 0,
  "encoder_missed_steps_decay_x": 5,
  "encoder_missed_steps_decay_y": 5,
  "encoder_missed_steps_decay_z": 5,
  "encoder_missed_steps_max_x": 5,
  "encoder_missed_steps_max_y": 5,
  "encoder_missed_steps_max_z": 5,
  "encode
```

#  GET /api/first_party_farmwares

**Response**

```
[
  {
    "id": 1,
    "created_at": "2019-08-14 18:33:08.428306",
    "updated_at": "2019-08-14 18:33:08.428306",
    "url": "https://raw.githubusercontent.com/FarmBot-Labs/farmware_manifests/main/packages/take-photo/manifest_v2.json",
    "package": "take-photo",
    "package_error": null
  },
  {
    "id": 2,
    "created_at": "2019-08-14 18:33:08.428306",
    "updated_at": "2019-08-14 18:33:08.428306",
    "url": "https://raw.githubusercontent.com/FarmBot-Labs/farmware_manifests/main/package
```

#  GET /api/first_party_farmwares/2

**Response**

```
{
  "id": 2,
  "created_at": "2019-08-14 18:33:08.428306",
  "updated_at": "2019-08-14 18:33:08.428306",
  "url": "https://raw.githubusercontent.com/FarmBot-Labs/farmware_manifests/main/packages/camera-calibration/manifest_v2.json",
  "package": "camera-calibration",
  "package_error": null
}
```

#  POST /api/folders

**Request**

```
{
  "parent_id": 14,
  "color": "blue",
  "name": "child"
}
```

**Response**

```
{
  "id": 15,
  "created_at": "2022-02-02T23:15:35.556Z",
  "updated_at": "2022-02-02T23:15:35.556Z",
  "parent_id": 14,
  "color": "blue",
  "name": "child"
}
```

#  GET /api/folders

**Response**

```
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

#  PATCH /api/folders/10

**Request**

```
{
  "name": "C",
  "color": "red",
  "parent_id": null
}
```

**Response**

```
{
  "id": 10,
  "created_at": "2022-02-02T23:15:35.130Z",
  "updated_at": "2022-02-02T23:15:35.142Z",
  "parent_id": null,
  "color": "red",
  "name": "C"
}
```

#  GET /api/folders/11

**Response**

```
{
  "id": 11,
  "created_at": "2022-02-02T23:15:35.171Z",
  "updated_at": "2022-02-02T23:15:35.171Z",
  "parent_id": null,
  "color": "red",
  "name": "parent"
}
```

#  DELETE /api/folders/12

**Response**

```
Empty Response
```

#  GET /api/global_bulletins/Okra

**Response**

```
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

#  GET /api/global_config

**Response**

```
{
  "PING": "92c1b9a825243770bef23b9600cffb2d"
}
```

#  GET /api/global_config

**Response**

```
{
  "PING": "92c1b9a825243770bef23b9600cffb2d"
}
```

#  POST /api/images

**Request**

```
{
  "attachment_url": "https://cdn.shopify.com/s/files/1/2040/0289/files/FarmBot.io_Trimmed_Logo_Gray_on_Transparent_1_434x200.png?v=1525220371",
  "meta": {
    "x": 1,
    "z": 3
  }
}
```

**Response**

```
{
  "id": 6,
  "created_at": "2022-02-02T23:15:47.821Z",
  "updated_at": "2022-02-02T23:15:47.821Z",
  "device_id": 567,
  "attachment_processed_at": null,
  "attachment_url": "http://192.168.1.112:3000/placeholder_farmbot.jpg?text=Processing...",
  "meta": {
    "x": 1.0,
    "z": 3.0
  }
}
```

#  GET /api/images

**Response**

```
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

#  DELETE /api/images/7

**Response**

```
Empty Response
```

#  GET /api/images/8

**Response**

```
{
  "id": 8,
  "created_at": "2022-02-02T23:15:48.486Z",
  "updated_at": "2022-02-02T23:15:48.486Z",
  "device_id": 569,
  "attachment_processed_at": null,
  "attachment_url": "http://192.168.1.112:3000/placeholder_farmbot.jpg?text=Processing...",
  "meta": {
    "x": 1,
    "y": 2,
    "z": 3
  }
}
```

#  GET /api/logs

**Response**

```
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
  },
  {
    "id": 14,
    "created_at": 1643842974,
    "updated_at": "2022-02-02T23:14:54.428Z",
    "channels": [
      "toast"

```

#  GET /api/logs

**Response**

```
[
  {
    "id": 183,
    "created_at": 1643843695,
    "updated_at": "2022-02-02T23:14:55.587Z",
    "channels": [

    ],
    "message": null,
    "meta": null,
    "major_version": null,
    "minor_version": null,
    "patch_version": null,
    "type": "info",
    "verbosity": 1,
    "x": null,
    "y": null,
    "z": null
  },
  {
    "id": 182,
    "created_at": 1643843695,
    "updated_at": "2022-02-02T23:14:55.583Z",
    "channels": [

    ],
    "message": null,
    "meta": null,
    "maj
```

#  POST /api/logs

**Request**

```
{
  "message": "HELLO"
}
```

**Response**

```
{
  "id": 189,
  "created_at": 1643843695,
  "updated_at": "2022-02-02T23:14:55.682Z",
  "channels": [

  ],
  "message": "HELLO",
  "meta": null,
  "major_version": null,
  "minor_version": null,
  "patch_version": null,
  "type": "info",
  "verbosity": 1,
  "x": null,
  "y": null,
  "z": null
}
```

#  POST /api/logs

**Request**

```
{
  "channels": [

  ],
  "major_version": 8,
  "message": "HELLO",
  "minor_version": 4,
  "patch_version": 0,
  "type": "success",
  "verbosity": 1,
  "x": 0,
  "y": 0,
  "z": 0
}
```

**Response**

```
{
  "id": 195,
  "created_at": 1643843695,
  "updated_at": "2022-02-02T23:14:55.759Z",
  "channels": [

  ],
  "message": "HELLO",
  "meta": null,
  "major_version": 8,
  "minor_version": 4,
  "patch_version": 0,
  "type": "success",
  "verbosity": 1,
  "x": 0.0,
  "y": 0.0,
  "z": 0.0
}
```

#  POST /api/logs

**Request**

```
{
  "created_at": 1643709415,
  "meta": {
    "x": 1,
    "y": 2,
    "z": 3,
    "type": "info"
  },
  "channels": [
    "toast"
  ],
  "message": "Hello, world!"
}
```

**Response**

```
{
  "id": 201,
  "created_at": 1643709415,
  "updated_at": "2022-02-02T23:14:55.833Z",
  "channels": [
    "toast"
  ],
  "message": "Hello, world!",
  "meta": null,
  "major_version": null,
  "minor_version": null,
  "patch_version": null,
  "type": "info",
  "verbosity": 1,
  "x": null,
  "y": null,
  "z": null
}
```

#  POST /api/logs

**Request**

```
{
  "meta": {
    "x": 1,
    "y": 2,
    "z": 3,
    "type": "info"
  },
  "channels": [
    "fatal_email"
  ],
  "message": "KABOOOOMM - SYSTEM ERROR!"
}
```

**Response**

```
{
  "id": 223,
  "created_at": 1643843696,
  "updated_at": "2022-02-02T23:14:56.461Z",
  "channels": [
    "fatal_email"
  ],
  "message": "KABOOOOMM - SYSTEM ERROR!",
  "meta": null,
  "major_version": null,
  "minor_version": null,
  "patch_version": null,
  "type": "info",
  "verbosity": 1,
  "x": null,
  "y": null,
  "z": null
}
```

#  POST /api/logs

**Request**

```
{
  "channels": [

  ],
  "major_version": 8,
  "message": "HELLO",
  "minor_version": 4,
  "patch_version": 0,
  "type": "assertion",
  "verbosity": 1,
  "x": 0,
  "y": 0,
  "z": 0
}
```

**Response**

```
{
  "id": 229,
  "created_at": 1643843696,
  "updated_at": "2022-02-02T23:14:56.557Z",
  "channels": [

  ],
  "message": "HELLO",
  "meta": null,
  "major_version": 8,
  "minor_version": 4,
  "patch_version": 0,
  "type": "assertion",
  "verbosity": 1,
  "x": 0.0,
  "y": 0.0,
  "z": 0.0
}
```

#  DELETE /api/logs/123

**Notes:** WARNING: All logs will be deleted upon request, regardless of the specific log id provided.

**Response**

```
Empty Response
```

#  DELETE /api/logs/all

**Response**

```
Empty Response
```

#  GET /api/logs/search

**Request**

```
{
  "x": "-10"
}
```

**Response**

```
[
  {
    "id": 23,
    "created_at": 1643842434,
    "updated_at": "2022-02-02T23:14:54.546Z",
    "channels": [
      "toast"
    ],
    "message": "This is -10.0",
    "meta": null,
    "major_version": null,
    "minor_version": null,
    "patch_version": null,
    "type": "busy",
    "verbosity": 1,
    "x": -10.0,
    "y": 704.0,
    "z": 100.0
  }
]
```

#  GET /api/logs/search

**Response**

```
[
  {
    "id": 32,
    "created_at": 1643841894,
    "updated_at": "2022-02-02T23:14:54.660Z",
    "channels": [
      "toast"
    ],
    "message": "deliver virtual experiences",
    "meta": null,
    "major_version": null,
    "minor_version": null,
    "patch_version": null,
    "type": "success",
    "verbosity": 1,
    "x": -484.0,
    "y": 89.0,
    "z": 371.0
  },
  {
    "id": 33,
    "created_at": 1643841834,
    "updated_at": "2022-02-02T23:14:54.666Z",
    "channels": [
      "toast"
```

#  GET /api/logs/search

**Response**

```
[

]
```

#  PUT /api/password_resets

**Request**

```
{
  "password": "xpassword123",
  "password_confirmation": "xpassword123",
  "fbos_version": {
    "version": "999.9.9",
    "segments": null
  },
  "id": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJzdWIiOiJyYXVsLnRyZXV0ZWxAaG93ZS1tb3Jpc3NldHRlLmNvIiwiaWF0IjoxNjQzODQzNzQ1LCJqdGkiOiIyMWVjY2E5YS1iZDY5LTQ3NTEtOTZiMC1mMzJkMThhZGY4NTIiLCJpc3MiOiIvLzE5Mi4xNjguMS4xMTI6MzAwMCIsImV4cCI6MTY0MzkzMDE0NSwiYXVkIjoiUEFTU1dPUkRfUkVTRVRFUiJ9.FmLusmeBVNZp71zeW0d6eeLefLP26RVucJnGplnTDtytOvvZmm18bDZVwTmU8KXnCOSQaZM7Vv
```

**Response**

```
{
  "token": {
    "unencoded": {
      "aud": "unknown",
      "sub": 382,
      "iat": 1643843745,
      "jti": "affdcfef-889b-4aa0-a2fc-268654c065fa",
      "iss": "//192.168.1.112:3000",
      "exp": 1649027745,
      "mqtt": "blooper.io",
      "bot": "device_541",
      "vhost": "/",
      "mqtt_ws": "ws://blooper.io:3002/ws"
    },
    "encoded": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJhdWQiOiJ1bmtub3duIiwic3ViIjozODIsImlhdCI6MTY0Mzg0Mzc0NSwianRpIjoiYWZmZGNmZWYtODg5Yi00YWEwLWEyZmMtMjY4Nj
```

#  POST /api/password_resets

**Request**

```
{
  "email": "tad@gislason-wiza.org"
}
```

**Response**

```
{
  "status": "Check your email!"
}
```

#  GET /api/peripherals

**Response**

```
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

#  POST /api/peripherals

**Request**

```
{
  "pin": 13,
  "label": "LED"
}
```

**Response**

```
{
  "id": 74,
  "created_at": "2022-02-02T23:15:45.427Z",
  "updated_at": "2022-02-02T23:15:45.427Z",
  "pin": 13,
  "label": "LED",
  "mode": 0
}
```

#  GET /api/peripherals/12

**Response**

```
{
  "id": 12,
  "created_at": "2022-02-02T23:14:44.699Z",
  "updated_at": "2022-02-02T23:14:44.699Z",
  "pin": 6,
  "label": "MyString",
  "mode": 0
}
```

#  PATCH /api/peripherals/77

**Request**

```
{
  "pin": 9
}
```

**Response**

```
{
  "id": 77,
  "created_at": "2022-02-02T23:15:47.259Z",
  "updated_at": "2022-02-02T23:15:47.278Z",
  "pin": 9,
  "label": "MyString",
  "mode": 0
}
```

#  DELETE /api/peripherals/9

**Response**

```
{
  "id": 9,
  "created_at": "2022-02-02T23:14:38.975Z",
  "updated_at": "2022-02-02T23:14:38.975Z",
  "pin": 3,
  "label": "wow",
  "mode": 0
}
```

#  GET /api/pin_bindings

**Response**

```
[
  {
    "id": 46,
    "created_at": "2022-02-02T23:15:50.154Z",
    "updated_at": "2022-02-02T23:15:50.154Z",
    "device_id": 589,
    "sequence_id": null,
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
    "special_action": null,
    "pin_num": 1,
    "binding_type": "standard"
  },
  {
    "id": 48,

```

#  POST /api/pin_bindings

**Request**

```
{
  "pin_num": 4,
  "sequence_id": 262
}
```

**Response**

```
{
  "id": 52,
  "created_at": "2022-02-02T23:15:50.403Z",
  "updated_at": "2022-02-02T23:15:50.403Z",
  "device_id": 591,
  "sequence_id": 262,
  "special_action": null,
  "pin_num": 4,
  "binding_type": "standard"
}
```

#  GET /api/pin_bindings/37

**Response**

```
{
  "id": 37,
  "created_at": "2022-02-02T23:15:49.783Z",
  "updated_at": "2022-02-02T23:15:49.783Z",
  "device_id": 585,
  "sequence_id": null,
  "special_action": null,
  "pin_num": 5,
  "binding_type": "standard"
}
```

#  DELETE /api/pin_bindings/40

**Response**

```
Empty Response
```

#  PUT /api/pin_bindings/49

**Request**

```
{
  "pin_num": 0,
  "sequence_id": 261
}
```

**Response**

```
{
  "id": 49,
  "created_at": "2022-02-02T23:15:50.276Z",
  "updated_at": "2022-02-02T23:15:50.310Z",
  "device_id": 590,
  "sequence_id": 261,
  "special_action": null,
  "pin_num": 0,
  "binding_type": "standard"
}
```

#  GET /api/plant_templates

**Response**

```
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
  },
  {
    "id": 8,
    "saved_garden_id": 8,
    "device_id": 160,
    "radius": 1.5,
    "x": 548.0,
    "y": 324.0,
    "z": 234.0,
    "name": "untitled",
    "openfarm_slug": "lettuce",
    "created_at": "2022-02-
```

#  POST /api/plant_templates

**Request**

```
{
  "name": "Fresh Chillies",
  "saved_garden_id": 10,
  "x": 1,
  "y": 2,
  "z": 3,
  "openfarm_slug": "tomato",
  "radius": 32
}
```

**Response**

```
{
  "id": 10,
  "saved_garden_id": 10,
  "device_id": 161,
  "radius": 32.0,
  "x": 1.0,
  "y": 2.0,
  "z": 3.0,
  "name": "Fresh Chillies",
  "openfarm_slug": "tomato",
  "created_at": "2022-02-02T23:14:34.469Z",
  "updated_at": "2022-02-02T23:14:34.469Z"
}
```

#  PUT /api/plant_templates/1

**Request**

```
{
  "name": "Green Pepper",
  "x": 9,
  "y": 10,
  "z": 11,
  "openfarm_slug": "melon",
  "radius": 32
}
```

**Response**

```
{
  "device_id": 158,
  "radius": 32.0,
  "x": 9.0,
  "y": 10.0,
  "z": 11.0,
  "name": "Green Pepper",
  "openfarm_slug": "melon",
  "id": 1,
  "saved_garden_id": 1,
  "created_at": "2022-02-02T23:14:34.213Z",
  "updated_at": "2022-02-02T23:14:34.256Z"
}
```

#  DELETE /api/plant_templates/11

**Response**

```
Empty Response
```

#  PUT /api/plant_templates/4

**Request**

```
{
  "saved_garden_id": 5
}
```

**Response**

```
{
  "device_id": 159,
  "saved_garden_id": 5,
  "id": 4,
  "radius": 1.5,
  "x": 326.0,
  "y": 415.0,
  "z": 530.0,
  "name": "untitled",
  "openfarm_slug": "lettuce",
  "created_at": "2022-02-02T23:14:34.298Z",
  "updated_at": "2022-02-02T23:14:34.346Z"
}
```

#  POST /api/point_groups

**Request**

```
{
  "name": "this is a group",
  "point_ids": [
    7,
    8,
    9
  ]
}
```

**Response**

```
{
  "id": 3,
  "created_at": "2022-02-02T23:14:14.893Z",
  "updated_at": "2022-02-02T23:14:14.893Z",
  "name": "this is a group",
  "point_ids": [
    7,
    8,
    9
  ],
  "sort_type": "xy_ascending",
  "criteria": {
    "day": {
      "op": "<",
      "days_ago": 0
    },
    "string_eq": {
    },
    "number_eq": {
    },
    "number_lt": {
    },
    "number_gt": {
    }
  }
}
```

#  POST /api/point_groups

**Request**

```
{
  "name": "Criteria group",
  "point_ids": [
    10,
    11,
    12
  ],
  "criteria": {
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
    },
    "day": {
      "op": "<",
      "days_ago": 0
    }
  }
}
```

**Response**

```
{
  "id": 4,
  "created_at": "2022-02-02T23:14:14.995Z",
  "updated_at": "2022-02-02T23:14:14.995Z",
  "name": "Criteria group",
  "point_ids": [
    10,
    11,
    12
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
    "number
```

#  GET /api/point_groups

**Response**

```
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
      },
      "number_eq": {
      },
      "number_lt": {
      },
      "number_gt": {
      }
    }
  },
  {
    "id": 16,
    "created_at": "2022-02-02T23:14:32.593Z"
```

#  PUT /api/point_groups/1

**Request**

```
{
  "name": "new name",
  "point_ids": [
    4,
    5,
    6,
    2,
    3
  ]
}
```

**Response**

```
{
  "id": 1,
  "created_at": "2022-02-02T23:14:14.262Z",
  "updated_at": "2022-02-02T23:14:14.384Z",
  "name": "new name",
  "point_ids": [
    2,
    3,
    4,
    5,
    6
  ],
  "sort_type": "xy_ascending",
  "criteria": {
    "day": {
      "op": "<",
      "days_ago": 0
    },
    "string_eq": {
    },
    "number_eq": {
    },
    "number_lt": {
    },
    "number_gt": {
    }
  }
}
```

#  PUT /api/point_groups/2

**Request**

```
{
  "point_ids": [

  ],
  "criteria": {
    "string_eq": {
      "name": [
        "carrot"
      ]
    },
    "number_eq": {
      "x": [
        42,
        52,
        62
      ]
    },
    "number_lt": {
      "y": 8
    },
    "number_gt": {
      "z": 2
    },
    "day": {
      "op": ">",
      "days_ago": 10
    }
  }
}
```

**Response**

```
{
  "id": 2,
  "created_at": "2022-02-02T23:14:14.434Z",
  "updated_at": "2022-02-02T23:14:14.469Z",
  "name": "XYZ",
  "point_ids": [

  ],
  "sort_type": "xy_ascending",
  "criteria": {
    "day": {
      "op": ">",
      "days_ago": 10
    },
    "string_eq": {
      "name": [
        "carrot"
      ]
    },
    "number_eq": {
      "x": [
        42,
        52,
        62
      ]
    },
    "number_lt": {
      "y": 8
    },
    "number_gt": {
      "z": 2
    }
  }
}
```

#  DELETE /api/point_groups/25

**Response**

```
Empty Response
```

#  GET /api/point_groups/74

**Response**

```
{
  "id": 74,
  "created_at": "2022-02-02T23:15:38.537Z",
  "updated_at": "2022-02-02T23:15:38.537Z",
  "name": "PointGroups#show test",
  "point_ids": [

  ],
  "sort_type": "xy_ascending",
  "criteria": {
    "day": {
      "op": "<",
      "days_ago": 0
    },
    "string_eq": {
    },
    "number_eq": {
    },
    "number_lt": {
    },
    "number_gt": {
    }
  }
}
```

#  GET /api/point_groups/75

**Response**

```
{
  "id": 75,
  "created_at": "2022-02-02T23:15:38.576Z",
  "updated_at": "2022-02-02T23:15:38.576Z",
  "name": "x",
  "point_ids": [

  ],
  "sort_type": "xy_ascending",
  "criteria": {
    "day": {
      "op": "<",
      "days_ago": 0
    },
    "string_eq": {
    },
    "number_eq": {
    },
    "number_lt": {
    },
    "number_gt": {
    }
  }
}
```

#  GET /api/points

**Response**

```
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
    "radius": 50.0
  },
  {
    "id": 51,
    "created_at": "2022-02-02T23:14:25.971Z",
    "updated_at": "2022-02-02T23:14:25.971Z",
    "device_id
```

#  GET /api/points

**Notes:** If you want to see previously deleted points, add `?filter=old` to the end of the URL.

**Request**

```
{
  "filter": "old"
}
```

**Response**

```
[
  {
    "id": 53,
    "created_at": "2022-02-02T23:14:26.040Z",
    "updated_at": "2022-02-02T23:14:26.040Z",
    "device_id": 100,
    "name": "old",
    "pointer_type": "Plant",
    "meta": {
    },
    "x": 5,
    "y": 5,
    "z": 5,
    "openfarm_slug": "cabbage",
    "plant_stage": "planned",
    "planted_at": "2022-02-02T23:14:26.040Z",
    "radius": 50.0
  }
]
```

#  GET /api/points

**Notes:** If you want to see previously deleted points, add `?filter=old` to the end of the URL.

**Response**

```
[
  {
    "id": 57,
    "created_at": "2022-02-02T23:14:26.150Z",
    "updated_at": "2022-02-02T23:14:26.150Z",
    "device_id": 102,
    "name": "new",
    "pointer_type": "Plant",
    "meta": {
    },
    "x": 5,
    "y": 5,
    "z": 5,
    "openfarm_slug": "cabbage",
    "plant_stage": "planned",
    "planted_at": "2022-02-02T23:14:26.150Z",
    "radius": 50.0
  }
]
```

#  GET /api/points

**Response**

```
[
  {
    "id": 58,
    "created_at": "2022-02-02T23:14:26.216Z",
    "updated_at": "2022-02-02T23:14:26.216Z",
    "device_id": 103,
    "name": "untitled",
    "pointer_type": "GenericPointer",
    "meta": {
    },
    "x": 7.0,
    "y": 289.0,
    "z": 88.0,
    "radius": 1.5,
    "discarded_at": null
  }
]
```

#  GET /api/points

**Response**

```
[
  {
    "id": 59,
    "created_at": "2022-02-02T23:14:26.275Z",
    "updated_at": "2022-02-02T23:14:26.275Z",
    "device_id": 104,
    "name": "untitled",
    "pointer_type": "GenericPointer",
    "meta": {
    },
    "x": 375.0,
    "y": 59.0,
    "z": 332.0,
    "radius": 1.5,
    "discarded_at": null
  },
  {
    "id": 60,
    "created_at": "2022-02-02T23:14:26.282Z",
    "updated_at": "2022-02-02T23:14:26.282Z",
    "device_id": 104,
    "name": "untitled",
    "pointer_type": "GenericPoi
```

#  GET /api/points

**Response**

```
[
  {
    "id": 62,
    "created_at": "2022-02-02T23:14:26.397Z",
    "updated_at": "2022-02-02T23:14:26.397Z",
    "device_id": 105,
    "name": "My TS",
    "pointer_type": "ToolSlot",
    "meta": {
    },
    "x": 0.0,
    "y": 0.0,
    "z": 0.0,
    "tool_id": null,
    "pullout_direction": 0,
    "gantry_mounted": false
  }
]
```

#  GET /api/points

**Notes:** If you want to see previously deleted points alongside your active points, add `?filter=all` to the end of the URL.

**Request**

```
{
  "filter": "all"
}
```

**Response**

```
[
  {
    "id": 63,
    "created_at": "2022-02-02T23:14:26.451Z",
    "updated_at": "2022-02-02T23:14:26.451Z",
    "device_id": 106,
    "name": "old",
    "pointer_type": "Plant",
    "meta": {
    },
    "x": 5,
    "y": 5,
    "z": 5,
    "openfarm_slug": "cabbage",
    "plant_stage": "planned",
    "planted_at": "2022-02-02T23:14:26.451Z",
    "radius": 50.0
  },
  {
    "id": 64,
    "created_at": "2022-02-02T23:14:26.457Z",
    "updated_at": "2022-02-02T23:14:26.457Z",
    "device_id": 10
```

#  POST /api/points

**Request**

```
{
  "pointer_type": "ToolSlot",
  "name": "foo",
  "x": 0,
  "y": 0,
  "z": 0
}
```

**Response**

```
{
  "id": 194,
  "created_at": "2022-02-02T23:15:32.544Z",
  "updated_at": "2022-02-02T23:15:32.544Z",
  "device_id": 365,
  "name": "foo",
  "pointer_type": "ToolSlot",
  "meta": {
  },
  "x": 0.0,
  "y": 0.0,
  "z": 0.0,
  "tool_id": null,
  "pullout_direction": 0,
  "gantry_mounted": false
}
```

#  POST /api/points

**Request**

```
{
  "x": 1,
  "y": 2,
  "z": 3,
  "radius": 3,
  "name": "test weed",
  "pointer_type": "Weed",
  "meta": {
    "foo": "BAR"
  }
}
```

**Response**

```
{
  "id": 195,
  "created_at": "2022-02-02T23:15:32.585Z",
  "updated_at": "2022-02-02T23:15:32.585Z",
  "device_id": 366,
  "name": "test weed",
  "pointer_type": "Weed",
  "meta": {
    "foo": "BAR"
  },
  "x": 1.0,
  "y": 2.0,
  "z": 3.0,
  "radius": 3.0,
  "discarded_at": null,
  "plant_stage": "active"
}
```

# (NOT OK) POST /api/points

**Notes:** This is what happens when you post bad JSON

**Response**

```
{
  "error": "This is a JSON API. Please use a _valid_ JSON object or array. Validate JSON objects at https://jsonlint.com/"
}
```

#  POST /api/points

**Request**

```
{
  "x": 1,
  "y": 2,
  "z": 3,
  "radius": 3,
  "name": "YOLO",
  "pointer_type": "GenericPointer",
  "meta": {
    "foo": "BAR"
  }
}
```

**Response**

```
{
  "id": 196,
  "created_at": "2022-02-02T23:15:32.671Z",
  "updated_at": "2022-02-02T23:15:32.671Z",
  "device_id": 368,
  "name": "YOLO",
  "pointer_type": "GenericPointer",
  "meta": {
    "foo": "BAR"
  },
  "x": 1.0,
  "y": 2.0,
  "z": 3.0,
  "radius": 3.0,
  "discarded_at": null
}
```

#  POST /api/points

**Request**

```
{
  "pointer_type": "ToolSlot",
  "name": "foo",
  "x": 0,
  "y": 0,
  "z": 0,
  "pullout_direction": 1
}
```

**Response**

```
{
  "id": 197,
  "created_at": "2022-02-02T23:15:32.718Z",
  "updated_at": "2022-02-02T23:15:32.718Z",
  "device_id": 369,
  "name": "foo",
  "pointer_type": "ToolSlot",
  "meta": {
  },
  "x": 0.0,
  "y": 0.0,
  "z": 0.0,
  "tool_id": null,
  "pullout_direction": 1,
  "gantry_mounted": false
}
```

#  POST /api/points

**Request**

```
{
  "name": "Fooo",
  "x": 4,
  "y": 5,
  "z": 6,
  "pointer_type": "ToolSlot"
}
```

**Response**

```
{
  "id": 198,
  "created_at": "2022-02-02T23:15:32.791Z",
  "updated_at": "2022-02-02T23:15:32.791Z",
  "device_id": 371,
  "name": "Fooo",
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
```

#  POST /api/points

**Request**

```
{
  "x": 23,
  "y": 45,
  "pointer_type": "Weed"
}
```

**Response**

```
{
  "id": 199,
  "created_at": "2022-02-02T23:15:32.829Z",
  "updated_at": "2022-02-02T23:15:32.829Z",
  "device_id": 372,
  "name": "untitled",
  "pointer_type": "Weed",
  "meta": {
  },
  "x": 23.0,
  "y": 45.0,
  "z": 0.0,
  "radius": 25.0,
  "discarded_at": null,
  "plant_stage": "active"
}
```

#  POST /api/points

**Request**

```
{
  "x": 23,
  "y": 45,
  "name": "Put me in a salad",
  "pointer_type": "Plant",
  "openfarm_slug": "mung-bean",
  "planted_at": "\"2022-02-01T23:15:32.859+00:00\"",
  "plant_stage": "sprouted"
}
```

**Response**

```
{
  "id": 200,
  "created_at": "2022-02-01T23:15:32.859Z",
  "updated_at": "2022-02-02T23:15:32.868Z",
  "device_id": 373,
  "name": "Put me in a salad",
  "pointer_type": "Plant",
  "meta": {
  },
  "x": 23,
  "y": 45,
  "z": 0,
  "openfarm_slug": "mung-bean",
  "plant_stage": "sprouted",
  "planted_at": "2022-02-01T23:15:32.859Z",
  "radius": 25.0
}
```

#  PUT /api/points/233

**Request**

```
{
  "x": 99,
  "y": 87,
  "z": 33,
  "radius": 55,
  "meta": {
    "foo": "BAR"
  }
}
```

**Response**

```
{
  "id": 233,
  "created_at": "2022-02-02T23:15:45.141Z",
  "updated_at": "2022-02-02T23:15:45.169Z",
  "device_id": 534,
  "name": "untitled",
  "pointer_type": "GenericPointer",
  "meta": {
    "foo": "BAR"
  },
  "x": 99.0,
  "y": 87.0,
  "z": 33.0,
  "radius": 55.0,
  "discarded_at": null
}
```

#  PUT /api/points/235

**Request**

```
{
  "id": 235,
  "x": 23,
  "y": 45,
  "name": "My Lettuce",
  "openfarm_slug": "limestone-lettuce"
}
```

**Response**

```
{
  "id": 235,
  "created_at": "2022-02-02T23:15:45.211Z",
  "updated_at": "2022-02-02T23:15:45.229Z",
  "device_id": 535,
  "name": "My Lettuce",
  "pointer_type": "Plant",
  "meta": {
  },
  "x": 23,
  "y": 45,
  "z": 0,
  "openfarm_slug": "limestone-lettuce",
  "plant_stage": "planned",
  "planted_at": "2022-02-02T23:15:45.211Z",
  "radius": 1.0
}
```

#  PUT /api/points/239

**Request**

```
{
  "pullout_direction": 1
}
```

**Response**

```
{
  "id": 239,
  "created_at": "2022-02-02T23:15:45.327Z",
  "updated_at": "2022-02-02T23:15:45.342Z",
  "device_id": 537,
  "name": "untitled",
  "pointer_type": "ToolSlot",
  "meta": {
  },
  "x": 0.0,
  "y": 0.0,
  "z": 0.0,
  "tool_id": null,
  "pullout_direction": 1,
  "gantry_mounted": false
}
```

#  DELETE /api/points/245

**Response**

```
[
  {
    "id": 245,
    "created_at": "2022-02-02T23:15:48.571Z",
    "updated_at": "2022-02-02T23:15:48.571Z",
    "device_id": 571,
    "name": "untitled",
    "pointer_type": "GenericPointer",
    "meta": {
    },
    "x": 4.0,
    "y": 94.0,
    "z": 365.0,
    "radius": 1.5,
    "discarded_at": null
  }
]
```

#  DELETE /api/points/249,250,251,252,253,254

**Response**

```
[
  {
    "id": 249,
    "created_at": "2022-02-02T23:15:48.856Z",
    "updated_at": "2022-02-02T23:15:48.856Z",
    "device_id": 572,
    "name": "untitled",
    "pointer_type": "GenericPointer",
    "meta": {
    },
    "x": 512.0,
    "y": 527.0,
    "z": 200.0,
    "radius": 1.5,
    "discarded_at": null
  },
  {
    "id": 250,
    "created_at": "2022-02-02T23:15:48.863Z",
    "updated_at": "2022-02-02T23:15:48.863Z",
    "device_id": 572,
    "name": "untitled",
    "pointer_type": "Generic
```

#  DELETE /api/points/257

**Response**

```
[
  {
    "id": 257,
    "created_at": "2022-02-02T23:15:49.197Z",
    "updated_at": "2022-02-02T23:15:49.197Z",
    "device_id": 573,
    "name": "untitled",
    "pointer_type": "Plant",
    "meta": {
    },
    "x": 10,
    "y": 20,
    "z": 30,
    "openfarm_slug": "lettuce",
    "plant_stage": "planned",
    "planted_at": "2022-02-02T23:15:49.197Z",
    "radius": 1.0
  }
]
```

#  GET /api/points/98

**Response**

```
{
  "id": 98,
  "created_at": "2022-02-02T23:14:41.606Z",
  "updated_at": "2022-02-02T23:14:41.606Z",
  "device_id": 233,
  "name": "untitled",
  "pointer_type": "ToolSlot",
  "meta": {
  },
  "x": 0.0,
  "y": 0.0,
  "z": 0.0,
  "tool_id": null,
  "pullout_direction": 0,
  "gantry_mounted": false
}
```

#  GET /api/points/99

**Response**

```
{
  "id": 99,
  "created_at": "2022-02-02T23:14:41.646Z",
  "updated_at": "2022-02-02T23:14:41.654Z",
  "device_id": 234,
  "name": "untitled",
  "pointer_type": "GenericPointer",
  "meta": {
  },
  "x": 532.0,
  "y": 147.0,
  "z": 422.0,
  "radius": 1.5,
  "discarded_at": "2022-02-02T23:14:41.653Z"
}
```

#  POST /api/points/search

**Request**

```
{
  "created_by": "plant-detection"
}
```

**Response**

```
[

]
```

#  POST /api/points/search

**Request**

```
{
  "pointer_type": "Plant"
}
```

**Response**

```
[
  {
    "id": 219,
    "created_at": "2022-02-02T23:15:37.101Z",
    "updated_at": "2022-02-02T23:15:37.101Z",
    "device_id": 463,
    "name": "untitled",
    "pointer_type": "Plant",
    "meta": {
    },
    "x": 276,
    "y": 148,
    "z": 302,
    "openfarm_slug": "lettuce",
    "plant_stage": "planned",
    "planted_at": "2022-02-02T23:15:37.101Z",
    "radius": 1.5
  }
]
```

#  POST /api/points/search

**Request**

```
{
  "meta": {
    "foo1": 1
  }
}
```

**Response**

```
[
  {
    "id": 221,
    "created_at": "2022-02-02T23:15:37.144Z",
    "updated_at": "2022-02-02T23:15:37.144Z",
    "device_id": 465,
    "name": "untitled",
    "pointer_type": "GenericPointer",
    "meta": {
      "foo1": "1"
    },
    "x": 154.0,
    "y": 135.0,
    "z": 172.0,
    "radius": 1.5,
    "discarded_at": null
  }
]
```

#  POST /api/points/search

**Request**

```
{
  "x": 23
}
```

**Response**

```
[
  {
    "id": 223,
    "created_at": "2022-02-02T23:15:37.211Z",
    "updated_at": "2022-02-02T23:15:37.211Z",
    "device_id": 466,
    "name": "untitled",
    "pointer_type": "GenericPointer",
    "meta": {
    },
    "x": 23.0,
    "y": 135.0,
    "z": 255.0,
    "radius": 1.5,
    "discarded_at": null
  }
]
```

#  POST /api/points/search

**Request**

```
{
  "openfarm_slug": "tomato"
}
```

**Response**

```
[
  {
    "id": 225,
    "created_at": "2022-02-02T23:15:37.258Z",
    "updated_at": "2022-02-02T23:15:37.258Z",
    "device_id": 467,
    "name": "untitled",
    "pointer_type": "Plant",
    "meta": {
    },
    "x": 325,
    "y": 213,
    "z": 420,
    "openfarm_slug": "tomato",
    "plant_stage": "planned",
    "planted_at": "2022-02-02T23:15:37.258Z",
    "radius": 1.5
  }
]
```

#  POST /api/points/search

**Request**

```
{
  "plant_stage": "harvested"
}
```

**Response**

```
[
  {
    "id": 228,
    "created_at": "2022-02-02T23:15:37.306Z",
    "updated_at": "2022-02-02T23:15:37.306Z",
    "device_id": 468,
    "name": "untitled",
    "pointer_type": "Plant",
    "meta": {
    },
    "x": 458,
    "y": 410,
    "z": 549,
    "openfarm_slug": "lettuce",
    "plant_stage": "harvested",
    "planted_at": "2022-02-02T23:15:37.306Z",
    "radius": 1.5
  }
]
```

#  POST /api/points/search

**Request**

```
{
  "meta": {
    "created_by": "plant-detection"
  }
}
```

**Response**

```
[
  {
    "id": 229,
    "created_at": "2022-02-02T23:15:37.359Z",
    "updated_at": "2022-02-02T23:15:37.359Z",
    "device_id": 469,
    "name": "untitled",
    "pointer_type": "GenericPointer",
    "meta": {
      "created_by": "plant-detection"
    },
    "x": 83.0,
    "y": 47.0,
    "z": 101.0,
    "radius": 1.5,
    "discarded_at": null
  },
  {
    "id": 230,
    "created_at": "2022-02-02T23:15:37.366Z",
    "updated_at": "2022-02-02T23:15:37.366Z",
    "device_id": 469,
    "name": "unt
```

#  GET /api/public_key

**Response**

```
Empty Response
```

#  GET /api/regimens

**Response**

```
[
  {
    "id": 1,
    "created_at": "2022-02-02T23:14:14.521Z",
    "updated_at": "2022-02-02T23:14:14.521Z",
    "name": "f7430daddadd182f2384d60fea4d259a",
    "color": null,
    "device_id": 9,
    "body": [

    ],
    "regimen_items": [

    ]
  }
]
```

#  GET /api/regimens

**Response**

```
[

]
```

#  POST /api/regimens

**Request**

```
{
  "device": {
    "id": 595,
    "name": "Snowpea sprouts",
    "max_log_count": 1000,
    "max_images_count": 450,
    "timezone": "America/Sitka",
    "last_saw_api": null,
    "fbos_version": "17.0.0",
    "throttled_until": null,
    "throttled_at": null,
    "mounted_tool_id": null,
    "created_at": "2022-02-02T23:15:50.583Z",
    "updated_at": "2022-02-02T23:15:50.583Z",
    "serial_number": "2fded985e7666d47ce4b2d8b4b09a011",
    "mqtt_rate_limit_email_sent_at": null,
    "ota_hour": 3
```

**Response**

```
{
  "id": 31,
  "created_at": "2022-02-02T23:15:50.695Z",
  "updated_at": "2022-02-02T23:15:50.766Z",
  "name": "specs",
  "color": "red",
  "device_id": 594,
  "body": [
    {
      "kind": "parameter_declaration",
      "args": {
        "label": "parent",
        "default_value": {
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
      "id": 13,
      "created_at":
```

#  POST /api/regimens

**Request**

```
{
  "device": {
    "id": 600,
    "name": "Raspberry",
    "max_log_count": 1000,
    "max_images_count": 450,
    "timezone": "America/Santa_Isabel",
    "last_saw_api": null,
    "fbos_version": "17.0.0",
    "throttled_until": null,
    "throttled_at": null,
    "mounted_tool_id": null,
    "created_at": "2022-02-02T23:15:51.067Z",
    "updated_at": "2022-02-02T23:15:51.067Z",
    "serial_number": "d7b521e7d2eede5654192d34936849de",
    "mqtt_rate_limit_email_sent_at": null,
    "ota_hour":
```

**Response**

```
{
  "id": 33,
  "created_at": "2022-02-02T23:15:51.180Z",
  "updated_at": "2022-02-02T23:15:51.239Z",
  "name": "specs",
  "color": "red",
  "device_id": 599,
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
      "id": 15,
      "created_at": "2
```

#  POST /api/regimens

**Request**

```
{
  "name": "Arbok Flareon Nidoran",
  "color": "pink",
  "regimen_items": [
    {
      "time_offset": 123,
      "sequence_id": 268
    }
  ]
}
```

**Response**

```
{
  "id": 34,
  "created_at": "2022-02-02T23:15:51.370Z",
  "updated_at": "2022-02-02T23:15:51.374Z",
  "name": "Arbok Flareon Nidoran",
  "color": "pink",
  "device_id": 601,
  "body": [

  ],
  "regimen_items": [
    {
      "id": 16,
      "created_at": "2022-02-02T23:15:51.372Z",
      "updated_at": "2022-02-02T23:15:51.372Z",
      "regimen_id": 34,
      "sequence_id": 268,
      "time_offset": 123
    }
  ]
}
```

#  DELETE /api/regimens/15

**Response**

```
Empty Response
```

#  PUT /api/regimens/22

**Request**

```
{
  "id": 22,
  "name": "something new",
  "color": "blue",
  "body": [
    {
      "kind": "parameter_application",
      "args": {
        "label": "parent",
        "data_value": {
          "kind": "tool",
          "args": {
            "tool_id": 130
          }
        }
      }
    }
  ],
  "regimen_items": [
    {
      "time_offset": 950700000,
      "sequence_id": 218
    }
  ]
}
```

**Response**

```
{
  "id": 22,
  "created_at": "2022-02-02T23:15:37.914Z",
  "updated_at": "2022-02-02T23:15:38.133Z",
  "name": "something new",
  "color": "blue",
  "device_id": 476,
  "body": [
    {
      "kind": "parameter_application",
      "args": {
        "label": "parent",
        "data_value": {
          "kind": "tool",
          "args": {
            "tool_id": 130
          }
        }
      }
    }
  ],
  "regimen_items": [
    {
      "id": 6,
      "created_at": "2022-02-02T23:15:38.126Z",

```

#  PUT /api/regimens/24

**Request**

```
{
  "id": 24,
  "name": "something new",
  "color": "blue",
  "regimen_items": [
    {
      "time_offset": 1555500000,
      "sequence_id": 220
    },
    {
      "time_offset": 864300000,
      "sequence_id": 220
    },
    {
      "time_offset": 950700000,
      "sequence_id": 220
    }
  ]
}
```

**Response**

```
{
  "id": 24,
  "created_at": "2022-02-02T23:15:38.292Z",
  "updated_at": "2022-02-02T23:15:38.379Z",
  "name": "something new",
  "color": "blue",
  "device_id": 478,
  "body": [

  ],
  "regimen_items": [
    {
      "id": 7,
      "created_at": "2022-02-02T23:15:38.368Z",
      "updated_at": "2022-02-02T23:15:38.368Z",
      "regimen_id": 24,
      "sequence_id": 220,
      "time_offset": 1555500000
    },
    {
      "id": 8,
      "created_at": "2022-02-02T23:15:38.370Z",
      "updated_at"
```

#  GET /api/regimens/3

**Response**

```
{
  "id": 3,
  "created_at": "2022-02-02T23:14:24.710Z",
  "updated_at": "2022-02-02T23:14:24.710Z",
  "name": "895f4ec4c89acf4268429b0e75534acc",
  "color": null,
  "device_id": 91,
  "body": [

  ],
  "regimen_items": [

  ]
}
```

#  GET /api/releases

**Request**

```
{
  "channel": "stable",
  "platform": "rpi3"
}
```

**Response**

```
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

#  POST /api/rmq/resource

**Request**

```
{
  "password": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJhdWQiOiJ1bmtub3duIiwic3ViIjozNzAsImlhdCI6MTY0Mzg0Mzc0NCwianRpIjoiOWI4NGJiMWUtMmIwZC00ZjdkLWIwMjctMjI5ZDE0MDVjNzBmIiwiaXNzIjoiLy8xOTIuMTY4LjEuMTEyOjMwMDAiLCJleHAiOjE2NDkwMjc3NDQsIm1xdHQiOiJibG9vcGVyLmlvIiwiYm90IjoiZGV2aWNlXzUyOSIsInZob3N0IjoiLyIsIm1xdHRfd3MiOiJ3czovL2Jsb29wZXIuaW86MzAwMi93cyJ9.V34sM5eeZV1xxg5YKcNHQNxaby3pCpk7OYpPJF_SJxqxznM50-iXB0j8hr5AccylA9ALAT6rUnNkmAjpnG2VGULVeDL5TvFQZ6niy-ZF7rVt_0UpBF7g8uawoc1xtieLbJDMEES-KlpTPTObKCiVy
```

**Response**

```
Empty Response
```



#  POST /api/rmq/topic

**Request**

```
{
  "password": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJhdWQiOiJ1bmtub3duIiwic3ViIjozNjEsImlhdCI6MTY0Mzg0Mzc0MSwianRpIjoiM2Q0Y2UxNTMtZjM5Zi00ZTY3LWI2NmMtYjNhOWFkODEyMWExIiwiaXNzIjoiLy8xOTIuMTY4LjEuMTEyOjMwMDAiLCJleHAiOjE2NDkwMjc3NDEsIm1xdHQiOiJibG9vcGVyLmlvIiwiYm90IjoiZGV2aWNlXzUyMCIsInZob3N0IjoiLyIsIm1xdHRfd3MiOiJ3czovL2Jsb29wZXIuaW86MzAwMi93cyJ9.qli_fjLcxEmSAC46e7BZsTddFhaQdPkoYvuOdqnQrKvwYxbg4Vowo9euGW3oGvyn4-xXJShfmkPSR-swbILcYm3QGBxHmpzUaM3KgzHOw8_59JDNS8WeSZ-KmsbAYPzE-IdV00l3rF8smfhSzBNS0
```

**Response**

```
Empty Response
```





#  POST /api/rmq/topic

**Request**

```
{
  "password": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJhdWQiOiJ1bmtub3duIiwic3ViIjozNjQsImlhdCI6MTY0Mzg0Mzc0MiwianRpIjoiOWFhMjdjYzEtOWRmNC00MDE0LTgzNTktNGJiYjMxODViMGYwIiwiaXNzIjoiLy8xOTIuMTY4LjEuMTEyOjMwMDAiLCJleHAiOjE2NDkwMjc3NDIsIm1xdHQiOiJibG9vcGVyLmlvIiwiYm90IjoiZGV2aWNlXzUyMyIsInZob3N0IjoiLyIsIm1xdHRfd3MiOiJ3czovL2Jsb29wZXIuaW86MzAwMi93cyJ9.AMrhB-cDNVDyjrq1h5l9qU2Fpfh57AKlAxgDx_bzJYyQnEoSZLNWyit5o4Ztlk4sNTkfLE2H0y-KeyCXnqJzMDUvOr2QjYjjPpRbR6aad_1FN1DhK9V0b-hk4nmP8NpQy9jtG9h5Vnm6tooznRVV7
```

**Response**

```
Empty Response
```





#  POST /api/rmq/topic

**Request**

```
{
  "password": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJhdWQiOiJ1bmtub3duIiwic3ViIjozNjYsImlhdCI6MTY0Mzg0Mzc0MywianRpIjoiZmY0MDQ2ZDQtZDM2MC00NGM0LTkwYjYtNjc1MjdkMGRkYzFlIiwiaXNzIjoiLy8xOTIuMTY4LjEuMTEyOjMwMDAiLCJleHAiOjE2NDkwMjc3NDMsIm1xdHQiOiJibG9vcGVyLmlvIiwiYm90IjoiZGV2aWNlXzUyNSIsInZob3N0IjoiLyIsIm1xdHRfd3MiOiJ3czovL2Jsb29wZXIuaW86MzAwMi93cyJ9.A-_bcpwLnTTH-d-HdldeyJnXNM1W6SNaoodEa4Lv2bvx6XcxCVs_kunCTsIcx_hanItpIm9aNOplQ_acfD3_sRm39ey2sMQtVl_1AjOHdYOKp6oWMTttCMj2S4oJqzlz2ModXDHar-ESrSpMvm6uM
```

**Response**

```
Empty Response
```





#  POST /api/rmq/topic

**Request**

```
{
  "permission": "read",
  "routing_key": "demos.d3f91ygdrajxn8jk",
  "username": "farmbot_demo"
}
```

**Response**

```
Empty Response
```









#  POST /api/rmq/user

**Request**

```
{
  "password": "37161cedcd8d5d63",
  "username": "admin"
}
```

**Response**

```
Empty Response
```

#  POST /api/rmq/user

**Request**

```
{
  "password": "6pVmq37G0Urb5CBE",
  "username": "farmbot_demo"
}
```

**Response**

```
Empty Response
```

#  POST /api/rmq/user

**Request**

```
{
  "password": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJhdWQiOiJ1bmtub3duIiwic3ViIjozNjksImlhdCI6MTY0Mzg0Mzc0NCwianRpIjoiNjA1NmIxZGQtNTZiMy00OTcyLTlkNjgtZGI0YjJiZDBiYTZiIiwiaXNzIjoiLy8xOTIuMTY4LjEuMTEyOjMwMDAiLCJleHAiOjE2NDkwMjc3NDQsIm1xdHQiOiJibG9vcGVyLmlvIiwiYm90IjoiZGV2aWNlXzUyOCIsInZob3N0IjoiLyIsIm1xdHRfd3MiOiJ3czovL2Jsb29wZXIuaW86MzAwMi93cyJ9.wAIrB0yd_2eOOxXs9cDRcpdBzESPBK1UOzeifU3cZ-bIGA4T1JsSWLFkbe7NJ9qVpWsDwGJIDO3TUGA6_MSvdnJywsWYKZe8DWdYYvZHAoNiTd_POY3uc95Zhb9DJrJPvLU4Wo9CPVTEdcW0CYptK
```

**Response**

```
Empty Response
```

#  POST /api/rmq/user

**Request**

```
{
  "password": "37161cedcd8d5d63",
  "username": "admin"
}
```

**Response**

```
Empty Response
```

#  POST /api/rmq/vhost

**Request**

```
{
  "password": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJhdWQiOiJ1bmtub3duIiwic3ViIjozNjAsImlhdCI6MTY0Mzg0Mzc0MSwianRpIjoiNzU3Njg1ODMtOGM5ZS00OGUzLTg4YTUtNDJhMjM0MWYyZDk1IiwiaXNzIjoiLy8xOTIuMTY4LjEuMTEyOjMwMDAiLCJleHAiOjE2NDkwMjc3NDEsIm1xdHQiOiJibG9vcGVyLmlvIiwiYm90IjoiZGV2aWNlXzUxOSIsInZob3N0IjoiLyIsIm1xdHRfd3MiOiJ3czovL2Jsb29wZXIuaW86MzAwMi93cyJ9.XI_zV7NQ4LZoijautvBa1TPu55IoDv3ry5LDyCtcKZdJYKl3s00ewq_d2MJGUMIeR0lSfFrslcy-VJ2F27NCfflL6NioFiyHt01f4sySv8KSuXsqhA-7Sc8AkNsCkHvlSlZK0kVXhBcxiU7199i4f
```

**Response**

```
Empty Response
```

#  POST /api/saved_gardens

**Request**

```
{
  "name": "Kale"
}
```

**Response**

```
{
  "id": 31,
  "name": "Kale",
  "device_id": 383,
  "created_at": "2022-02-02T23:15:33.949Z",
  "updated_at": "2022-02-02T23:15:33.949Z"
}
```

#  GET /api/saved_gardens

**Response**

```
[
  {
    "id": 32,
    "name": "Andromeda",
    "device_id": 384,
    "created_at": "2022-02-02T23:15:33.978Z",
    "updated_at": "2022-02-02T23:15:33.978Z"
  },
  {
    "id": 33,
    "name": "Medea",
    "device_id": 384,
    "created_at": "2022-02-02T23:15:33.983Z",
    "updated_at": "2022-02-02T23:15:33.983Z"
  },
  {
    "id": 34,
    "name": "Arachne",
    "device_id": 384,
    "created_at": "2022-02-02T23:15:33.989Z",
    "updated_at": "2022-02-02T23:15:33.989Z"
  }
]
```

#  POST /api/saved_gardens/24/apply

**Response**

```
Empty Response
```

#  PATCH /api/saved_gardens/25/apply

**Response**

```
Empty Response
```

#  DELETE /api/saved_gardens/28

**Response**

```
Empty Response
```

#  PUT /api/saved_gardens/35

**Request**

```
{
  "name": "Onion"
}
```

**Response**

```
{
  "device_id": 385,
  "name": "Onion",
  "id": 35,
  "created_at": "2022-02-02T23:15:34.023Z",
  "updated_at": "2022-02-02T23:15:34.047Z"
}
```

#  POST /api/saved_gardens/snapshot

**Response**

```
Empty Response
```

#  GET /api/sensor_readings

**Response**

```
[
  {
    "id": 1,
    "created_at": "2022-02-02T23:14:15.819Z",
    "updated_at": "2022-02-02T23:14:15.819Z",
    "mode": 0,
    "pin": 166,
    "value": 80,
    "x": 281.0,
    "y": 205.0,
    "z": 76.0,
    "read_at": "2022-02-02T23:14:15.819Z"
  }
]
```

#  GET /api/sensor_readings

**Request**

```
{
  "page": "2",
  "per": "5"
}
```

**Response**

```
[
  {
    "id": 26,
    "created_at": "2022-02-02T23:14:16.035Z",
    "updated_at": "2022-02-02T23:14:16.035Z",
    "mode": 0,
    "pin": 416,
    "value": 33,
    "x": 268.0,
    "y": 112.0,
    "z": 208.0,
    "read_at": "2022-02-02T23:14:16.035Z"
  },
  {
    "id": 25,
    "created_at": "2022-02-02T23:14:16.027Z",
    "updated_at": "2022-02-02T23:14:16.027Z",
    "mode": 0,
    "pin": 153,
    "value": 200,
    "x": 67.0,
    "y": 229.0,
    "z": 467.0,
    "read_at": "2022-02-02T23:14:16.027
```

#  POST /api/sensor_readings

**Request**

```
{
  "pin": 13,
  "value": 128,
  "x": null,
  "y": 1,
  "z": 2,
  "mode": 1,
  "read_at": "2022-02-02T18:14:16.115+00:00"
}
```

**Response**

```
{
  "id": 32,
  "created_at": "2022-02-02T23:14:16.124Z",
  "updated_at": "2022-02-02T23:14:16.124Z",
  "mode": 1,
  "pin": 13,
  "value": 128,
  "x": null,
  "y": 1.0,
  "z": 2.0,
  "read_at": "2022-02-02T18:14:16.115Z"
}
```

#  POST /api/sensor_readings

**Request**

```
{
  "pin": 13,
  "value": 128,
  "x": null,
  "y": 1,
  "z": 2,
  "mode": 1
}
```

**Response**

```
{
  "id": 33,
  "created_at": "2022-02-02T23:14:16.167Z",
  "updated_at": "2022-02-02T23:14:16.167Z",
  "mode": 1,
  "pin": 13,
  "value": 128,
  "x": null,
  "y": 1.0,
  "z": 2.0,
  "read_at": "2022-02-02T23:14:16.166Z"
}
```

#  GET /api/sensor_readings

**Response**

```
[
  {
    "id": 35,
    "created_at": "2022-02-02T23:14:16.455Z",
    "updated_at": "2022-02-02T23:14:16.456Z",
    "mode": 0,
    "pin": 387,
    "value": 662,
    "x": 305.0,
    "y": 220.0,
    "z": 57.0,
    "read_at": "2022-02-02T23:14:16.455Z"
  },
  {
    "id": 36,
    "created_at": "2022-02-02T23:13:16.463Z",
    "updated_at": "2022-02-02T23:14:16.464Z",
    "mode": 0,
    "pin": 33,
    "value": 503,
    "x": 311.0,
    "y": 426.0,
    "z": 47.0,
    "read_at": "2022-02-02T23:13:16.463Z
```

#  DELETE /api/sensor_readings/34

**Response**

```
Empty Response
```

#  GET /api/sensor_readings/45

**Response**

```
{
  "id": 45,
  "created_at": "2022-02-02T23:14:16.615Z",
  "updated_at": "2022-02-02T23:14:16.615Z",
  "mode": 0,
  "pin": 416,
  "value": 918,
  "x": 154.0,
  "y": 428.0,
  "z": 462.0,
  "read_at": "2022-02-02T23:14:16.615Z"
}
```

#  GET /api/sensors

**Response**

```
[
  {
    "id": 4,
    "created_at": "2022-02-02T23:14:40.839Z",
    "updated_at": "2022-02-02T23:14:40.839Z",
    "pin": 3,
    "label": "MyString",
    "mode": 1
  },
  {
    "id": 5,
    "created_at": "2022-02-02T23:14:40.847Z",
    "updated_at": "2022-02-02T23:14:40.847Z",
    "pin": 4,
    "label": "MyString",
    "mode": 1
  }
]
```

#  POST /api/sensors

**Request**

```
{
  "pin": 13,
  "label": "LED",
  "mode": 0
}
```

**Response**

```
{
  "id": 7,
  "created_at": "2022-02-02T23:14:40.954Z",
  "updated_at": "2022-02-02T23:14:40.954Z",
  "pin": 13,
  "label": "LED",
  "mode": 0
}
```

#  DELETE /api/sensors/3

**Response**

```
{
  "id": 3,
  "created_at": "2022-02-02T23:14:40.787Z",
  "updated_at": "2022-02-02T23:14:40.787Z",
  "pin": 2,
  "label": "The old label",
  "mode": 1
}
```

#  PUT /api/sensors/6

**Request**

```
{
  "label": "The new label"
}
```

**Response**

```
{
  "id": 6,
  "created_at": "2022-02-02T23:14:40.897Z",
  "updated_at": "2022-02-02T23:14:40.914Z",
  "pin": 5,
  "label": "The new label",
  "mode": 1
}
```

#  GET /api/sensors/8

**Response**

```
{
  "id": 8,
  "created_at": "2022-02-02T23:14:40.997Z",
  "updated_at": "2022-02-02T23:14:40.997Z",
  "pin": 6,
  "label": "MyString",
  "mode": 1
}
```

#  GET /api/sequence_versions/8

**Response**

```
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

```

#  GET /api/sequences

**Response**

```
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
        }
      }
    },
    "color": "orange",
    "folder_id": null,
    "forked": false,
    "name": "Versatile national portal",
    "pinned": false,
    "copyright": null,
    "description": null,
    "sequence_versions": [

    ],
    "sequence_version_id": null,

```

#  POST /api/sequences

**Request**

```
{
  "name": "Scare Birds",
  "body": [

  ],
  "args": {
    "foo": "BAR"
  }
}
```

**Response**

```
{
  "id": 270,
  "created_at": "2022-02-02T23:15:51.569Z",
  "updated_at": "2022-02-02T23:15:51.569Z",
  "args": {
    "version": 20180209,
    "locals": {
      "kind": "scope_declaration",
      "args": {
      }
    }
  },
  "color": "gray",
  "folder_id": null,
  "forked": false,
  "name": "Scare Birds",
  "pinned": false,
  "copyright": null,
  "description": null,
  "sequence_versions": [

  ],
  "sequence_version_id": null,
  "kind": "sequence",
  "body": [

  ]
}
```

#  POST /api/sequences

**Request**

```
{
  "name": "Scare Birds",
  "body": [
    {
      "kind": "move_absolute",
      "args": {
        "location": {
          "kind": "coordinate",
          "args": {
            "x": 1,
            "y": 2,
            "z": 3
          }
        },
        "offset": {
          "kind": "coordinate",
          "args": {
            "x": 0,
            "y": 0,
            "z": 0
          }
        },
        "speed": 4
      },
      "uuid": "b5c45abb-1d70-464d-925f-bc0366f57bf9"
    },
    {

```

**Response**

```
{
  "id": 273,
  "created_at": "2022-02-02T23:15:51.782Z",
  "updated_at": "2022-02-02T23:15:51.782Z",
  "args": {
    "version": 20180209,
    "locals": {
      "kind": "scope_declaration",
      "args": {
      }
    }
  },
  "color": "gray",
  "folder_id": null,
  "forked": false,
  "name": "Scare Birds",
  "pinned": false,
  "copyright": null,
  "description": null,
  "sequence_versions": [

  ],
  "sequence_version_id": null,
  "kind": "sequence",
  "body": [
    {
      "kind": "move_absol
```

#  POST /api/sequences

**Request**

```
{
  "name": "Scare Birds",
  "args": {
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
                "x": 0,
                "y": 0,
                "z": 0
              }
            }
          }
        },
        {
          "kind": "variable_declaration"
```

**Response**

```
{
  "id": 275,
  "created_at": "2022-02-02T23:15:52.200Z",
  "updated_at": "2022-02-02T23:15:52.200Z",
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
                "x": 0,
                "y": 0,
                "z": 0

```

#  POST /api/sequences

**Request**

```
{
  "name": "Scare Birds",
  "body": [

  ]
}
```

**Response**

```
{
  "id": 276,
  "created_at": "2022-02-02T23:15:52.500Z",
  "updated_at": "2022-02-02T23:15:52.500Z",
  "args": {
    "version": 20180209,
    "locals": {
      "kind": "scope_declaration",
      "args": {
      }
    }
  },
  "color": "gray",
  "folder_id": null,
  "forked": false,
  "name": "Scare Birds",
  "pinned": false,
  "copyright": null,
  "description": null,
  "sequence_versions": [

  ],
  "sequence_version_id": null,
  "kind": "sequence",
  "body": [

  ]
}
```

#  POST /api/sequences

**Request**

```
{
  "name": "Scare Birds",
  "body": [
    {
      "kind": "move_absolute",
      "args": {
        "location": {
          "kind": "point",
          "args": {
            "pointer_type": "GenericPointer",
            "pointer_id": 259
          }
        },
        "offset": {
          "kind": "coordinate",
          "args": {
            "x": 0,
            "y": 0,
            "z": 0
          }
        },
        "speed": 100
      }
    }
  ]
}
```

**Response**

```
{
  "id": 278,
  "created_at": "2022-02-02T23:15:59.761Z",
  "updated_at": "2022-02-02T23:15:59.761Z",
  "args": {
    "version": 20180209,
    "locals": {
      "kind": "scope_declaration",
      "args": {
      }
    }
  },
  "color": "gray",
  "folder_id": null,
  "forked": false,
  "name": "Scare Birds",
  "pinned": false,
  "copyright": null,
  "description": null,
  "sequence_versions": [

  ],
  "sequence_version_id": null,
  "kind": "sequence",
  "body": [
    {
      "kind": "move_absol
```

#  POST /api/sequences

**Request**

```
{
  "name": "Scare Birds",
  "body": [
    {
      "kind": "move_absolute",
      "args": {
        "location": {
          "kind": "coordinate",
          "args": {
            "x": 1,
            "y": 2,
            "z": 3
          }
        },
        "offset": {
          "kind": "coordinate",
          "args": {
            "x": 0,
            "y": 0,
            "z": 0
          }
        },
        "speed": 4
      }
    },
    {
      "kind": "move_absolute",
      "args": {
        "lo
```

**Response**

```
{
  "id": 281,
  "created_at": "2022-02-02T23:16:00.055Z",
  "updated_at": "2022-02-02T23:16:00.055Z",
  "args": {
    "version": 20180209,
    "locals": {
      "kind": "scope_declaration",
      "args": {
      }
    }
  },
  "color": "gray",
  "folder_id": null,
  "forked": false,
  "name": "Scare Birds",
  "pinned": false,
  "copyright": null,
  "description": null,
  "sequence_versions": [

  ],
  "sequence_version_id": null,
  "kind": "sequence",
  "body": [
    {
      "kind": "move_absol
```

#  POST /api/sequences

**Request**

```
{
  "name": "v. important sequence",
  "body": [

  ],
  "pinned": true
}
```

**Response**

```
{
  "id": 283,
  "created_at": "2022-02-02T23:16:00.482Z",
  "updated_at": "2022-02-02T23:16:00.482Z",
  "args": {
    "version": 20180209,
    "locals": {
      "kind": "scope_declaration",
      "args": {
      }
    }
  },
  "color": "gray",
  "folder_id": null,
  "forked": false,
  "name": "v. important sequence",
  "pinned": true,
  "copyright": null,
  "description": null,
  "sequence_versions": [

  ],
  "sequence_version_id": null,
  "kind": "sequence",
  "body": [

  ]
}
```

#  POST /api/sequences

**Request**

```
{
  "args": {
    "locals": {
      "kind": "scope_declaration",
      "args": {
      },
      "body": [
        {
          "kind": "variable_declaration",
          "args": {
            "label": "parent",
            "data_value": {
              "kind": "coordinate",
              "args": {
                "x": 50,
                "y": 50,
                "z": 50
              }
            }
          }
        }
      ]
    }
  },
  "color": "gray",
  "name": "MOVE V3 QA",
  "kind": "sequ
```

**Response**

```
{
  "id": 284,
  "created_at": "2022-02-02T23:16:00.594Z",
  "updated_at": "2022-02-02T23:16:00.594Z",
  "args": {
    "version": 20180209,
    "locals": {
      "kind": "scope_declaration",
      "args": {
      },
      "body": [
        {
          "kind": "variable_declaration",
          "args": {
            "label": "parent",
            "data_value": {
              "kind": "coordinate",
              "args": {
                "x": 50,
                "y": 50,
                "z": 50

```

#  POST /api/sequences/1/unpublish

**Response**

```
{
  "published": false,
  "id": 1,
  "cached_author_email": "lanny@keebler.com",
  "author_device_id": 30,
  "author_sequence_id": 1,
  "created_at": "2022-02-02T23:14:15.498Z",
  "updated_at": "2022-02-02T23:14:15.709Z"
}
```

#  POST /api/sequences/19/publish

**Request**

```
{
  "copyright": "FarmBot, Inc. 2021"
}
```

**Response**

```
{
  "id": 6,
  "cached_author_email": "charmain@kulas.info",
  "author_device_id": 81,
  "author_sequence_id": 19,
  "published": true,
  "created_at": "2022-02-02T23:14:22.706Z",
  "updated_at": "2022-02-02T23:14:22.706Z"
}
```

#  POST /api/sequences/217/upgrade/16

**Request**

```
{
  "sequence_version_id": "16"
}
```

**Response**

```
{
  "id": 217,
  "created_at": "2022-02-02T23:15:37.558Z",
  "updated_at": "2022-02-02T23:15:37.558Z",
  "args": {
    "version": 20180209,
    "locals": {
      "kind": "scope_declaration",
      "args": {
      }
    }
  },
  "color": "gray",
  "folder_id": null,
  "forked": false,
  "name": "Grass-roots didactic system engine",
  "pinned": false,
  "copyright": "Farmbot, Inc 2021",
  "description": null,
  "sequence_versions": [
    16
  ],
  "sequence_version_id": 16,
  "kind": "sequence"
}
```

#  DELETE /api/sequences/230

**Response**

```
Empty Response
```

#  DELETE /api/sequences/232

**Response**

```
Empty Response
```

#  PATCH /api/sequences/30

**Request**

```
{
  "id": 30,
  "sequence": {
    "name": "no",
    "args": {
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

```

**Response**

```
{
  "id": 30,
  "created_at": "2022-02-02T23:14:28.115Z",
  "updated_at": "2022-02-02T23:14:28.265Z",
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

```

#  PATCH /api/sequences/31

**Request**

```
{
  "sequence": {
    "name": "pinned",
    "pinned": true,
    "args": {
    },
    "body": [

    ]
  }
}
```

**Response**

```
{
  "id": 31,
  "created_at": "2022-02-02T23:14:28.334Z",
  "updated_at": "2022-02-02T23:14:28.456Z",
  "args": {
    "version": 20180209,
    "locals": {
      "kind": "scope_declaration",
      "args": {
      }
    }
  },
  "color": "gray",
  "folder_id": null,
  "forked": false,
  "name": "pinned",
  "pinned": true,
  "copyright": null,
  "description": null,
  "sequence_versions": [

  ],
  "sequence_version_id": null,
  "kind": "sequence",
  "body": [

  ]
}
```

#  GET /api/sequences/85

**Response**

```
{
  "id": 85,
  "created_at": "2022-02-02T23:14:41.485Z",
  "updated_at": "2022-02-02T23:14:41.526Z",
  "args": {
    "version": 20180209,
    "locals": {
      "kind": "scope_declaration",
      "args": {
      }
    }
  },
  "color": "gray",
  "folder_id": null,
  "forked": false,
  "name": "Enterprise-wide 6th generation access",
  "pinned": false,
  "copyright": null,
  "description": null,
  "sequence_versions": [

  ],
  "sequence_version_id": null,
  "kind": "sequence",
  "body": [

  ]
}
```

#  POST /api/sequences/9/install

**Request**

```
{
  "sequence_version_id": "9"
}
```

**Response**

```
{
  "id": 41,
  "created_at": "2022-02-02T23:14:33.394Z",
  "updated_at": "2022-02-02T23:14:33.399Z",
  "args": {
    "version": 20180209,
    "locals": {
      "kind": "scope_declaration",
      "args": {
      }
    }
  },
  "color": "purple",
  "folder_id": null,
  "forked": false,
  "name": "Organic zero tolerance open system",
  "pinned": false,
  "copyright": "FarmBot, Inc. 2021",
  "description": null,
  "sequence_versions": [
    9
  ],
  "sequence_version_id": 9,
  "kind": "sequence"
}
```

#  GET /api/storage_auth

**Response**

```
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
  "instructions": "Send a 'from-data' request to the URL provided.Then POST the resulting URL as an 'att
```

#  GET /api/storage_auth

**Response**

```
{
  "verb": "POST",
  "url": "//192.168.1.112:3000/direct_upload/",
  "form_data": {
    "key": "temp/6978bff3-b849-4a5d-b0db-f1ba5811960e.jpg",
    "acl": "public-read",
    "Content-Type": "image/jpeg",
    "policy": "N/A",
    "signature": "N/A",
    "GoogleAccessId": "N/A",
    "file": "REPLACE_THIS_WITH_A_BINARY_JPEG_FILE"
  },
  "instructions": "Send a 'from-data' request to the URL provided.Then POST the resulting URL as an 'attachment_url' (json) to api/images/."
}
```

#  GET /api/tokens

**Response**

```
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
    "encoded": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJhdWQiOiJ1bmtub3duIiwic3ViIjoxMzQsImlhdCI6MTY0Mzg0MzY4MCwianRpIjoiMjJkZWFjZjMtY2I3Yy00YjQyLTk3MjctMjRkNG
```

#  GET /api/tokens

**Response**

```
{
  "token": {
    "unencoded": {
      "aud": "unknown",
      "sub": 135,
      "iat": 1643843680,
      "jti": "12436d09-0cdc-4c80-b625-c244552dc98a",
      "iss": "//192.168.1.112:3000",
      "exp": 1649027680,
      "mqtt": "blooper.io",
      "bot": "device_215",
      "vhost": "/",
      "mqtt_ws": "ws://blooper.io:3002/ws"
    },
    "encoded": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJhdWQiOiJ1bmtub3duIiwic3ViIjoxMzUsImlhdCI6MTY0Mzg0MzY4MCwianRpIjoiMTI0MzZkMDktMGNkYy00YzgwLWI2MjUtYzI0ND
```

#  GET /api/tokens

**Response**

```
{
  "token": {
    "unencoded": {
      "aud": "unknown",
      "sub": 136,
      "iat": 1643843680,
      "jti": "5853a785-3787-4d51-bba5-0650389d1bfe",
      "iss": "//192.168.1.112:3000",
      "exp": 1649027680,
      "mqtt": "blooper.io",
      "bot": "device_216",
      "vhost": "/",
      "mqtt_ws": "ws://blooper.io:3002/ws"
    },
    "encoded": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJhdWQiOiJ1bmtub3duIiwic3ViIjoxMzYsImlhdCI6MTY0Mzg0MzY4MCwianRpIjoiNTg1M2E3ODUtMzc4Ny00ZDUxLWJiYTUtMDY1MD
```

#  POST /api/tokens

**Request**

```
{
  "user": {
    "email": "saul@mckenzie.com",
    "password": "password"
  }
}
```

**Response**

```
{
  "token": {
    "unencoded": {
      "aud": "unknown",
      "sub": 297,
      "iat": 1643843735,
      "jti": "15190aaa-73b6-4fdf-b6b7-f421fa7450a8",
      "iss": "//192.168.1.112:3000",
      "exp": 1649027735,
      "mqtt": "blooper.io",
      "bot": "device_422",
      "vhost": "/",
      "mqtt_ws": "ws://blooper.io:3002/ws"
    },
    "encoded": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJhdWQiOiJ1bmtub3duIiwic3ViIjoyOTcsImlhdCI6MTY0Mzg0MzczNSwianRpIjoiMTUxOTBhYWEtNzNiNi00ZmRmLWI2YjctZjQyMW
```

#  POST /api/tools

**Request**

```
{
  "tool_slot_id": 97,
  "name": "wow"
}
```

**Response**

```
{
  "id": 42,
  "created_at": "2022-02-02T23:14:39.322Z",
  "updated_at": "2022-02-02T23:14:39.322Z",
  "name": "wow",
  "status": "inactive"
}
```

#  GET /api/tools

**Response**

```
[
  {
    "id": 129,
    "created_at": "2022-02-02T23:15:37.737Z",
    "updated_at": "2022-02-02T23:15:37.737Z",
    "name": "PoliwhirlVileplume",
    "status": "active"
  }
]
```

#  GET /api/tools/12

**Response**

```
{
  "id": 12,
  "created_at": "2022-02-02T23:14:27.477Z",
  "updated_at": "2022-02-02T23:14:27.477Z",
  "name": "NinetalesPrimeape",
  "status": "active"
}
```

#  DELETE /api/tools/20

**Response**

```
{
  "id": 20,
  "created_at": "2022-02-02T23:14:32.240Z",
  "updated_at": "2022-02-02T23:14:32.240Z",
  "name": "WeepinbellMuk",
  "status": "inactive"
}
```

#  DELETE /api/tools/22

**Response**

```
{
  "id": 22,
  "created_at": "2022-02-02T23:14:32.348Z",
  "updated_at": "2022-02-02T23:14:32.348Z",
  "name": "GyaradosTangela",
  "status": "inactive"
}
```

#  PUT /api/tools/46

**Request**

```
{
  "name": "Hi!"
}
```

**Response**

```
{
  "id": 46,
  "created_at": "2022-02-02T23:14:48.343Z",
  "updated_at": "2022-02-02T23:14:48.363Z",
  "name": "Hi!",
  "status": "active"
}
```

#  PATCH /api/users

**Request**

```
{
  "email": "rick@rick.com",
  "name": "Ricky McRickerson",
  "format": "json"
}
```

**Response**

```
{
  "id": 228,
  "created_at": "2022-02-02T23:14:56.685Z",
  "updated_at": "2022-02-02T23:14:56.722Z",
  "name": "Ricky McRickerson",
  "email": "magda@bogisich-hackett.org"
}
```

#  DELETE /api/users

**Request**

```
{
  "password": "SeYgNi5A0"
}
```

**Response**

```
{
  "id": null,
  "priority": 0,
  "attempts": 0,
  "handler": "--- !ruby/object:Delayed::PerformableMethod\nobject: !ruby/object:User\n  concise_attributes:\n  - !ruby/object:ActiveModel::Attribute::FromDatabase\n    name: id\n    value_before_type_cast: 231\n  - !ruby/object:ActiveModel::Attribute::FromDatabase\n    name: device_id\n    value_before_type_cast: 324\n  - !ruby/object:ActiveModel::Attribute::FromDatabase\n    name: name\n    value_before_type_cast: Earl Huels\n  - !ruby/object:Ac
```

#  PATCH /api/users

**Request**

```
{
  "password": "Ge3OiFcX1cVd25",
  "new_password": "123456789",
  "new_password_confirmation": "123456789",
  "format": "json"
}
```

**Response**

```
{
  "id": 232,
  "created_at": "2022-02-02T23:14:56.893Z",
  "updated_at": "2022-02-02T23:14:56.931Z",
  "name": "Napoleon Klocko",
  "email": "ed_berge@brakus-graham.net"
}
```

#  GET /api/users

**Response**

```
[
  {
    "id": 234,
    "created_at": "2022-02-02T23:14:56.988Z",
    "updated_at": "2022-02-02T23:14:56.988Z",
    "name": "Susana Bogan",
    "email": "suzy@hirthe.name"
  }
]
```

#  POST /api/users

**Request**

```
{
  "password_confirmation": "Password123",
  "password": "Password123",
  "email": "delbert.veum@johns.info",
  "name": "Frank"
}
```

**Response**

```
{
  "message": "Check your email!"
}
```

#  POST /api/users/control_certificate

**Request**

```
{
  "email": "jerold@kemmer-hagenes.com",
  "password": "password456"
}
```

**Response**

```
Empty Response
```

#  POST /api/users/resend_verification

**Request**

```
{
  "email": "aurelio@kozey.net"
}
```

**Response**

```
{
  "user": "Check your email!"
}
```

#  PUT /api/web_app_config

**Request**

```
{
  "info_log": 23,
  "bot_origin_quadrant": -1
}
```

**Response**

```
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
  "x_axis
```

#  PUT /api/web_app_config

**Request**

```
{
  "device_id": 99
}
```

**Response**

```
{
  "id": 3,
  "created_at": "2022-02-02T23:14:24.474Z",
  "updated_at": "2022-02-02T23:14:24.474Z",
  "device_id": 87,
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
  "x_axis
```

#  PUT /api/web_app_config

**Request**

```
{
  "info_log": 23,
  "bot_origin_quadrant": -1,
  "internal_use": "null"
}
```

**Response**

```
{
  "id": 4,
  "created_at": "2022-02-02T23:14:24.521Z",
  "updated_at": "2022-02-02T23:14:24.536Z",
  "device_id": 88,
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
  "x_axis
```

#  DELETE /api/web_app_config

**Response**

```
Empty Response
```

#  GET /api/web_app_config

**Response**

```
{
  "id": 8,
  "created_at": "2022-02-02T23:14:24.672Z",
  "updated_at": "2022-02-02T23:14:24.672Z",
  "device_id": 90,
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
  "x_axis
```

#  GET /api/webcam_feeds

**Response**

```
[
  {
    "id": 14,
    "created_at": "2022-02-02T23:14:53.317Z",
    "updated_at": "2022-02-02T23:14:53.317Z",
    "url": "0",
    "name": "feed 0"
  },
  {
    "id": 15,
    "created_at": "2022-02-02T23:14:53.322Z",
    "updated_at": "2022-02-02T23:14:53.322Z",
    "url": "1",
    "name": "feed 1"
  }
]
```

#  POST /api/webcam_feeds

**Request**

```
{
  "name": "name1",
  "url": "url1"
}
```

**Response**

```
{
  "id": 23,
  "created_at": "2022-02-02T23:15:47.730Z",
  "updated_at": "2022-02-02T23:15:47.730Z",
  "url": "url1",
  "name": "name1"
}
```

#  DELETE /api/webcam_feeds/20

**Response**

```
Empty Response
```

#  GET /api/webcam_feeds/22

**Response**

```
{
  "id": 22,
  "created_at": "2022-02-02T23:15:47.684Z",
  "updated_at": "2022-02-02T23:15:47.684Z",
  "url": "Url!",
  "name": "Name!"
}
```

#  PATCH /api/webcam_feeds/9

**Request**

```
{
  "url": "/foo.jpg",
  "name": "ok"
}
```

**Response**

```
{
  "id": 9,
  "created_at": "2022-02-02T23:14:39.358Z",
  "updated_at": "2022-02-02T23:14:39.372Z",
  "url": "/foo.jpg",
  "name": "ok"
}
```

#  GET /api/wizard_step_results

**Response**

```
[
  {
    "id": 5,
    "created_at": "2022-02-02T23:15:34.279Z",
    "updated_at": "2022-02-02T23:15:34.279Z",
    "answer": false,
    "outcome": "Leech Life",
    "slug": "Poliwrath"
  },
  {
    "id": 6,
    "created_at": "2022-02-02T23:15:34.283Z",
    "updated_at": "2022-02-02T23:15:34.283Z",
    "answer": false,
    "outcome": "Dizzy Punch",
    "slug": "Caterpie"
  },
  {
    "id": 7,
    "created_at": "2022-02-02T23:15:34.287Z",
    "updated_at": "2022-02-02T23:15:34.287Z",
    "answer":
```

#  POST /api/wizard_step_results

**Request**

```
{
  "slug": "MY_SLUG"
}
```

**Response**

```
{
  "id": 10,
  "created_at": "2022-02-02T23:15:34.374Z",
  "updated_at": "2022-02-02T23:15:34.374Z",
  "answer": null,
  "outcome": null,
  "slug": "MY_SLUG"
}
```

#  DELETE /api/wizard_step_results/11

**Response**

```
Empty Response
```

#  PATCH /api/wizard_step_results/9

**Request**

```
{
  "slug": "MY_SLUG"
}
```

**Response**

```
{
  "id": 9,
  "created_at": "2022-02-02T23:15:34.326Z",
  "updated_at": "2022-02-02T23:15:34.339Z",
  "answer": false,
  "outcome": "Bone Club",
  "slug": "MY_SLUG"
}
```

#  GET /app/nope.jpg

**Request**

```
{
  "path": "nope.jpg"
}
```

**Response**

```
Empty Response
```

#  POST /csp_reports

**Response**

```
{
  "problem": "Crashed while parsing report"
}
```

#  POST /csp_reports.json

**Response**

```
{
}
```

#  POST /direct_upload

**Request**

```
{
  "file": "fake_file",
  "key": "fake_key"
}
```

**Response**

```
Empty Response
```

#  GET /featured

**Response**

```
Empty Response
```

#  GET /os

**Response**

```
Empty Response
```

#  GET /tos_update

**Response**

```
Empty Response
```

#  GET /verify/632a1740-855d-4f62-9c99-b2109b91ab3e

**Request**

```
{
  "token": "632a1740-855d-4f62-9c99-b2109b91ab3e"
}
```

**Response**

```
Empty Response
```

#  GET /verify/9a67a4a5-e98f-463f-b3b9-5132b5914d76

**Request**

```
{
  "token": "9a67a4a5-e98f-463f-b3b9-5132b5914d76"
}
```

**Response**

```
Empty Response
```


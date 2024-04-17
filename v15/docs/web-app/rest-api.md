---
title: "REST API"
slug: "rest-api"
description: "[Example API requests](api-docs.md)"
---

The **REST API** is an HTTP web server commonly referred to as "The API", "The REST API" or simply "The server". The REST API handles a number of responsibilities including:

 * **Data storage, validation, and security:** Allows users to edit information such as sequences and the garden layout even when the device is offline, prevents data loss between factory resets of FarmBot OS by storing the data in the cloud, validates data and controls access to data via authentication and authorization mechanisms.
 * **Email delivery:** Sends email notifications such as password resets and critical errors to end users. All other messaging is handled by the [Message Broker](../message-broker.md), a distinctly decoupled sub-system of the Web API.
 * **Image uploads and manipulation:** Re-sizes and stores images captured by FarmBot's onboard camera.

{%
include callout.html
type="info"
content="Generally speaking, the REST API does _not_ control FarmBot. Device control is handled by the [Message Broker](../message-broker.md), [CeleryScript](../celery-script.md), and [FarmBot JS](../farmbot-js.md)."
%}

# Specifications

|                              |                              |
|------------------------------|------------------------------|
|Web Framework                 |[Ruby on Rails](https://rubyonrails.org)
|Authorization Mechanism       |[JSON Web Tokens](https://jwt.io)
|Deployment Methodology        |[12 Factor](https://12factor.net)
|API Architectural Style       |[REST](https://en.wikipedia.org/wiki/Representational_state_transfer)
|Database                      |[PostgreSQL](https://www.postgresql.org)
|Test Framework                |[RSpec](http://rspec.info)
|File Storage Mechanism        |[Google Cloud Storage](https://cloud.google.com/storage/) or filesystem (configurable)
|Error Monitoring              |[Rollbar](https://rollbar.com) (optional)
|Operating System              |[Ubuntu](https://www.ubuntu.com) (**not** configurable)
|Continuous Integration System |[Circle CI](https://circleci.com/) (optional)

# Resources

**Resources** are JSON documents that can be downloaded from the server and used by FarmBots, humans, and third-party tools to store FarmBot related information. Every resource has a URL, and the [HTTP verb](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods) used to access the URL will determine how the server handles the request.

As of April 2024, the API manages the following resources:

|Resource                                                |Description                                     |Pagination?|
|--------------------------------------------------------|------------------------------------------------|-----------|
|[`ai_feedbacks`](api-docs-next.md#ai_feedbacks)              |Positive/negative reactions to auto-generation prompt results.
|[`alerts`](api-docs-next.md#alerts)                          |A single item in the message center. Only useful to site administrators.|Yes
|[`corpus`](api-docs-next.md#corpus)                          |A glossary of all Celery Script node types in JSON format.
|[`curves`](api-docs-next.md#curves)                          |Time-based plant water/height/spread data tables.|Yes
|[`device`](api-docs-next.md#device)                          |Device account settings.
|[`export_data`](api-docs-next.md#export_data)                |A dump of all the resources listed above.
|[`farm_events`](api-docs-next.md#farm_events)                |Executes a sequence or regimen based on time. Eg: "Execute this sequence every 6 hours".|Yes
|[`farmware_envs`](api-docs-next.md#farmware_envs)            |Key/value pairs used for persistent storage.|Yes
|[`fbos_config`](api-docs-next.md#fbos_config)                |Configuration for FarmBot OS.
|[`featured_sequences`](api-docs-next.md#featured_sequences)  |Promoted publicly shared sequences available for import.
|[`firmware_config`](api-docs-next.md#firmware_config)        |Configuration for the Arduino Firmware
|[`folders`](api-docs-next.md#folders)                        |Organization for sequences.
|[`global_bulletins`](api-docs-next.md#global_bulletins)      |(advanced) An announcement intended for all users of a server
|[`global_config`](api-docs-next.md#global_config)            |Configuration for all users of a server.
|[`images`](api-docs-next.md#images)                          |Meta data about photos taken by FarmBot.
|[`logs`](api-docs-next.md#logs)                              |Messages from a device.
|[`peripherals`](api-docs-next.md#peripherals)                |Meta data about output hardware.|Yes
|[`pin_bindings`](api-docs-next.md#pin_bindings)              |Bind an I/O pin to sequence execution.|Yes
|[`plant_templates`](api-docs-next.md#plant_templates)        |A single plant within a saved garden. Not a real plant.|Yes
|[`points`](api-docs-next.md#points)                          |Represents a saved point on the garden bed. All point types are included in this resource: Plants, Weeds, Tool Slots, and Generic Points.
|[`point_groups`](api-docs-next.md#point_groups)              |A collection of points based on a criteria or predefined set of points (eg: "All Weeds", "My Basil Plants" etc..)|Yes
|[`public_key`](api-docs-next.md#public_key)                  |(advanced) A public encryption key owned by the API server.
|[`regimens`](api-docs-next.md#regimens)                      |Executes sequences based on an offset from the regimen start date.|Yes
|[`releases`](api-docs-next.md#releases)                      |FarmBot OS releases.
|[`saved_gardens`](api-docs-next.md#saved_gardens)            |A pre arranged configuration of plants in a garden.|Yes
|[`sensor_readings`](api-docs-next.md#sensor_readings)        |A single reading from a sensor, recorded to the API.|Yes
|[`sensors`](api-docs-next.md#sensors)                        |Meta data about input hardware.|Yes
|[`sequence_versions`](api-docs-next.md#sequence_versions)    |Published versions of sequences for sharing.
|[`sequences`](api-docs-next.md#sequences)                    |Commands created in the sequence editor.
|[`storage_auth`](api-docs-next.md#storage_auth)              |(advanced) A policy object for Google Cloud Storage.
|[`telemetries`](api-docs-next.md#telemetries)                |Historical FarmBot OS status information.
|[`tokens`](api-docs-next.md#tokens)                          |An authorization / authentication secret shared between a user or device and the API.
|[`tools`](api-docs-next.md#tools)                            |An physical object that is mounted to the gantry or a tool slot (UTM).|Yes
|[`users`](api-docs-next.md#users)                            |Device operator data such as registration email.
|[`web_app_config`](api-docs-next.md#web_app_config)          |User interface preferences.
|[`webcam_feeds`](api-docs-next.md#webcam_feeds)              |Meta data about an external webcam (stream URL)|Yes
|[`wizard_step_results`](api-docs-next.md#wizard_step_results)|Setup wizard result data.|Yes

## Example request

If we wished to change the name of our device to "Carrot Overlord", we could perform an HTTP `PUT` to the URL `https://my.farm.bot/api/device/325` with the following request body:

```json
{
  "name": "Carrot Overlord"
}
```

Such a request would generate the following JSON HTTP response:

```json
{
  "id": 325,
  "name": "Carrot Overlord",
  "timezone": "America/Curacao",
  "last_saw_api": null,
  "last_saw_mq": null,
  "tz_offset_hrs": -4,
  "fbos_version": null,
  "throttled_until": null,
  "throttled_at": null
}
```

## Pagination

Some API endpoints support **pagination** of `GET` requests to break the results into smaller "pages" of a fixed length. To make a paginated request, append [query strings](https://en.wikipedia.org/wiki/Query_string) for **page size** (eg: `per=10`) and **page number** (eg: `page=3`) to the request.

For example, to download the third page of `sensor_readings` with a page size of 10 items:

```
GET https://my.farm.bot/api/sensor_readings?page=3&per=10
```

# Points endpoint

While the REST API is relatively uniform in how it handles resources, `plants`, `weeds`, `tool_slots`, and generic `points` fall under the same `/api/points` endpoint. This endpoint also has some additional capabilities that the other endpoints do not.

## Bulk deletion

To delete many point resources in one request, separate the point IDs with a comma:

```
DELETE https://farm.bot/api/points/1,4,23
```

{%
include callout.html
type="warning"
content="When points are deleted, it is still possible to view them for 2 months after the time of deletion. This is useful for tools relating to weeding and historical records.
"
%}

## Filtering

The points endpoint supports a special `?filter=` [query parameter](https://en.wikipedia.org/wiki/Query_string). There are three options for this parameter:

  * `?filter=all` returns archived and active points.
  * `?filter=old` only returns archived points.
  * `?filter=kept` only returns active (not-archived) points. **This is the default behavior for the index endpoint (`/api/points`).**

# Generating an API token

You must pass a `token` string into most HTTP requests under the `Authorization` request header. Here are some ways in which you can get a token. Also see our [web app API examples](../../python/web-app-api-examples.md).


```curl
curl -H "Content-Type: application/json" \
     -X POST \
     -d '{"user":{"email":"test123@test.com","password":"password123"}}' \
     https://my.farm.bot/api/tokens
```

```javascript
// Since the API supports [CORS](http://enable-cors.org/), you can generate your
// token right in the browser. Here's an example:

$.ajax({
    url: "https://my.farm.bot/api/tokens",
    type: "POST",
    data: JSON.stringify({user: {email: 'admin@admin.com', password: 'password123'}}),
    contentType: "application/json",
    success: function (data) {
                 // You can now use your token:
                 var MY_SHINY_TOKEN = data.token.encoded;
             }
});
```

```python
import requests
response = requests.request(
    method='POST',
    url='https://my.farm.bot/api/tokens',
    headers={'content-type': 'application/json'},
    json={'user': {'email': 'admin@admin.com', 'password': 'password123'}})
TOKEN = response.json()['token']['encoded']
```

And here's what the response will look like:

```json
{
    "token": {
        "unencoded": {
            ...
            "iat": 1459109728,
            // USE THIS AS YOUR USERNAME WHEN LOGGING INTO THE MESSAGE BROKER:
            "bot": "device_456",
            "jti": "922a5a0d-0b3a-4767-9318-1e41ae600352",
            "exp": 1459455328
        },
        "encoded":
        // THE IMPORTANT PART IS HERE (shortened for clarity):
         "eyJ0eXAiOiJ...Ry7CiA"
    }
}
```

{%
include callout.html
type="info"
title=""
content="The response is provided as JSON for human readability. For your `Authorization` header, you will only be using `data.token.encoded`. In this example, it's the string starting with `eyJ0eXAiOiJ...`"
%}

# Security

The API uses [JSON Web Tokens](https://jwt.io) for authentication and authorization. Additionally, it uses [Content Security Policies](https://en.wikipedia.org/wiki/Content_Security_Policy) to prevent unauthorized access by malicious software on client machines.

# What's next?

 * [Example API requests](api-docs.md)

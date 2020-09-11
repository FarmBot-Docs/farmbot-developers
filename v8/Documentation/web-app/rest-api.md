---
title: "REST API"
slug: "rest-api"
excerpt: "[Example API requests](https://gist.github.com/RickCarlino/10db2df375d717e9efdd3c2d9d8932af)"
hidden: false
createdAt: "2018-05-15T21:36:52.836Z"
updatedAt: "2019-12-13T05:30:05.098Z"
---
The **REST API** is an HTTP web server commonly referred to as "The API", "The REST API" or simply "The Server". The REST API handles a number of responsibilities including:

 * **Data storage, validation, and security:** Prevents data loss between reflashes by storing it in a centralized database, allows users to edit information when the device is offline, validates data and controls access to data via authentication and authorization mechanisms.
 * **Email delivery:** Sends email notifications (such as password resets and critical errors) to end users. All other messaging is handled by the [Message Broker](doc:message-broker), a distinctly decoupled sub-system of the Web API.
 * **Image uploads and manipulation:** Re-sizes and stores images captured by FarmBot's internal camera.

Generally speaking, the REST API does _not_ control FarmBot. Device control is handled by the [Message Broker](doc:message-broker), [CeleryScript](doc:celery-script) and [FarmBot JS](doc:farmbot-js).

## API specifications

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
|OS                            |[Ubuntu](https://www.ubuntu.com) (**not** configurable)
|Continous Integration System  |[Circle CI](https://circleci.com/) (optional)



# Resources

**Resources** are JSON documents that can be downloaded from the server and used by devices, humans, and third-party tools to store FarmBot related information. Resources have names like "tool", "plant", "device" and "user".

Every resource has a URL, and the [HTTP verb](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods) used to access the URL will determine how the server handles the request:

|HTTP VERB                     |Action                        |
|------------------------------|------------------------------|
|`GET`                         |View resource(s).
|`PUT`, `PATCH`                |Update or replace a resource.
|`POST`                        |Create a new resource.
|`DELETE`                      |Destroy a resource.

As an example, if we wished to change the name of our device to "carrot overlord", we could perform an HTTP `PUT` to the URL `https://my.farm.bot/api/device/325` with the following request body:

```
{
  "name": "Carrot Overlord"
}
```

Such a request would generate the following HTTP response:


__JSON HTTP RESPONSE:__

```json

  "id": 325,
  "name": "Carrot Overlord",
  "timezone": "America/Curacao",
  "last_saw_api": null,
  "last_saw_mq": null,
  "tz_offset_hrs": -4,
  "fbos_version": null,
  "throttled_until": null,
  "throttled_at": null
```

## Resource list
As of August 2018, the API manages the following resources:

|Resource Name    |Description                                     |
|-----------------|------------------------------------------------|
|device           |Device account settings.
|users            |Device operator data such as registration email.
|tokens           |An authorization / authentication secret shared between a user or device and the API.
|sequences        |Commands created in the sequence editor.
|regimens         |Executes sequence(s) based on arbitrary dates and time on a calendar.
|farm_events      |Executes a sequence or regimen based on time. Eg: "Execute this sequence every 6 hours".
|images           |Meta data about photos taken by FarmBot.
|logs             |Messages from a device.
|peripherals      |Meta data about output hardware.
|sensors          |Meta data about input hardware.
|sensor_readings  |A single reading from a sensor, recorded to the API.
|pin_bindings     |Bind an I/O pin to sequence execution.
|saved_gardens    |A pre arranged configuration of plants in a garden.
|plant_templates  |A single plant within a saved garden. Not a real plant.
|points           |Represents a saved point on the garden bed. Example: Plants, Tool Slots or Generic Points.
|tools            |An physical object that is mounted to the gantry or a tool slot (UTM).
|webcam_feeds     |Meta data about an external webcam (stream URL)
|fbos_config      |Configuration for FarmBot OS.
|firmware_config  |Configuration for the Arduino Firmware
|global_config    |Configuration for all users of a server.
|web_app_config   |User interface preferences.
|farmware_envs    |Key/value pairs used by Farmware authors for persistent storage.
|alerts           |A single item in the message center.
|diagnostic_dumps |A dump of all internal FarmBot logs used to assist in troubleshooting.
|corpus           |A glossary of all Celery Script node types.
|global_bulletins |(advanced)An anouncement intended for all users of a server
|public_key       |(advanced) A public encryption key owned by the API server.
|storage_auth     |(advanced) A policy object for Google Cloud Storage
|export_data      |A dump of all the resources listed above.


# Generating an API token

You must pass a `token` string into most HTTP requests under the `Authorization` request header. Here are some ways in which you can get a token. Also see our [web app API examples](doc:web-app-api-examples).


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

    "token": {
        "unencoded": {
            // Some fields removed for brevity.
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
```



__:__
The response is provided as JSON for human readability. For your `Authorization` header, you will only be using `data.token.encoded`. In this example, it's the string starting with `eyJ0eXAiOiJ...`

# Security
The API uses [JSON Web Tokens](https://jwt.io) for authentication and authorization (see "Frequently Asked Questions" section for token generation instructions). Additionally, it uses [Content Security Policies](https://en.wikipedia.org/wiki/Content_Security_Policy) to prevent unauthorized access by malicious software on client machines.

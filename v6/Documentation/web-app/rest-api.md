---
title: "REST API"
slug: "rest-api"
---

* toc
{:toc}


{% include callout.html type="info" title="One Software Package, Many Uses" content="The [Web App](https://github.com/FarmBot/Farmbot-Web-App) is one software package that serves multiple use cases. In this document, we will only focus on the RESTful JSON API endpoints. This is typically used for managing configuration and creating \"resources\" such as `plants` and `tools`." %}

# What are Resources and How Do I Interact With Them?

The term "resource" is used extensively in this document. When we refer to "resources" in this article, we are specifically referring to JSON documents that can be downloaded from the server. The resources are used by devices, humans and third-party tools to store FarmBot related information. Resources will have names like "tool", "plant", "device" and "user".

**Every resource has a URL**. The [HTTP verb](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods) used to access the URL will determine how the server handles the request:

|HTTP VERB                     |Action                        |
|------------------------------|------------------------------|
|GET                           |View resource(s).
|PUT/PATCH                     |Update or replace a resource.
|POST                          |Create a new resource.
|DELETE                        |Destroy a resource.

So, as an example, if we wished to change the name of our device to "carrot overlord", we could perform an HTTP `PUT` to the URL `https://my.farm.bot/api/device/325` with the following request body:

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

# Example Requests

We maintain a [list of working examples here](https://gist.github.com/RickCarlino/10db2df375d717e9efdd3c2d9d8932af). This list is useful if you are unsure of which resources are available. Most browsers can search the document for keywords using the <kbd>ctrl</kbd> <kbd>F</kbd> hotkey.

# Overview

The REST API is an HTTP web server commonly referred to as "The API", "The REST API" or simply "The Server".

The REST API handles a number of responsibilities including:

 * **Data Storage, Validation, Security:** Prevents data loss between reflashes by storing it in a centralized database, allows users to edit information when the device is offline, validates data and controls access to data via authentication and authorization mechanisms.
 * **Email Delivery:** Sends email notifications (such as password resets and critical errors) to end users. All other messaging is handled by the [Message Broker](/v6/Documentation/web-app/message-broker.md), a distinctly decoupled sub-system of the Web API.
 * **Image Manipulation and Uploads:** Re-sizes and stores images captured by FarmBot's internal camera.

Genreally speaking, the REST API does _not_ control FarmBot. Device control is handled by the [Message Broker](/v6/Documentation/web-app/message-broker.md), [CeleryScript](/v6/Documentation/celery-script.md) and [FarmBot JS](/v6/Documentation/farmbot-js.md).

# API Technical Specifications

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
|Continous Integration System  |[Travis CI](https://travis-ci.org) (optional)
|Performance Profiler          |[Skylight](https://www.skylight.io) (optional)

# Security

The API uses [JSON Web Tokens](https://jwt.io) for authentication and authorization (see "Frequently Asked Questions" section for token generation instructions). Additionally, it uses [Content Security Policies](https://en.wikipedia.org/wiki/Content_Security_Policy) to prevent unauthorized access by malicious software on client machines.

# Resource List

As of August 2018, the API manages the following resources:

| Resource                 |                    |
|--------------------------|--------------------|
| `device`                 | Basic configuration of the device, such as its `name`.|
| `diagnostic_dumps`       | A (gigantic) JSON document used by FarmBot employees to help users find device problems.|
| `farm_events`            ||
| `farmware_envs`          ||
| `farmware_installations` ||
| `fbos_config`            | FarmBot OS specific configurations|
| `firmware_config`        ||
| `images`                 | Meta data about image captures. Contains a URL to the actual image file.|
| `peripherals`            ||
| `pin_bindings`           ||
| `plant_templates`        ||
| `points`                 ||
| `regimens`               ||
| `sensor_readings`        ||
| `sensors`                ||
| `sequences`              ||
| `tokens`                 ||
| `tools`                  ||
| `web_app_config`         | User preferences used by the web app only. Example: Turning animations on or off.|
| `webcam_feeds`           ||

# Frequently Asked Questions

## How Can I Control the Bot Via HTTP Requests?

The REST API does not control devices. It is only used for data storage, email delivery and image resizing. To control a device remotely, please see documentation for the [Message Broker](/v6/Documentation/web-app/message-broker.md), [CeleryScript](/v6/Documentation/celery-script.md) and [FarmBot JS](/v6/Documentation/farmbot-js.md).

## Where Can I See API Example Usage?

We maintain an [automatically generated list of example requests here](https://gist.github.com/RickCarlino/10db2df375d717e9efdd3c2d9d8932af). Fully formed API docs will be available soon.

## How Do I Generate an API Token?

You must pass a `token` string into most HTTP requests under the `Authorization: ` request header.

Here's what a response looks like when you request a token:


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

**Important:** The response is provided as JSON for human readability. For your `Authorization` header, you will only be using `data.token.encoded`. In this example, it's the string starting with `eyJ0eXAiOiJ...`

## Create a Token Using CURL


```curl
curl -H "Content-Type: application/json" \
     -X POST \
     -d '{"user":{"email":"test123@test.com","password":"password123"}}' \
     https://my.farmbot.io/api/tokens
```

## Create a Token Using JQuery

Since the API supports [CORS](http://enable-cors.org/), you can generate your token right in the browser.

Here's an example:


```javascript
$.ajax({
    url: "https://my.farmbot.io/api/tokens",
    type: "POST",
    data: JSON.stringify({user: {email: 'admin@admin.com', password: 'password123'}}),
    contentType: "application/json",
    success: function (data) {
                 // You can now use your token:
                 var MY_SHINY_TOKEN = data.token.encoded;
             }
});
```


---
title: "Software Development Tools Used By FarmBot"
slug: "software-development-tools"
---

* toc
{:toc}


{%
include callout.html
type="danger"
title="Advanced Topics Ahead!"
content="The document below provides developers a picture of internal system implementation details. For most third-party software developers, in-depth knowledge of each component is not necessary.

Very few developers will interact with every component of the system. As such, an understanding of every tool listed below is not required."
%}

# Summary of our developer tools
The table below shows a rough overview of the developer tools used when working on various aspects of the FarmBot software system. Realistically, no one would need to know all of these tools; the actual tool set required will vary based on the task you want to perform.

|                              |                              |
|------------------------------|------------------------------|
|[Firmware](#section-firmware) |Arduino microcontroller written in C++
|[FarmBot OS](#section-farmbot-os)|Elixir
|[Rest API](#section-rest-api) |Ruby on Rails
|[Web App](#section-web-app)   |ReactJS, Typescript, and WebPack

# Which technologies must I learn to program a FarmBot?

For users who _only_ need to control a FarmBot, any language that provides the following will suffice:

 * An HTTP client for talking to the [REST API](../web-app/rest-api.md).
 * An MQTT client for talking to the [Message Broker](../web-app/message-broker.md)

If you wish to write a [Farmware](../farmware.md), Python is the only language currently supported, but [most developers do not need to write a Farmware](../farmware/you-might-not-need-farmware.md).

The document that follows is **not a list of required skills**. It would be **unrealistic for a new developer to learn all of these skills**. Instead, it is an inventory of all languages and tools used by the project. The tools that a developer will need to know will vary depending on the task at hand.

# Firmware

The [Firmware](https://github.com/FarmBot/farmbot-arduino-firmware) runs on an [Arduino microcontroller](https://farm.bot/shop/arduino-mega-2560/). It is written in C++.

The device firmware is often uploaded to the Arduino via FarmBot OS, but it can also be uploaded to the microcontroller via [AVRDude](https://www.nongnu.org/avrdude/).

# FarmBot OS

FarmBot OS is written in [Elixir](https://elixir-lang.org). It uses the [Nerves Framework](https://nerves-project.org) to compile the source code into a single binary image and also handle low-level details such as cross-compilation and driver management.

It communicates with the Web App via HTTP and [AMQP](https://www.amqp.org).

The source code for FarmBot OS is found [here](https://github.com/FarmBot/farmbot_os).

# REST API

The REST API is a [Ruby on Rails](https://rubyonrails.org) web server that stores data in a [PostgreSQL database](https://www.postgresql.org/about/) and uses [RabbitMQ](https://www.rabbitmq.com) for real-time messaging. It can be configured to store image data on local disc or on [Google Cloud Storage](https://cloud.google.com/storage/).

Aside from data storage and image manipulation, it also handles email delivery and user authorization.

The source code for the REST API is found [here](https://github.com/FarmBot/Farmbot-Web-App).

# Web App

The user interface is written in [ReactJS](https://reactjs.org) and [Typescript](https://www.typescriptlang.org). [WebPack](https://webpack.js.org) is used for compilation and asset management.

The Web App is found in [the same repository as the REST API](https://github.com/FarmBot/Farmbot-Web-App).

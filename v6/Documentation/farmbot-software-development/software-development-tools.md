---
title: "Software Development Tools Used By FarmBot"
slug: "software-development-tools"
---

* toc
{:toc}


{% include callout.html type="warning" title="Advanced Topics Ahead!" content="This listing is provided for reference purposes only. For most third-party software developers, in-depth knowledge of each component is not necessary. The information below is an implementation detail and is intended for developers who are curious about the inner workings of the software suite.

For example, although the REST API uses PostgreSQL as a storage mechanism, very few developers will directly interact with PostgreSQL.

Knowledge of inner components is not required for authorship of Farmware or API usage. It is merely an implementation detail for which knowledge is only required when modifying the core source code." %}

# Firmware

The [Firmware](https://github.com/FarmBot/farmbot-arduino-firmware) runs on an [Arduino microcontroller](https://farm.bot/shop/arduino-mega-2560/). It is written in C++ and is uploaded to the microcontroller via [AVRDude](https://www.nongnu.org/avrdude/).

# FarmBot OS

FarmBot OS is written in [Elixir](https://elixir-lang.org). It uses the [Nerves Framework](https://nerves-project.org) to compile the source code into a single binary image and also handle low-level details such as cross-compilation and driver management.

It communicates with the Web App via HTTP and [AMQP](https://www.amqp.org).

Here is the [GitHub-Repository of FarmBot OS](https://github.com/FarmBot/farmbot_os)

# REST API

The REST API is a [Ruby on Rails](https://rubyonrails.org) web server that stores data in a [PostgreSQL database](https://www.postgresql.org/about/) and uses [RabbitMQ](https://www.rabbitmq.com) for real-time messaging. It can be configured to store image data on local disc or on [Google Cloud Storage](https://cloud.google.com/storage/).

Aside from data storage and image manipulation, it also handles email delivery and user authorization.


# Web App

The user interface is written in [ReactJS](https://reactjs.org) and [Typescript](https://www.typescriptlang.org). [WebPack](https://webpack.js.org) is used for compilation and asset management.

The Web App and the REST API are in the same [repository](https://github.com/FarmBot/Farmbot-Web-App).

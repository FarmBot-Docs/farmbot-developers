---
title: "Frequently Asked Questions"
slug: "faq"
---

* toc
{:toc}

# Where can I download FarmBot source code?
Like most open source projects, we host our software on [GitHub](https://github.com/farmbot). Here are the most popular source code links:
  * [Web App](https://github.com/FarmBot/Farmbot-Web-App) (Ruby, Typescript) - Cloud storage, REST API and user interface.
  * [FarmBot OS](https://github.com/FarmBot/farmbot_os) (Elixir) - Embedded operating system that runs on the Raspberry Pi. The “glue” between the API, frontend and firmware.
  * [Firmware](https://github.com/FarmBot/farmbot-arduino-firmware) (C++) - Arduino source code. Controls stepper motors, pins, etc.

# Which technologies must I learn to program a FarmBot?
For users who _only_ need to control a FarmBot, any language that provides the following will suffice:

 * An HTTP client for talking to the [REST API](../web-app/rest-api.md).
 * An MQTT client for talking to the [Message Broker](../web-app/message-broker.md)

# Does the web API support ARM-based processors?
Not at this time. The only software that supports Raspberry Pi is FarmBot OS. Do not attempt to run a web server on a Raspberry Pi.

# What language is FarmBot written in?
FarmBot is comprised of many different software systems and the language used varies across projects. Generally speaking, we use a combination of C++, [Ruby](https://www.ruby-lang.org/en/), [Elixir](https://elixir-lang.org), and [TypeScript](https://www.typescriptlang.org).

# Do I need to know Elixir to program FarmBot?
No. The best approach is to write a standalone application that interacts with FarmBot externally via [REST API](../web-app/rest-api.md), [FarmBot JS](../farmbot-js.md) or the [Message Broker](../web-app/message-broker.md).

# Should I clone FarmBot OS on GitHub or use the image?
You almost certainly want the image. The only exception is if you plan on modifying the FarmBot OS source code.

# Why was my device blocked?
If your device attempts to connect to the message broker more than 20 times in a 10 minute period, it will be temporarily blocked from re-connecting. You will be able to reconnect after the 10 minute cool down period. This measure is put in place to protect server resources. Your device may be blocked from the server for a number of reasons:

 * (Most common) Your device does not have an adequately reliable internet connection, which is causing the device to reconnect to the network too often. This is commonly seen on cellular networks and in setups where the device is too far from the WiFi access point. **FarmBot requires a stable internet connection to function properly.** More information is available [here](https://software.farm.bot/docs/connecting-farmbot-to-the-internet).
 * (Less common) If you are a third party software developer, the error may be caused by bugs in third party software, such as code that connects to the MQTT broker within a loop. Ensure that your plugin or script does not leak TCP connections.

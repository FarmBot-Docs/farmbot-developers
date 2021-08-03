---
title: "FarmBot OS"
slug: "farmbot-os"
description: "The operating system and all related software that runs on FarmBot's Raspberry Pi. [GitHub repository](https://github.com/FarmBot/farmbot_os/)"
---

* toc
{:toc}


{%
include callout.html
type="info"
title="Trying to install FarmBot OS onto the microSD card?"
content="Please see [the consumer software documentation](https://software.farm.bot/docs/farmbot-os#installing-farmbot-os) for help."
%}

FarmBot OS is written in [Elixir](https://elixir-lang.org). It uses the [Nerves Framework](https://nerves-project.org) to compile the source code into a single binary image and also handle low-level details such as cross-compilation and driver management. It communicates with the Web App via HTTP and [AMQP](https://www.amqp.org).

# Building FarmBot OS from source
This project is written in the programming language Elixir and built using the Nerves Project framework.

{%
include callout.html
type="info"
title="Before you begin"
content="You will need a x64 bit non Windows machine to build FarmBot OS from source. We suggest the latest OSX or Ubuntu LTS."
%}

## Arduino firmware
FarmBot OS now bundles the [Arduino Firmware](https://github.com/farmbot/farmbot-arduino-firmware). This is compiled separately and bundled as a `.hex` file.

## Installing dependencies
If you have the above set up you will need the following software dependencies. Following [this guide](http://embedded-elixir.com/post/2017-05-23-using-asdf-vm/) will get you mostly setup.

|Dependency                    |Info                          |
|------------------------------|------------------------------|
|Erlang                        |Required
|Elixir                        |Required
|[Nerves Bootstrapper](https://hexdocs.pm/nerves/installation.html#Linux)|Required
|GNU Make + GCC                |Required
|Git                           |Required
|Arduino                       |Optional. You can do one of:<br>  * Set the `ARDUINO_INSTALL_DIR` environment variable<br><br>  * Execute `.circleci/setup_arduino.sh`
|Python                        |Optional
|opencv-python                 |Optional

# FarmBot and Compatible Cameras for the Raspberry Pi

Although FarmBot OS supports plug-and-play USB webcams, it is not possible to install additional camera drivers on FarmBot OS. FarmBot OS only supports plug-and-play cameras, and it's very important to point out that although FarmBot OS is a Linux-powered Raspberry Pi, it is not intended to be used in the same manner as a Desktop machine where end users are free to add and remove the software components running on the machine. This means that FarmBot OS is not capable of directly running specialized cameras intended for scientific or specialised use (most consumer-grade USB webcams are fine, though). FarmBot OS has a read-only filesystem and does not use the same Raspberry Pi Linux distribution that desktop Linux users are used to. In situations where you need to install special drivers or Python modules, we recommend adding a "sidecar" hardware module to the FarmBot. The sidecar computer would be a second Raspberry Pi (or similar) that is completely under your control and which does not run FarmBot OS. You would install Raspberry Pi OS on the sidecar and follow the directions provided by most tutorials found online.

Once the sidecar is configured, there are a number of ways you can support interaction between the FarmBot's CPU and the sidecar:

 * If the device has a reasonably reliable internet connection, you can have the sidecar talk to FBOS via [FarmBot.py](https://github.com/FarmBot/farmbot-py) or [FarmBot.js](https://github.com/FarmBot/farmbot-js). This is the easiest option.
 * You can run a serial line from the FarmBot to the sidecar and use the Lua [UART helpers](https://developer.farm.bot/v14/Documentation/lua.html#uartopenpath-baud) to send messages between the devices.
 * The sidecar can trigger a "pin binding" which activates a sequence on FBOS whenever the sidecar pulls a GPIO line high.
 * You could create an HTTP server that resides on the sidecar module and [make HTTP calls from Lua code in a sequence](https://developer.farm.bot/v14/Documentation/lua.html#httpparams)The sidecar module could then upload the photos to the FarmBot API, or you could store them on a completely different server that has higher storage limits than what the Web App provides. You could also perform image manipulation tasks directly on the sidecar.Other methods may be possible.

# What's next?

 * [Development](farmbot-os/farmbot-os-development.md)
 * [Gathering Information at Runtime](farmbot-os/gathering-information-at-runtime.md)
 * [Beta Updates](farmbot-os/beta-updates.md)
 * [Gathering a Log Dump](farmbot-os/gathering-a-log-dump.md)
 * [FAQ](farmbot-os/farmbot-os-faq.md)

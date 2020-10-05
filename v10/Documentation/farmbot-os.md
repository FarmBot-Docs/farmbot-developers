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

## Cloning
Farmbot OS now bundles and builds the [Arduino Firmware](https://github.com/farmbot/farmbot-arduino-firmware). This is bundled as a `git` submodule. To initialize the repository you can choose to do one of: `git clone https://github.com/FarmBot/farmbot_os.git --recursive` or
```bash
git clone https://github.com/FarmBot/farmbot_os.git
git submodule update --init --recursive
```

## Installing dependencies
If you have the above set up you will need the following software dependencies. Following [this guide](http://embedded-elixir.com/post/2017-05-23-using-asdf-vm/) will get you mostly setup.

|Dependency                    |Info                          |
|------------------------------|------------------------------|
|Erlang                        |Required
|Elixir                        |Required
|[Nerves Bootstrapper](https://hexdocs.pm/nerves/installation.html#Linux)|Required
|GNU Make + GCC                |Required
|Git                           |Required
|Arduino                       |Required. You can do one of:<br>  * Set the `ARDUINO_INSTALL_DIR` environment variable<br><br>  * Execute `.circleci/setup_arduino.sh`
|Python                        |Optional
|opencv-python                 |Optional


# What's next?

 * [Development](farmbot-os/farmbot-os-development.md)
 * [Gathering Information at Runtime](farmbot-os/gathering-information-at-runtime.md)
 * [Beta Updates](farmbot-os/beta-updates.md)
 * [Gathering a Log Dump](farmbot-os/gathering-a-log-dump.md)
 * [FAQ](farmbot-os/farmbot-os-faq.md)

---
title: "FarmBot OS"
slug: "farmbot-os"
excerpt: "[GitHub repository](https://github.com/FarmBot/farmbot_os/)"
---

* toc
{:toc}


{% include callout.html type="info" title="Trying to install FarmBot OS onto the microSD card?" content="Please see [the consumer software documentation](https://software.farm.bot/docs/farmbot-os#section-installing-farmbot-os) for help." %}

# Building FarmBot OS from source
This project is written in the programming language Elixir and built using the Nerves Project framework.

{% include callout.html type="info" title="Before you begin" content="You will need a x64 bit non Windows machine to build FarmBot OS from source. We suggest the latest OSX or Ubuntu LTS." %}

## Cloning
Farmbot OS now bundles and builds the [Arduino Firmware](https://github.com/farmbot/farmbot-arduino-firmware). This is bundled as a `git` submodule. To initialize the repository you can choose to do one of: `git clone https://github.com/FarmBot/farmbot_os.git --recursive` or
```bash
git clone https://github.com/FarmBot/farmbot_os.git
git submodule update --init --recursive
```

## Install dependencies
If you have the above set up you will need some software dependencies:
* Erlang
* Elixir
  * Nerves Bootstrapper found [here](https://hexdocs.pm/nerves/installation.html#Linux)
* GNU Make + GCC
* git
* Arduino. You can do one of:
  * Set the `ARDUINO_INSTALL_DIR` environment variable
  * execute `.circleci/setup_arduino.sh`

## Optional dependencies
* python
* opencv-python

Following [this](http://embedded-elixir.com/post/2017-05-23-using-asdf-vm/) guide will get you mostly setup.

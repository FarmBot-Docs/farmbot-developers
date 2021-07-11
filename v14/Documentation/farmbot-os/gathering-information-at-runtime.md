---
title: "Gathering Information at Runtime"
slug: "gathering-information-at-runtime"
---

* toc
{:toc}

There are multiple ways to gather information about FarmBot while it is running:

# FTDI cable
Almost all development for FarmBot OS is done using one of these. You can purchase one [here](https://www.adafruit.com/product/954). This will allow you to connect a PC to FarmBot to see very verbose logs about what is happening internally to FarmBot.

# SSH
As of the 6.4.10 beta release a debug SSH console was added. In the "Advanced Network Settings" menu during Configurator you will be able to add an SSH public key that you can connect with. See [this document](https://github.com/FarmBot/farmbot_os/blob/staging/docs/target_development/consoles/ssh.md) for usage.

# Connect a monitor
This is the least useful, but can help in a crunch. The same logs are displayed on the HDMI port, although you won't be able to scroll them, and you are stuck either copying them or taking a picture (preferred).

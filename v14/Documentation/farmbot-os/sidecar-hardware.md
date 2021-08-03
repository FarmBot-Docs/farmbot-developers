---
title: "Sidecar hardware"
slug: "sidecar-hardware"
description: "Adding additional specialized hardware to your FarmBot"
---

* toc
{:toc}

# FarmBot and Compatible Cameras for the Raspberry Pi

Although FarmBot OS supports plug-and-play USB webcams, it is not possible to install additional camera drivers on FarmBot OS. FarmBot OS only supports plug-and-play cameras, and it's very important to point out that although FarmBot OS is a Linux-powered Raspberry Pi, it is not intended to be used in the same manner as a Desktop machine where end users are free to add and remove the software components running on the machine. This means that FarmBot OS is not capable of directly running specialized cameras intended for scientific or specialized use (most consumer-grade USB webcams are fine, though). FarmBot OS has a read-only filesystem and does not use the same Raspberry Pi Linux distribution that desktop Linux users are used to. In situations where you need to install special drivers or Python modules, we recommend adding a "sidecar" hardware module to the FarmBot. The sidecar computer would be a second Raspberry Pi (or similar) that is completely under your control and which does not run FarmBot OS. You would install Raspberry Pi OS on the sidecar and follow the directions provided by most tutorials found online.

Once the sidecar is configured, there are a number of ways you can support interaction between the FarmBot's CPU and the sidecar:

 * If the device has a reasonably reliable internet connection, you can have the sidecar talk to FBOS via [FarmBot.py](https://github.com/FarmBot/farmbot-py) or [FarmBot.js](https://github.com/FarmBot/farmbot-js). This is the easiest option.
 * You can run a serial line from the FarmBot to the sidecar and use the Lua [UART helpers](../lua.md#uartopenpath-baud) to send messages between the devices.
 * The sidecar can trigger a "pin binding" which activates a sequence on FBOS whenever the sidecar pulls a GPIO line high.
 * You could create an HTTP server that resides on the sidecar module and [make HTTP calls from Lua code in a sequence](../lua.md#httpparams). The sidecar module could then upload the photos to the FarmBot API, or you could store them on a completely different server that has higher storage limits than what the Web App provides. You could also perform image manipulation tasks directly on the sidecar. Other methods may be possible.

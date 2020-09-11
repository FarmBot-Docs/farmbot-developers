---
title: "Why Was My Device Blocked?"
slug: "connectivity-issues"
hidden: false
createdAt: "2019-07-10T17:46:10.151Z"
updatedAt: "2019-07-16T20:25:06.060Z"
---
If your device attempts to connect to the message broker more than 20 times in a 10 minute period, it will be temporarily blocked from re-connecting. You will be able to reconnect after the 10 minute cool down period. This measure is put in place to protect server resources.

Your device may be blocked from the server for a number of reasons:

 * (Most common) Your device does not have an adequately reliable internet connection, which is causing the device to reconnect to the network too often. This is commonly seen on cellular networks and in setups where the device is too far from the WiFi access point. **FarmBot requires a stable internet connection to function properly.** More information is available [here](https://software.farm.bot/docs/connecting-farmbot-to-the-internet).
 * (Less common) If you are a third party software developer, the error may be caused by bugs in third party software, such as code that connects to the MQTT broker within a loop. Ensure that your plugin or farmware does not leak TCP connections.

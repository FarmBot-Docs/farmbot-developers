---
title: "You Might Not Need Farmware"
slug: "you-might-not-need-farmware"
hidden: false
createdAt: "2019-03-25T17:13:46.620Z"
updatedAt: "2019-12-13T05:09:03.253Z"
---

__Most developers do not need to use farmware:__
FarmBot has always supported remote control of devices without the need for Farmware. We recommend that third-party developers run custom software off the device as traditional software applications. Farmware development should be reserved for use cases with hard requirements that cannot otherwise be met.

Farmware is only one way to customize a device. Another, more convenient means of customizing a FarmBot is to write software that controls the device remotely. **For most device customization, you do not need to write Farmware**.

# Alternatives

The easiest way to control a FarmBot via software is to run the software on a dedicated desktop or server. Device control is possible via the [Message Broker](doc:message-broker). Remote access to device data is possible via the [REST API](doc:rest-api). For examples written in Python, see [Web App API Examples](doc:web-app-api-examples) and [Message Broker Examples](doc:message-broker-examples). There is also a [collection of Python-based examples here](https://github.com/FarmBot-Labs/FarmBot-Python-Examples) .

Unless there is a specific reason to do so, it is advisable to not run software on the device, excluding the edge cases listed in the following section. Running software on a FarmBot device will create a number of challenges that are easily avoided by running the software outside of the device.

# When to write a farmware

There are only a few use cases that _require_ a Farmware:

 * Applications that must operate regularly, even when the device is offline.
 * Applications where network delay creates unacceptable latency
   * Note: Benefits of reduced network latency may be negated by the lower CPU speed of the onboard CPU.

# Trade-offs

Farmware provides a number of benefits, such as:

 * Ability to operate software even when the device is offline.
 * Ability to send device commands without network overhead

Despite these advantages, there are some drawbacks to running software directly on the device:

 * FarmBot halts all other operations while a Farmware is running, which can lead to slowdowns in some cases.
 * Farmware is harder to debug than traditional off-device applications
 * Farmware is harder to upgrade and install than traditional off-device applications
 * Does not support third-party Python packages found on `pip`
 * Does not allow developers to pick a specific Python version
 * Does not support custom extensions written in C
 * Does not provide a real time interface or allow keyboard input

In the case that your application does not require offline support, **developing a Farmware does not add substantial benefit over a traditional off-device application.**

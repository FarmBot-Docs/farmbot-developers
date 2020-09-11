---
title: "Out-of-Band Responses"
slug: "out-of-band-responses"
hidden: false
createdAt: "2019-01-18T04:01:10.747Z"
---
Not every piece of data that FarmBot works with can be transmitted as CeleryScript. When an RPC creates data that is not formatted as CeleryScript, the response is said to be "out of band", meaning that it relays the information through a channel that does not support CeleryScript (typically the [REST API](doc:rest-api) or status channel on the [Message Broker](doc:message-broker)).

|                              |                              |
|------------------------------|------------------------------|
|`take_photo`                  |Creates an image resource in the [REST API](doc:rest-api) .
|`read_pin`                    |Updates the bot state tree and broadcasts over the appropriate status channel on the [Message Broker](doc:message-broker).
|`read_status`                 |Forces the bot to re-transmit the entire status tree over the appropriate channel on the [Message Broker](doc:message-broker).
|`sync`                        |Causes the bot to upload and download newly created resources on the [REST API](doc:rest-api).
|`dump_info`                   |Creates a device diagnostic report that is only visible to server admins for the sake of troubleshooting.



__This list is not exhaustive:__
If you have questions about a specific RPC, please raise an issue on [Github](https://www.github.com/farmbot) or [the forum](https://forum.farmbot.org/).


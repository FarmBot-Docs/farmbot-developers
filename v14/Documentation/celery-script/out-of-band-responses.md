---
title: "Out-of-Band Responses"
slug: "out-of-band-responses"
---

* toc
{:toc}

Not every piece of data that FarmBot works with can be transmitted as CeleryScript. When an RPC creates data that is not formatted as CeleryScript, the response is said to be "out of band", meaning that it relays the information through a channel that does not support CeleryScript (typically the [REST API](../web-app/rest-api.md) or status channel on the [Message Broker](../web-app/message-broker.md)).

|                              |                              |
|------------------------------|------------------------------|
|`take_photo`                  |Creates an image resource in the [REST API](../web-app/rest-api.md) .
|`read_pin`                    |Updates the bot state tree and broadcasts over the appropriate status channel on the [Message Broker](../web-app/message-broker.md).
|`read_status`                 |Forces the bot to re-transmit the entire status tree over the appropriate channel on the [Message Broker](../web-app/message-broker.md).
|`sync`                        |Causes the bot to upload and download newly created resources on the [REST API](../web-app/rest-api.md).



{%
include callout.html
type="info"
title="This list is not exhaustive"
content="If you have questions about a specific RPC, please raise an issue on [Github](https://www.github.com/farmbot) or [the forum](https://forum.farmbot.org/)."
%}


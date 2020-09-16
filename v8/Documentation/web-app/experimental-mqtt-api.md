---
title: "Publishing Resources via MQTT, Introduction"
slug: "experimental-mqtt-api"
---

* toc
{:toc}


{% include callout.html type="danger" title="Alpha Feature" content="The feature described below is **highly experimental**. Feedback is appreciated, but please **do not write mission critical code with this feature**. We reserve the right to change the API (or remove it) without notice.

It is also important to note that **the API described below is not a replacement for the REST API yet**. Some features are still missing." %}

# Updating Resources over MQTT

In the previous section, we learned how to _read_ resources over MQTT. This section will cover an experimental feature that allows developers to _modify and create_ resources over MQTT.

This feature was inspired by requests from application developers who wanted to manage resources over one unified protocol rather than HTTP and MQTT.

# Important Notes

 * This is a new feature. Official software packages do not yet rely on MQTT updates and there may still be undiscovered bugs. For applications requiring higher levels of stability, consider using the [REST API](/v8/Documentation/web-app/rest-api.md) for data modification.
 * The feature set is not complete yet. It is not a drop-in replacement for the REST API in all use cases. A full list of supported resources is available [in the API source code](https://github.com/FarmBot/Farmbot-Web-App/blob/staging/app/lib/resources.rb#L5).


**If you experience problems with this new feature, please report bugs [here](https://github.com/FarmBot/Farmbot-Web-App/issues/new?title=MQTT%20API%20Problems)**

# Limitations of HTTP

The [REST API](/v8/Documentation/web-app/rest-api.md) is an appropriate solution for most resource management operations.

It does suffer some drawbacks in some circumstances, though:

 * Performing many updates requires many HTTP requests. The overhead of an HTTP request wastes bandwidth and CPU time.
 * Maintaining two client libraries (HTTP, MQTT) is inconvenient for developers whose applications only require light resource management. **Important note:** The MQTT resource update API is not yet a replacement for REST in all use cases.

# Solution

To address the issues above, the API exposes an experimental feature to update resources via MQTT. This feature is **currently not a replacement for HTTP in all use cases**. Some resources, such as `ToolSlot` are not yet supported. A full list of supported resources is available [in the API source code](https://github.com/FarmBot/Farmbot-Web-App/blob/staging/app/lib/resources.rb#L5).

# Next Steps

[Create, Update and Delete a Resource via MQTT](/v8/Documentation/web-app/create-a-resource.md)

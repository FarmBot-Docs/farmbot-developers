---
title: "Python"
slug: "intro"
description: "Use Python to communicate directly with FarmBot and the API"
---

FarmBot, Inc. provides a Python wrapper library, [**farmbot-py**](https://github.com/FarmBot/farmbot-py), that provides authentication and communication utilities for communicating with FarmBot devices directly via the [message broker](../docs/message-broker.md) and for manipualting account data stored in the FarmBot Web App via the [REST API](../docs/web-app/rest-api.md).

The library can be used when running Python code from another device such as a laptop, server, or another Raspberry Pi. The library's functions cannot currently be used to run code on the FarmBot device itself.

# Getting started

To start a project using the FarmBot Python library, create and activate a virtual environment and install the `farmbot` package:

```bash
python3 -m venv py_venv
source py_venv/bin/activate
python -m pip install --upgrade farmbot
```

The library can then be used via `from farmbot import Farmbot` as shown in examples in the following pages.

{%
include callout.html
type="info"
title="Options available"
content='When applicable, the following pages provide usage examples of the FarmBot Python library. Examples without usage of the FarmBot library are also provided.'
%}

# What's next?

 * [Authorization](authorization.md)
 * [Settings](settings.md)
 * [Functions](functions.md)
 * [Examples](examples.md)

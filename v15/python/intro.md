---
title: "Python"
slug: "intro"
description: "Use Python to communicate directly with FarmBot"
---

FarmBot, Inc. provides a Python wrapper library, [`farmbot-py`](https://github.com/FarmBot/farmbot-py).

{%
include callout.html
type="info"
title="Options available"
content='When applicable, the following pages provide usage examples of the FarmBot Python library. without usage of the FarmBot library are also provided.'
%}

# Getting started

In a command line terminal, run:
```bash
python3 -m venv py_venv
source py_venv/bin/activate
python -m pip install farmbot
```

This will install the FarmBot Python library into your environment so that it can be used via `from farmbot import Farmbot` as shown in examples.

# What's next?

 * [Authorization](authorization.md)
 * [Examples](examples.md)
 * [Functions](functions.md)
 * [Settings](settings.md)

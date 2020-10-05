---
title: "Common Farmware Problems"
slug: "common-farmware-problems"
description: "Troubleshooting tips"
---

* toc
{:toc}


# Farmware installation failed

Verify the following:
* The URL you are providing for installation points to the __raw__ Farmware `manifest.json` file. (If using GitHub to host your Farmware, the URL should start with `https://raw.githubusercontent.com/`.)
* The `manifest.json` file is valid JSON.
* The `zip` URL in `manifest.json` points to the __raw__ `.zip` file including your Farmware code.
* The Farmware manifest is compatible with the FarmBot OS version used.

# Farmware execution failed

There are several ways to determine what went wrong:
* Try running the Farmware code on your computer. (`pip install --user farmware_tools` first if you are using Farmware Tools. See [more about Farmware Tools](../farmware.md#more-about-farmware-tools) for details.)
* Use an FTDI cable to view low-level device logs. `stdout` and `stderr` are sent here.
* Try catching the error as shown below. This method will not catch syntax errors, and should be used only for temporary debugging purposes on the device.


```python
import farmware_tools

try:
    code
except Exception as error:
    farmware_tools.device.log(repr(error))
```

Only a few specific packages outside of the standard library are available to Farmware. See [currently supported languages and packages](../farmware.md#currently-supported-languages-and-packages) for a complete list.

# Farmware input issues

Verify the following:
 * The `farmware_name` provided to `farmware_tools.get_config_value` matches the value for `package` (`package_version`) in `manifest.json`.
 * The `config_name` provided to `farmware_tools.get_config_value` matches the value for the `config` in `manifest.json`.

{%
include callout.html
type="info"
title=""
content="See [Hello Farmware Input](https://github.com/FarmBot-Labs/hello-farmware-input) for an example."
%}



# The web UI is unresponsive when I run my Farmware

Here are some facts to keep in mind when developing a _performant_ Farmware:

 * A log message (or RPC) requires a screen update at the UI layer.
 * An update to the bot's state (such as a change in the `sync_status`)  requires a screen update at the UI layer.
 * A screen update requires CPU resources

Therefore, an unusually high number of log messages (or operation causing the bot’s state to change too often, such as polling) will consume all of the browsers CPU resources.

Some things to look for are:

 * Sending too many RPC messages at one time
 * Sending too many logs
 * Performing a polling operation (Doing RPCs on a timer)

{%
include callout.html
type="info"
title="Sending too many logs?"
content="A warning sign that you are sending too many logs is that the server \"throttles\" your device.
You will receive a message similar to this if you are throttled:  `\"Device is sending too many logs (%s). Suspending log storage and display until %s.\"`"
%}

## How to fix a slow Farmware

 * Avoid sending excessive logs
 * Consider using an event-based architecture instead of performing [polling](https://en.wikipedia.org/wiki/Polling_computer_science). With few exceptions, **polling (particularly across a network) is almost always an architectural mistake**.

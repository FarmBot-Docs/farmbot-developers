---
title: "FarmBot Sidecar Starter Pack"
slug: "sidecar-starter-pack"
description: "Use Python to communicate directly with FarmBot"
---

This library provides authentication, API, and control utilities for **FarmBot sidecars**. A **sidecar** is another computer such as a Raspberry Pi, laptop, or server that you are in full control of to install your own packages onto and run your own code, unlocking what cannot be done using FarmBot OS or the web app alone. For example, a sidecar could:

- Extend the capabilities of your FarmBot with specialized hardware such as a GPU, or a camera or other sensor requiring special drivers.
- Expose your FarmBot's hardware capabilities as a device in a larger ecosystem such as one for home automation or scientific research.
- Perform more advanced manipulation of your web app account's data which may be infeasible using the frontend interface.

See the [sidecar hardware documentation](../docs/farmbot-os/sidecar-hardware.md) for more information about sidecars.

# :computer: Installation

To use the sidecar starter pack, follow these steps:

(1) Create a virtual environment.
```bash
python -m venv py_venv
```

(2) Activate the virtual environment.
```bash
source py_venv/bin/activate
```

(3) Install the farmbot-sidecar-starter-pack library within the virtual environment:
```bash
python -m pip install farmbot-sidecar-starter-pack
```

# :seedling: Getting Started

Import `farmbot_sidecar_starter_pack` and create an instance of the Farmbot class:
```python
from farmbot_sidecar_starter_pack import Farmbot
fb = Farmbot()
```

## Get your authentication token

Use the same login credentials associated with the web app account you are interacting with. The server is "https://my.farm.bot" by default.
```python
token = fb.get_token("email", "password")
```

To avoid storing your account credentials in plaintext, you can print your token:
```python
print(token)
```

and then delete the `fb.get_token("email", "password")` line and set your token directly instead:
```python
token = {'token': {'unencoded': {'aud': ...
fb.set_token(token)
```

where the part after `token = ` is the entire token pasted from the `print(token)` output. The start should look similar to the value above.

{%
include callout.html
type="warning"
title="Storing your authorization token"
content="Store your authorization token securely. It grants full access and control over your FarmBot and your FarmBot Web App account."
%}

## Configure function output verbosity

Set the level of verbosity of function outputs to change the level of information shown when functions are called.
```python
fb.set_verbosity(2)
```

| Verbosity | Example using `e_stop()` |
| :--- | :--- |
| `0` The function will return with no output. | No output. |
| `1` A description of the action will be output with any additional results data. | `Emergency stopping device` |
| `2` The name of the function and the timestamp will be output. | `'e_stop()' called at: 2024-08-21 11:16:18.547813` |

## Configure timeouts

If you expect movements to take longer than the default timeout duration of 120 seconds, you can increase the movement timeout via:
```python
fb.set_timeout(240, "movements")
```

| Key | Default value in seconds | Description |
| :--- | :--- | :--- |
| `movements` | `120` | Timeout for movement commands. |
| `api` | `15` | Timeout for API requests. |
| `listen` | `15` | Message broker listen duration, used while waiting for a response for many sidecar commands. |

## Clear resource cache

To reduce duplicate API requests, some information used frequently to look up peripheral, sensor, tool, and sequence IDs is cached.

The cache will be automatically cleared when a resource is not found (for example, `fb.read_sensor("Not a valid sensor")`). To clear the cache manually, call:
```python
fb.clear_cache()
```

## Example: Add a new plant to your garden

This test will help familiarize you with sending commands via the [API](../docs/web-app/rest-api.md).
```python
new_cabbage = {
    "name": "Cabbage",              # Point name
    "pointer_type": "Plant",        # Point type
    "x": 400,                       # x-coordinate
    "y": 300,                       # y-coordinate
    "z": 0,                         # z-coordinate
    "openfarm_slug": "cabbage",     # Plant type
    "plant_stage": "planned",       # Point status
}

fb.api_post("points", new_cabbage) # Add plant to endpoint
```

## Example: Turn your LED strip on and off

This test will help familiarize you with sending commands via the [Message Broker](../docs/message-broker.md).
```python
fb.on(7)           # Turn ON pin 7 (LED strip)
fb.wait(2000)      # Wait 2000 milliseconds
fb.off(7)          # Turn OFF pin 7 (LED strip)
```

## Additional examples

For more examples that expand upon your FarmBot's capabilities, see [the examples on GitHub](https://github.com/FarmBot-Labs/sidecar-starter-pack/tree/main/examples).

# What's next?

 * [API](sidecar-starter-pack/api.md)
 * [Message Broker](sidecar-starter-pack/message-broker.md)
 * [Configuration](sidecar-starter-pack/configuration.md)
 * [Coordinates](sidecar-starter-pack/coordinates.md)
 * [Curves](sidecar-starter-pack/curves.md)
 * [E-Stop and Unlock](sidecar-starter-pack/e-stop-and-unlock.md)
 * [Images](sidecar-starter-pack/images.md)
 * [Jobs](sidecar-starter-pack/jobs.md)
 * [Messages](sidecar-starter-pack/messages.md)
 * [Movements](sidecar-starter-pack/movements.md)
 * [Pins](sidecar-starter-pack/pins.md)
 * [Tools](sidecar-starter-pack/tools.md)
 * [Time](sidecar-starter-pack/time.md)
 * [Advanced](sidecar-starter-pack/advanced.md)

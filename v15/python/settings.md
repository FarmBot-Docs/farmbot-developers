---
title: "Python Library Settings"
slug: "settings"
description: "Configure verbosity, timeouts, and cache settings for the FarmBot Python library"
---

# Configure function output verbosity

Set the level of verbosity of function outputs to change the level of information shown when functions are called.

```python
fb.set_verbosity(2)
```

| Verbosity | Example using `e_stop()` |
| :--- | :--- |
| `0` The function will return with no output. | No output. |
| `1` A description of the action will be output with any additional results data. | `Emergency stopping device` |
| `2` The name of the function and the timestamp will be output. | `'e_stop()' called at: 2024-08-21 11:16:18.547813` |

# Configure timeouts

If you expect movements to take longer than the default timeout duration of 120 seconds, you can increase the movement timeout via:

```python
fb.set_timeout(240, "movements")
```

| Key | Default value in seconds | Description |
| :--- | :--- | :--- |
| `movements` | `120` | Timeout for movement commands. |
| `api` | `15` | Timeout for API requests. |
| `listen` | `15` | Message broker listen duration, used while waiting for a response for many FarmBot Python library commands. |

# Clear resource cache

To reduce duplicate API requests, some information used frequently to look up peripheral, sensor, tool, and sequence IDs is cached.

The cache will be automatically cleared when a resource is not found (for example, `fb.read_sensor("Not a valid sensor")`). To clear the cache manually, call:

```python
fb.clear_cache()
```

# What's next?

 * [Functions](functions.md)
 * [Examples](examples.md)

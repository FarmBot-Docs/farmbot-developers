---
title: "Advanced"
slug: "advanced"
description: "List of advanced Python functions in the FarmBot Python library"
---

# sequence(name)

**Executes a subsequence** by name.

```python
# Execute a subsequence
fb.sequence("My Sequence")
```

{%
include callout.html
type="info"
content="Sequence ID lookups are cached. See [clearing the cache](../settings.md#clear-resource-cache)."
%}

# reboot()

**Reboots the device**.

```python
# Reboot the device
fb.reboot()
```

# shutdown()

**Shuts down the device**.

{%
include callout.html
type="warning"
content="You will need to unplug and plug the FarmBot back in to turn it back on."
%}

```python
# Shut down the device
fb.shutdown()
```

# set_home(axis="all")

`axis` can be one of `"x"`, `"y"`, `"z"`, or `"all"`.

**Sets the current position as home** for the given axis or all axes.

```python
# Set the current position as home for all axes
fb.set_home()
```

# connect_broker()

Establish a persistent connection to send messages via the [message broker](../../docs/message-broker.md).

```python
fb.connect_broker()
```

# disconnect_broker()

Disconnect from the [message broker](../../docs/message-broker.md).

```python
fb.disconnect_broker()
```

# publish(message)

Publish a message to the [message broker](../../docs/message-broker.md).

{%
include callout.html
type="info"
content="Messages sent over the [message broker](../../docs/message-broker.md) must be properly formatted **Celery Script**. [See the docs here](../../docs/celery-script.md)."
%}

```python
fb.publish({"kind": "wait", "args": {"milliseconds": 500}})

# Note: this is equivalent to the following command:
fb.wait(500)
```

# lua(lua_code)

**Executes a Lua script** on the FarmBot.

```python
# Execute a Lua script
fb.lua("wait(5000)")
```

# if_statement(variable, operator, value, then_sequence_name=None, else_sequence_name=None, named_pin_type=None)

**Executes a sequence based on a conditional statement**.

{%
include callout.html
type="info"
content="The conditional statement will be evaluated by the FarmBot device rather than your Python code."
%}

| Argument | Description |
| --- | --- |
| `variable` | `"x"`, `"y"`, `"z"`, one of `"pin0"` through `"pin69"`, or a sensor or peripheral name. If using a sensor or peripheral name, `named_pin_type` must be specified. |
| `operator` | `"<"`, `">"`, `"is"`, `"not"`, `"is_undefined"` |
| `value` | integer |
| `then_sequence_name` | The name of the sequence to execute if the condition is true. |
| `else_sequence_name` | The name of the sequence to execute if the condition is false. |
| `named_pin_type` | `"Sensor"` or `"Peripheral"`, if using a sensor or peripheral name for `variable` |

```python
# If the soil moisture sensor reading is greater than 500, execute the "Water Plant" sequence
fb.if_statement("Soil Moisture", ">", 500, then_sequence_name="Water Plant", named_pin_type="Sensor")
```

{%
include callout.html
type="info"
content="Sequence ID lookups are cached. See [clearing the cache](../settings.md#clear-resource-cache)."
%}

# assertion(lua_code, assertion_type, recovery_sequence_name=None)

**Executes a sequence based on an assertion**.

| Argument | Description |
| --- | --- |
| `lua_code` | A Lua script that will be evaluated by the FarmBot device. The return value will determine if the assertion passes or fails. |
| `assertion_type` | `"abort"`, `"recover"`, `"abort_recover"`, `"continue"` |
| `recovery_sequence_name` | The name of the sequence to execute if the assertion fails. |

```python
fb.assertion("return 2 + 2", "recover", recovery_sequence_name="Find Home")
```

{%
include callout.html
type="info"
content="Sequence ID lookups are cached. See [clearing the cache](../settings.md#clear-resource-cache)."
%}

# What's next?

 * [Examples](../examples.md)

---
title: "Pins"
slug: "pins"
description: "List of pin Python functions in the FarmBot Python library"
---

# on(pin_number)

**Sets the state of the given pin to digital `1`**, also known as "high" or "on".

```python
# Turn on the lighting peripheral
fb.on(7)
```

# off(pin_number)

**Sets the state of the given pin to digital `0`**, also known as "low" or "off".

```python
# Turn off the lighting peripheral
fb.off(7)
```

# read_pin(pin_number, mode="digital")

**Reads the given pin** with the read mode `analog` or `digital`. Defaults to `digital` if no mode is given.

{%
include callout.html
type="info"
content="Calling `read_pin()` does not record the reading in the API, it only reads the pin."
%}

```python
# Read pin 23 in digital mode
fb.read_pin(23)

# Read pin 23 in digital mode (alternative syntax)
fb.read_pin(23, "digital")

# Read pin 25 in analog mode
fb.read_pin(25, "analog")
```

# read_sensor(sensor_name)

**Reads the given sensor**.

```python
# Read the soil moisture sensor
fb.read_sensor("Soil Moisture")
```

{%
include callout.html
type="info"
content="Sensor ID lookups are cached. See [clearing the cache](../settings.md#clear-resource-cache)."
%}

# control_peripheral(peripheral_name, value, mode=None)

**Sets the state of the given peripheral**.

```python
# Turn on the LED peripheral
fb.control_peripheral("LED", value=1, mode="digital")
```

{%
include callout.html
type="info"
content="Peripheral ID lookups are cached. See [clearing the cache](../settings.md#clear-resource-cache)."
%}

# toggle_peripheral(peripheral_name)

**Toggles the state of the given peripheral** between digital `1` (on) and `0` (off).

{%
include callout.html
type="info"
content="If the pin is initially set to an analog value, it will be rounded to the nearest digital value and then toggled."
%}

```python
# Toggle the LED peripheral
fb.toggle_peripheral("LED")
```

{%
include callout.html
type="info"
content="Peripheral ID lookups are cached. See [clearing the cache](../settings.md#clear-resource-cache)."
%}

# write_pin(pin_number, value, mode="digital")

**Sets a pin to a particular mode and value.**

```python
# Set pin 13 to digital mode and write a value of 1
fb.write_pin(13, value=1, mode="digital")

# Set pin 13 to analog mode and write a value of 128
fb.write_pin(13, value=128, mode="analog")
```

# control_servo(pin, angle)

**Controls a servo motor** connected to the given pin by setting the angle.

```python
# Set the servo motor connected to pin 4 to 90 degrees
fb.control_servo(4, angle=90)
```

# What's next?

 * [Tools](./tools.md)

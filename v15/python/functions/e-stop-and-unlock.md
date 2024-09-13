---
title: "E-Stop and Unlock"
slug: "e-stop-and-unlock"
description: "List of E-stop and Unlock Python functions in the FarmBot Python library"
---

# e_stop()

**Emergency locks** (E-stops) the Farmduino microcontroller, preventing motor and peripheral usage, and resetting peripheral pins to OFF.

{%
include callout.html
type="info"
content="Features that do not rely on the microcontroller, such as sending messages and taking photos, are still available while emergency locked."
%}

```python
# Lock (E-stop) the device:
fb.e_stop()
```

# unlock()

**Unlocks** a locked (E-stopped) device.

```python
# Unlock the device:
fb.unlock()
```

# What's next?

 * [Images](./images.md)

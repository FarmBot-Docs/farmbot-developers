---
title: "Time"
slug: "time"
description: "List of time Lua functions in FarmBot OS"
---

# wait(ms)

Pause execution for a certain number of milliseconds. **Crashes if the value is three minutes or greater.**

```lua
-- wait for 1 second:
wait(1000)
```

# current_month / current_hour / current_minute / current_second

Returns a number representing the current month, hour, minute, or second.
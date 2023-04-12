---
title: "Time"
slug: "time"
description: "List of time Lua functions in FarmBot OS"
---

# wait(milliseconds, params?)

**Pauses execution** for a certain number of milliseconds. If the value is greater than 1000 milliseconds, a job will be created to track the progress of the wait in the jobs popup. You can optionally pass in job name and status parameters to customize the display of the job to end users.

```lua
-- Wait for 500 milliseconds
wait(500)

-- Wait for 5 seconds (will create a job)
wait(5000)

-- Wait for 10 seconds with a custom job name and status
wait(10000, {job = "Passing the time", status = "Watching paint dry"})
```

# current_month()

**Returns a number representing the current month** where January is `1` and December is `12`.

```lua
-- Print the current month
toast(current_month())
```

# current_hour()

**Returns a number representing the current hour** in UTC in 24-hour format. For example, 1:00 PM would return `13`.

```lua
-- Print the current hour
toast(current_hour())
```

# current_minute()

**Returns a number representing the current minute**. For example, 1:30 PM would return `30`.

```lua
-- Print the current minute
toast(current_minute())
```

# current_second()

**Returns a number representing the current second**. For example, 1:30:45 PM would return `45`.

```lua
-- Print the current second
toast(current_second())
```

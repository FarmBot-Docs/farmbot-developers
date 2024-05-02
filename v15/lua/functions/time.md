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

# utc()

**Returns the current UTC date and time, or parts of it.**

```lua
--Print the current UTC date and time in ISO 8601 format.
toast(utc())
--Print the current UTC year. For example, `2024`.
toast(utc("year"))
--Print the current UTC month, where January is `1` and December is `12`.
toast(utc("month"))
--Print the current UTC day of the month. For example, `31`.
toast(utc("day"))
--Print the current UTC hour. For example, 1:30:05 PM would return `13`.
toast(utc("hour"))
--Print the current UTC minute. For example, 1:30:05 PM would return `30`.
toast(utc("minute"))
--Print the current UTC second. For example, 1:30:05 PM would return `5`.
toast(utc("second"))
```

# local_time()

**Returns the current local date and time, or parts of it, according to your FarmBot's `timezone`.**
You can view your FarmBot's timezone via `toast(get_device("timezone"))` or in [FarmBot settings](https://software.farm.bot/docs/farmbot-settings).

```lua
--Print the current local local date and time in ISO 8601 format.
toast(local_time())
--Print the current local year. For example, `2024`.
toast(local_time("year"))
--Print the current local month, where January is `1` and December is `12`.
toast(local_time("month"))
--Print the current local day of the month. For example, `31`.
toast(local_time("day"))
--Print the current local hour. For example, 1:30:05 PM would return `13`.
toast(local_time("hour"))
--Print the current local minute. For example, 1:30:05 PM would return `30`.
toast(local_time("minute"))
--Print the current local second. For example, 1:30:05 PM would return `5`.
toast(local_time("second"))
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

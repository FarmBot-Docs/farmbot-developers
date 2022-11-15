---
title: "Jobs"
slug: "jobs"
description: "List of jobs Lua functions in FarmBot OS"
---

# set_job_progress()

Creates a new job in the jobs popup. This is useful for tracking long running tasks such a photo grids.

```lua
start_time = os.time() * 1000

set_job_progress("Scan the garden", {
  status = "working",
  percent = 12.3,
  time = start_time
})

-- Another string argument, type, can also be added to the job, though this field is no longer used by the FarmBot web app frontend.
```

# get_job_progress()

Gets the job by name.

```lua
job = get_job_progress("Scan the garden")
send_message("debug", "Job progress: " .. job.percent, "toast")
```
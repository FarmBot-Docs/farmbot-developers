---
title: "Jobs"
slug: "jobs"
description: "List of jobs Lua functions in FarmBot OS"
---

# set_job_progress()

**Creates or updates a job** in the jobs popup. This is useful for tracking long running tasks such as photo grids.

```lua
start_time = os.time() * 1000

set_job_progress("Scan the garden", {
  status = "Working",
  percent = 50,
  time = start_time
})

wait(2000)

set_job_progress("Scan the garden", {
  status = "Complete",
  percent = 100,
  time = start_time
})
```

{%
include callout.html
type="info"
content="Another string argument, `type`, can also be added to the job, though this field is no longer used by the FarmBot web app frontend."
%}

# get_job_progress()

**Gets a job** by name.

```lua
-- Get a job:
job = get_job_progress("Job name")
```

```lua
start_time = os.time() * 1000

set_job_progress("Scan the garden", {
  status = "Working",
  percent = 50,
  time = start_time
})

job = get_job_progress("Scan the garden")
toast("Job progress: " .. job.percent .. "%")
```

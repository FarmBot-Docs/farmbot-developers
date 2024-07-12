---
title: "Jobs"
slug: "jobs"
description: "List of jobs Lua functions in FarmBot OS"
---

# set_job(name, params?)

**Creates or updates a job** in the [jobs popup](https://software.farm.bot/docs/jobs-and-logs). This is useful for tracking long running tasks such as photo grids.

The `params` argument is an optional table with the following optional fields: `status`, `percent`, and `time`. When a job is first created, it will initialize with a `status` of `Working`, a `percent` of `0`, and a `time` set to the current time, unless explicitly defined otherwise.

Subsequent calls to `set_job()` will only update the provided fields.

```lua
-- Create a job:
local job_name = "Scan the garden"
set_job(job_name)

wait(2000)

-- Update the job's status and percent:
set_job(job_name, {
  status = "Still working...",
  percent = 50
})

wait(2000)

-- Update just the job's percent:
set_job(job_name, {
  percent = 75
})

wait(2000)

-- Complete the job:
complete_job(job_name)
```

# set_job_progress()

{%
include callout.html
type="warning"
title="Deprecated"
content="This is a low-level function that has been superseded by [set_job()](#set_jobname-params)."
%}

# get_job(name)

**Gets a job** by name.

```lua
-- Get a job:
job = get_job("Job name")
```

```lua
local job_name = "Scan the garden"

set_job(job_name, {
  percent = 50
})

job = get_job(job_name)
toast("Job progress: " .. job.percent .. "%")

complete_job(job_name)
```

# get_job_progress()

{%
include callout.html
type="warning"
title="Deprecated"
content="This is a low-level function that has been superseded by [get_job()](#get_jobname)."
%}

# complete_job(name)

**Completes a job** by name, where complete means a `percent` of `100` and a `status` of `Complete`.

```lua
-- Complete a job:
complete_job("Job name")
```

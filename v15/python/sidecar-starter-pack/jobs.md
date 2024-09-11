---
title: "Jobs"
slug: "jobs"
description: "List of jobs Python functions in the FarmBot Sidecar Starter Pack"
---

# set_job(job_name, status="Working", percent=0)

**Creates or updates a job** in the [jobs popup](https://software.farm.bot/docs/jobs-and-logs). This is useful for tracking long running tasks such as photo grids.

```python
# Create a job:
local job_name = "Scan the garden"
fb.set_job(job_name)

fb.wait(2000)

# Update the job's status and percent:
fb.set_job(job_name, status="Still working...", percent=50)

fb.wait(2000)

# Update just the job's percent:
fb.set_job(job_name, percent=75)

fb.wait(2000)

# Complete the job:
fb.complete_job(job_name)
```

# get_job(job_name=None)

**Gets a job** by name.

```python
# Get a job:
job = fb.get_job("Job name")
```

```python
job_name = "Scan the garden"

fb.set_job(job_name, percent=50)

job = fb.get_job(job_name)
fb.toast(f"Job progress: {job['percent']}%")

fb.complete_job(job_name)
```

```python
# Get all jobs:
jobs = fb.get_job()
```

# complete_job(name)

**Completes a job** by name, where complete means a `percent` of `100` and a `status` of `Complete`.

```python
# Complete a job:
fb.complete_job("Job name")
```

# What's next?

 * [Messages](./messages.md)

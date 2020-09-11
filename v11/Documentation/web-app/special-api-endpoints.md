---
title: "Special API Endpoints"
slug: "special-api-endpoints"
hidden: false
createdAt: "2019-06-11T16:30:32.480Z"
updatedAt: "2019-09-30T23:17:06.714Z"
---
The REST API is relatively uniform in how it handles resources. There are some exceptions, however.

# Tool slots, points, and plants

All `tool_slots`, `plants` and `points` fall under the same API endpoint: `/api/points`

# Bulk deletion of points

Unlike many other API endpoints, the `points` endpoint supports bulk deletion. It is possible to delete many point resources in one request by separating many point IDs with a comma. Example:

```
DELETE https://farm.bot/api/points/1,4,23
```

# Filtering archived points

When points are deleted, it is still possible to view them for 2 months after the time of deletion. This is useful for tools relating to weeding and historical records.

The `/api/points/` endpoint supports a special `?filter=` [query parameter](https://en.wikipedia.org/wiki/Query_string). There are three options for this parameter:

  * `?filter=all` returns archived and active points.
  * `?filter=old` only returns archived points.
  * `?filter=kept` only returns active (not-archived) points. **This is the default behavior for index (`/api/points`) endpoint.**

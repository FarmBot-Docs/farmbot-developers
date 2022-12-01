---
title: "Tools"
slug: "tools"
description: "List of tool Lua functions in FarmBot OS"
---

# dismount_tool()

Dismounts the currently mounted tool into it's assigned slot.

```lua
dismount_tool()
find_home()
```

{%
include callout.html
type="info"
content="This helper function should only be used with FarmBots that have a universal tool mount and interchangeable tools, such as FarmBot Genesis."
%}

# mount_tool(tool)

Mounts the tool provided in the argument.

```lua
-- It is recommended to Find Home before mounting tools to ensure accuracy of movements.
find_home()

-- Add a Location variable named "Tool" to the sequence and select the tool you wish to mount.
tool = variable("Tool")

-- Because tools themselves do not have coordinates, FarmBot will look up which slot the chosen tool has been assigned to and use the slot's coordinates in the mount_tool() function.
mount_tool(tool)
```

{%
include callout.html
type="info"
content="This helper function should only be used with FarmBots that have a universal tool mount and interchangeable tools, such as FarmBot Genesis."
%}

# verify_tool()

Checks the UTM’s tool verification pin as well as the **MOUNTED TOOL** field in FarmBot’s state tree to verify if a tool is mounted to the UTM. Note that this functionality is built-in to the `mount_tool()` and `dismount_tool()` helpers.

```lua
-- Exit sequence if tool verification fails (no tool)
if not verify_tool() then
  return
end
```

{%
include callout.html
type="info"
content="This helper function should only be used with FarmBots that have a universal tool mount and interchangeable tools, such as FarmBot Genesis."
%}

---
title: "Copy Plants to New Account"
slug: "copy-plants-to-new-account"
description: "Use the FarmBot Python library to copy all plants from one FarmBot account to another"
---

This example script will copy all plants from one FarmBot account to another. This demonstrates how to use the FarmBot Python library to interact with the FarmBot Web App REST API and is not meant to serve as a full account backup or cloning tool.

{%
include callout.html
type="info"
title="Limitations apply
content="The script will not copy any water, height, or spread curves ids associated with a plant because the curve resources will not exist in the target account."
%}

```python
from farmbot import Farmbot
from time import sleep

source = Farmbot()
target = Farmbot()

source.get_token("user@email.com", "password", "https://my.farm.bot")
target.get_token("newuser@email.com", "password", "https://example.com")

source.set_verbosity(0)
target.set_verbosity(0)

# Get all points from the API.
# Note this will include plants, weeds, generic points, and tools.
points = source.api_get("points")

# Filter out only the plants
plants = [point for point in points if point["pointer_type"] == "Plant"]

# Copy each plant to the target account
for plant in plants:

    # Only copy the relevant fields
    plant_copy = {key: plant[key] for key in [
        "name",
        "pointer_type",
        "x",
        "y",
        "z",
        "openfarm_slug",
        "plant_stage",
        "planted_at",
        "radius",
        "depth"
    ]}

    # Print the progress
    plant_details = f"{plant["name"]} at ({plant["x"]}, {plant["y"]}, {plant["z"]})"
    progress = f"{plants.index(plant) + 1}/{len(plants)}"
    print(f"{progress} Copying {plant_details} to target account...")

    # Add the plant to the target account
    target.api_post("points", plant_copy)
    sleep(0.5)
```

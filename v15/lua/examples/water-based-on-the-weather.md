---
title: "Water Based on the Weather"
slug: "water-based-on-the-weather"
description: "Get today's forecast to water more efficiently based on the weather and each plant's needs"
---

In this example we'll get today's **weather forecast** from an external service based on your FarmBot's latitude and longitude. We'll then determine if we should water a plant based on its age and watering curve as well as the expected volume of rain that will fall within the plant's root zone.

{%
include callout.html
type="cloud"
content="Weather data provided by [Open-Meteo.com](https://open-meteo.com) and licensed [Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/)."
%}

# Step 1: Add a plant variable

Add a location variable named "Plant" to the sequence. Set the variable to "Externally defined" with the default value set to a test plant. After testing you should set the default to "None".

# Step 2: Ensure your plants have watering curves

Make sure all of the plants you wish to use with this sequence have a [water curve](https://software.farm.bot/docs/curves) assigned to them. If a plant's `water_curve_id` is not set, the sequence will skip watering that plant entirely.

# Step 3: Add the Lua code

Add the Lua command with the following code:

```lua
plant = variable("Plant")
root_area = 3.14 * plant.radius^2

-- Get today's precipitation forecast from Open Meteo
request_url =
    "https://api.open-meteo.com/v1/forecast" ..
    "?latitude=" .. get_device("lat") ..
    "&longitude=" .. get_device("lng") ..
    "&timezone=auto&daily=precipitation_sum"
debug("Getting weather from " .. request_url)
api_response = http({url=request_url})
forecast = json.decode(api_response.body)
rain_mm = forecast.daily.precipitation_sum[1]

-- Calculate the volume of water the plant will get from the rain
rain_ml = math.floor(root_area * rain_mm / 1000)
debug("Forecasting " .. rain_mm .. "mm of rain today; plant's roots can expect " .. rain_ml .. "mL")

-- Get plant's water curve and water needs in mL based on plant's age
local water_curve, water_needs_ml
if plant.water_curve_id then
    water_curve = get_curve(plant.water_curve_id)
    water_needs_ml = water_curve.day(plant.age)
    debug("Plant needs " .. water_needs_ml .. "mL of water today")
else
    toast("Plant has no assigned water curve; skipping", "warn")
    return
end

-- Determine how much FarmBot should water
water_deficit = water_needs_ml - rain_ml

-- Move to and water the plant, or don't
if water_deficit > 0 then
    toast("Watering the deficit amount of " .. water_deficit .. "mL.")
    move{ x = plant.x, y = plant.y, z = safe_z() }
    dispense(water_deficit)
else
    toast("Rain will provide enough water for this plant today; skipping")
end
```

# Step 4: Make the sequence your own

Here are some ideas for modifying the sequence:

- Add a loop to water all of the plant's in the garden while only needing to get the weather forecast once.
- Add a fallback watering amount in case a plant does not have a watering curve assigned to it.
- Explore other features of the [Open-Meteo API](https://open-meteo.com) to utilize more weather data. For example, you could get the temperature forecast and use it to increase the watering amount if it will be very hot.


{%
include callout.html
type="share"
content="We want to see what modifications you come up with! Share your ideas and code in the [FarmBot Forum](https://forum.farmbot.org/)."
%}

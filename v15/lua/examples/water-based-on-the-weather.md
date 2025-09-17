---
title: "Water Based on the Weather"
slug: "water-based-on-the-weather"
description: "Get today's forecast to water more efficiently based on the weather and each plant's needs"
---

In this example we'll get today's **weather forecast** from an external service based on your FarmBot's latitude and longitude. The forecast will be cached as a [custom setting](https://software.farm.bot/docs/custom-settings) using [`env()`](../functions/configuration.md#envkey-value--envkey). We'll then determine if we should water a plant based on its age and watering curve as well as the expected volume of rain that will fall within the plant's root zone.

{%
include callout.html
type="cloud"
content="Weather data provided by [Open-Meteo.com](https://open-meteo.com) and licensed [Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/)."
%}

# Step 1: Create a new sequence

Create a new sequence named "Water Based on the Weather".

# Step 2: Add a plant variable

Add a location variable named "Plant" to the sequence. Set the variable to "Externally defined" with the default value set to a test plant. After testing you should set the default to "None".

# Step 3: Ensure your plants are planted and have watering curves

Make sure all of the plants you wish to use with this sequence have a **STATUS** of "Planted" and have a [water curve](https://software.farm.bot/docs/curves) assigned to them. If a plant's `water_curve_id` is not set or the `age` is not defined, the sequence will skip watering that plant entirely.

# Step 4: Add the Lua code

Add a Lua command to the sequence with the following code and try it out!

```lua
plant = variable("Plant")
root_area = 3.14 * plant.radius^2

function get_rain_forecast()
    -- ENV for storing rain data
    local env_key = "rain_forecast"

    -- Get today's date in YYYY-MM-DD format
    local today = local_time("year") .. "-" .. string.format("%02d", local_time("month")) .. "-" .. string.format("%02d", local_time("day"))

    -- Retrieve any stored precipitation data
    local stored_data = env(env_key)

    -- Check the stored data
    if stored_data then
        local stored_table = json.decode(stored_data)
        if stored_table.date == today then
            -- If the date matches, use the stored precipitation value
            rain_mm = stored_table.rain_mm
            debug("Using stored rain forecast for " .. today .. ": " .. rain_mm .. "mm")
        else
            -- Or clear the stale data
            stored_data = nil
        end
    end

    if not stored_data then
        debug("No stored rain forecast found for today")
        -- Get today's precipitation forecast from Open Meteo
        request_url =
            "https://api.open-meteo.com/v1/forecast" ..
            "?latitude=" .. get_device("lat") ..
            "&longitude=" .. get_device("lng") ..
            "&timezone=auto&daily=precipitation_sum"
        debug("Getting [forecast](" .. request_url .. ") from [Open-Meteo](https://open-meteo.com/) ([CC BY 4.0](https://creativecommons.org/licenses/by/4.0/))")
        api_response = http({url=request_url})
        forecast = json.decode(api_response.body)
        rain_mm = forecast.daily.precipitation_sum[1]

        -- Save the new precipitation data with today's date
        local new_data = json.encode({date = today, rain_mm = rain_mm})
        env(env_key, new_data)
        debug("Saved new rain forecast for " .. today .. ": " .. rain_mm .. "mm")
    end

    return rain_mm
end

rain_mm = get_rain_forecast()

-- Calculate the volume of rain the plant will get
rain_ml = math.floor(root_area * rain_mm / 1000)
debug("Forecasting " .. rain_mm .. "mm of rain today; plant's roots can expect " .. rain_ml .. "mL")

-- Get plant's water needs based on age
local water_curve, water_needs_ml
if plant.water_curve_id and plant.age then
    water_curve = get_curve(plant.water_curve_id)
    water_needs_ml = water_curve.day(plant.age)
    debug("Plant needs " .. water_needs_ml .. "mL of water today")
else
    toast("Plant has no assigned water curve or is not planted; skipping", "warn")
    return
end


-- If insufficient rain, water the deficit
water_deficit = water_needs_ml - rain_ml
if water_deficit > 0 then
    toast("Watering the deficit amount of " .. water_deficit .. "mL")
    move{ x = plant.x, y = plant.y, z = safe_z() }
    dispense(water_deficit)
else
    toast("Rain will provide enough water for this plant today; skipping")
end
```

# Step 5: Make the sequence your own

Here are some ideas for modifying the sequence:

- Add a loop to water all of the plants in the garden.
- Add a fallback watering amount in case a plant does not have a watering curve assigned to it.
- Explore other features of the [Open-Meteo API](https://open-meteo.com) to utilize more weather data. For example, you could get the temperature forecast and use it to increase the watering amount if it will be very hot.


{%
include callout.html
type="share"
content="We want to see what modifications you come up with! Share your ideas and code in the [FarmBot Forum](https://forum.farmbot.org/)."
%}

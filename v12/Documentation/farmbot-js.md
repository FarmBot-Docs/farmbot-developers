---
title: "FarmBot JS"
slug: "farmbot-js"
description: "Library to wrap FarmBot's authentication and RPC instructions. [GitHub repository](https://github.com/FarmBot/farmbot-js)."
---

* toc
{:toc}

# Installation


__NPM:__

```shell
npm install farmbot
```

__Vanilla JS:__

```html
<script src="https://cdn.jsdelivr.net/npm/farmbot@latest/dist/farmbot_single_file.js"></script>
<script>
  var farmbot123 = new fbjs.Farmbot({ token: "foo.bar.baz" });
</script>
```

## Supported environments

|                              |                              |
|------------------------------|------------------------------|
|**Browsers**                  |Works on all _modern_ browsers that were released in the last 12 months.
|**NodeJS**                    |Independent developers have reported success when using FarmBotJS in a Node environment, but we do not test against Node based setups, nor do we (FarmBot, Inc) use FarmBotJS in a production Node environment. Issue reports related to NodeJS are highly appreciated.

## Running the test suite

```bash
npm run test
```

# Login with an API Token
Login using your [API token](web-app/rest-api.md#generating-an-api-token) from the [FarmBot Web App](http://my.farm.bot).


```javascript
import { Farmbot } from "farmbot";

var SUPER_SECRET_TOKEN = "eyJ0eXAiOiJKV1...4Ry7CiA";

let bot = new Farmbot({ token: SUPER_SECRET_TOKEN });

bot
  .connect()
  .then(function () {
    return bot.moveRelative({ x: 1, y: 2, z: 3, speed: 100 });
  });
```

# Sending commands to a FarmBot object


```javascript
bot
  .connect()
  .then(function(bot){
    console.log("Bot online!");
    return bot.emergencyStop(); // You can chain commands.
  })
  .then(function(bot){
    console.log("Bot has stopped!");
  })
  .catch(function(error) {
    console.log("Something went wrong :(");
  });
```

## Basic RPC commands
Call RPC commands using the corresponding method on `bot`. All RPC commands return a promise.


```javascript
bot
  .home({ axis: "x", speed: 800 })
  .then(function (ack) {
    console.log("X Axis is now at 0.");
  })
  .catch(function (err) {
    console.log("Failed to bring X axis home.");
  })
```

## Currently supported commands
[See the annotated type definitions for available methods and properties.](https://github.com/FarmBot/farmbot-js/blob/main/dist/farmbot.d.ts)

# Events


```javascript
  var bot = Farmbot({ token: '---'});
  bot.on("eventName", function(data, eventName) {
    console.log("I just got an" + eventName + " event!");
    console.log("This is the payload: " + data);
  })
   // "I just got an eventName event!"
   // "This is the payload: any javascript object or primitive"
  bot.emit("eventName", "any javascript object or primitive");
  var eventHandlers = bot.event("eventName");
   // [function(){...}]
```

## Routine events
 * `"logs"`: The bot will send logs to this channel.
 * `"offline"`: Connection lost. **Note: FarmBotJS will try to auto-reconnect**.
 * `"online"`: Client is connected and subscribed to bot.
 * `"sent"`: Triggered when the application begins sending a message.
 * `"status_v8"`: Most important. When the REMOTE device state changes (eg: "x" goes from 0 to 100), the bot will emit this event.
 * `"legacy_status"`: Formerly `"status"`. Deprecated and scheduled for removal in 2019. Do not use in new applications.
 * `"sync"`: A resource on the API has changed.

## Special events
 * `<random uuid>`: RPC commands have UUIDs when they leave the browser. When the bot responds to that message, FarmBotJS will emit an event named after the request's UUID. Mostly for internal use.
 * `"malformed"`: When the bot gets a bad RPC command, it will notify you via this channel.
 * `*`: Catch all events (for debugging).

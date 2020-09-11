---
title: "FarmBot JS"
slug: "farmbot-js"
excerpt: "Content here is syndicated from the [repository README](https://github.com/FarmBot/farmbot-js/blob/master/README.md)."
hidden: false
createdAt: "2018-05-09T20:40:57.675Z"
updatedAt: "2019-01-18T17:30:29.665Z"
---
# Browser support

Works on any browser that supports:

 * [Native Promise objects](http://caniuse.com/#feat=promises).
 * [Web sockets](http://caniuse.com/#feat=websockets).
 * JSON (any browser made after 1942).

Independent developers have reported success when using FarmBotJS in a Node environment, but we do not test against Node based setups. Issue reports related to NodeJS are highly appreciated.

# Installation
## NPM

```
npm install farmbot
```

## Vanilla JS

```
<script src="./dist/farmbot_single_file.js"></script>
<script>
  var farmbot123 = new fbjs.Farmbot({ token: "foo.bar.baz" });
<script>
```

__:__
Please raise an issue if you require support with other package managers.

# Running the test suite (advanced)

```
npm run test
```

# Login with an API token

Login using your API token from the [FarmBot Web App](http://my.farm.bot). Click here for instructions on how to [generate an API token](https://github.com/FarmBot/farmbot-web-app#generating-an-api-token).


__Login example:__

```javascript
import { Farmbot } from "farmbot";

var SUPER_SECRET_TOKEN = "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJzdWIiOiJ0ZXN0MTIzQHRlc3QuY29tIiwiaWF0IjoxNDU5MTA5NzI4LCJqdGkiOiI5MjJhNWEwZC0wYjNhLTQ3NjctOTMxOC0xZTQxYWU2MDAzNTIiLCJpc3MiOiJodHRwOi8vbG9jYWxob3N0OjMwMDAvIiwiZXhwIjoxNDU5NDU1MzI4LCJtcXR0IjoibG9jYWxob3N0IiwiYm90IjoiYWE3YmIzN2YtNWJhMy00NjU0LWIyZTQtNThlZDU3NDY1MDhjIn0.KpkNGR9YH68AF3iHP48GormqXzspBJrDGm23aMFGyL_eRIN8iKzy4gw733SaJgFjmebJOqZkz3cly9P5ZpCKwlaxAyn9RvfjQgFcUK0mywWAAvKp5lHfOFLhBBGICTW1r4HcZBgY1zTzVBw4BqS4zM7Y0BAAsflYRdl4dDRG_236p9ETCj0MSYxFagfLLLq0W63943jSJtNwv_nzfqi3TTi0xASB14k5vYMzUDXrC-Z2iBdgmwAYUZUVTi2HsfzkIkRcTZGE7l-rF6lvYKIiKpYx23x_d7xGjnQb8hqbDmLDRXZJnSBY3zGY7oEURxncGBMUp4F_Yaf3ftg4Ry7CiA";

let bot = new Farmbot({ token: SUPER_SECRET_TOKEN });

bot
  .connect()
  .then(function () {
    return bot.moveRelative({ x: 1, y: 2, z: 3, speed: 100 });
  });
```

# Sending commands to a FarmBot object


__Command example:__

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


__RPC example:__

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

Currently supported commands: see the [annotated type definitions for available methods and properties](https://github.com/FarmBot/farmbot-js/blob/master/dist/farmbot.d.ts).

## Using events


__Event example:__

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

## Common events

 * `"logs"`: The bot will send logs to this channel.
 * `"malformed"`: When the bot gets a bad RPC command, it will notify you via this channel.
 * `"offline"`: Connection lost. **Note: FarmBotJS will try to auto-reconnect**.
 * `"online"`: Client is connected and subscribed to bot.
 * `"sent"`: Triggered when the application begins sending a message.
 * `"status"`: Most important. When the REMOTE device state changes (eg: "x" goes from 0 to 100), the bot will emit this event.
 * `"sync"`: A resource on the API has changed.
 * `<random uuid>`: RPC commands have UUIDs when they leave the browser. When the bot responds to that message, FarmBotJS will emit an event named after the request's UUID. Mostly for internal use.
 * `*`: Catch all events (for debugging).

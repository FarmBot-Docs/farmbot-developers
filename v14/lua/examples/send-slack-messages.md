---
title: "Send Slack Messages"
slug: "send-slack-messages"
description: "Example Lua code for sending messages to a Slack channel"
---

It is possible for FarmBot to send outbound HTTP requests using [Lua](../../lua/intro.md). This feature can be used to create third-party integrations with proprietary software products that offer webhook integrations, such as [Slack](https://slack.com/).

In this tutorial, we will demonstrate how it is possible to send messages from FarmBot to Slack using this abbreviated process:

1. FarmBot performs an HTTP POST to an [incoming webhook URL](https://en.wikipedia.org/wiki/Webhook) on Slack's servers.
2. Slack transforms the HTTP request to a message that is seen by Slack users in a particular chat room.

![Screenshot of Slack chat message sent by FarmBot](_images/slack_message.png)

# Step 1: Generate a webhook URL

Before you begin, you will need to generate an **incoming webhook URL**. Since these instructions may change over time, we recommend referencing the [official Slack webhook documentation](https://api.slack.com/messaging/webhooks) for guidance.

By the end of setup, you will have a URL that can be used to generate messages on Slack by way of an HTTP POST.

{%
include callout.html
type="warning"
title="Do not share the webhook URL"
content="Anyone with access to the URL will be able to send messages to your Slack channel."
%}

# Step 2: Create a sequence

Once you have a Slack webhook URL, navigate to the [sequence editor](https://software.farm.bot/docs/sequences) and create a new sequence. Then add a <span class="fb-step fb-lua">Lua</span> command to the sequence.

![A sequence with an empty Lua block](_images/empty_lua_sequence.png)

# Step 3: Add Lua code

Paste the following code into the Lua command, making sure to replace the example `url` with your webhook URL generated in step 1.

```lua
payload = json.encode({
  text = "FarmBot says hi! :wave:"
})

url = "https://hooks.slack.com/services/CHANGE/THIS/URL"

res, err = http({ url = url, method = 'POST', headers = {}, body = payload })

if err then
    send_message("error", "ERROR: " .. inspect(err), {"toast"})
else
    send_message("debug", "REQUEST SENT: " .. inspect(res))
end
```

Now <span class="fb-button fb-green">SAVE</span> the sequence and wait for it to sync with the FarmBot. You can then test it with the <span class="fb-button fb-orange">RUN</span> button to make sure it functions as expected.

# Step 4: Run the sequence

Once the sequence is coded and saved, you can run it in a variety of ways:

* By using the <span class="fb-button fb-orange">RUN</span> button in the [sequence editor](https://software.farm.bot/docs/sequences).
* By binding the sequence to a physical button on the device via a [pin binding](https://software.farm.bot/docs/pin-bindings).
* From within a parent sequence, via an <span class="fb-step fb-execute">EXECUTE</span> command.
* On a recurring schedule, via an [event](https://software.farm.bot/docs/events).
* Via third party software, using [FarmBot JS](https://github.com/FarmBot/farmbot-js).

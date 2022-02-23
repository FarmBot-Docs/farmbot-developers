---
title: "Server administration"
slug: "server-admin"
description: "Administrator reference document"
---

* toc
{:toc}

The intended audience for this document is employees of FarmBot, Inc. It outlines a number of tasks and features of the FarmBot Web App that are available to server administrators. Administrators of self-hosted servers may also find this document useful.

# Using the Rails console

Enter the following command to start the Rails console.

```
heroku run rails console --app=farmbot-staging
```

# Creating customer support tokens

Server admins can create admin tokens to remotely assist users when requested.

 * From the Rails console, type `puts Device.find($DEVICE_ID).help_customer`
 * Paste the resulting code into the Javascript console of a browser while using the web app.
 * Refresh the page.
 * Visit `/terminal` for device shell access if needed.

# Publishing a featured sequence

Not all sequences can be directly published from a web app account because of security restrictions. The web app offers a way for administrators to publish sequences that are not restricted in this way.

 * Log into the web app using the account specified by the `AUTHORIZED_PUBLISHER` environment variable.
 * Create a sequence as usual.
 * Run `heroku run rake sequence:publish --app=farmbot-staging`.
 * Enter the sequence ID you wish to publish from the list of available options.

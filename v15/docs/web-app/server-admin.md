---
title: "Server administration"
slug: "server-admin"
description: "Administrator reference document"
---

* toc
{:toc}

The intended audience for this document is employees of FarmBot, Inc. It outlines a number of tasks and features of the FarmBot Web App that are available to server administrators. Administrators of self-hosted servers may also find this document useful.

# Creating customer support tokens

Server admins can create admin tokens to remotely assist users when requested.

 * From the Rails console, type `puts Device.find($DEVICE_ID).help_customer`
 * Paste the resulting code into the Javascript console of a browser while using the web app.
 * Refresh the page.
 * Visit `/terminal` for device shell access if needed.

# Publishing a featured sequence

Not all sequences can be directly published from a Web App account because of security restrictions. The Web App offers a way for administrators to publish sequences that are not restricted in this way.

 * Log into the Web App using the account specified by the `AUTHORIZED_PUBLISHER` environment variable.
 * Create a sequence as usual.
 * Run `rake sequence:publish` on the running server instance.
 * Select the appropriate sequence you wish to publish from the list of available options.

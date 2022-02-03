---
title: "Example API requests"
slug: "api-docs"
description: "Example HTTP requests"
---

# About This Document

The intended audience for this document is employees of FarmBot, Inc. It outlines a number of tasks and features of the FarmBot Web App that are available to server administrators. Administrators of self-hosted servers may also find this document useful.

# Publishing FarmBot.JS

1. From the Web App repository, generate a new corpus via `sudo docker-compose run web rake corpus:generate`
1. Copy the corpus to your clipboard via `xclip -sel clip < ./latest_corpus.ts`
1. Paste the contents of the file into `corpus.ts`
1. Update the FarmBot VERSION in `farmbot.ts`
1. Update the FarmBot version in `package.json`
1. Run `./build.sh`
1. Commit the update to source control and push to Github.
1. Run `npm publish`.

# Publishing FarmBot.Py

Build instructions are provided in the README.md file of FarmBotPy

# Creating Customer Support Tokens

Server admins can create admin tokens to remotely assist users when requested.

 * From the Rails console, type `puts Device.find($DEVICE_ID).help_customer`
 * Paste the resulting code into the Javascript console of a browser while using the web app.
 * Refresh the page.
 * Visit `/terminal` for device shell access if needed.

# Updating Rollbar Tokens

Rollbar is used to track production runtime errors on FarmBot OS. The errors are reported using a rollbar token that is compiled into the FBOS release image.
Over time, the token must be rotated because Rollbar will continue to receive error reports from legacy versions of FarmBot OS that are not of interest.

 * Create a new project token in the Rollbar administrative settings page. `https://rollbar.com/ORG/PROJECT/settings/access_tokens/`
 * Copy the token into the ROLLBAR_TOKEN environment variable in Circle CI project for FarmBot OS.
 * New releases of FarmBot OS will use the new token.

**Ensure that you set a reasonable rate limit for the token.**

# Publishing an "Official" Featured Sequence

Not all sequences can be directly published from a Web App account because of security restrictions.
The Web App offers a way for administrators to publish sequences that are not restricted in this way.

 * Log into the Web App using the account specified by the `AUTHORIZED_PUBLISHER` environment variable.
 * Create a sequence as usual.
 * Run `rake sequence:publish` on the running server instance.
 * Select the appropriate sequence you wish to publish from the list of available options.

# Release a New Stable FBOS Release

 * Create a new pull request from `staging` to `main` and merge it after CI passes.
 * Merging a commit into staging will trigger a CI build.
 * After 5 minutes, a draft release will be created.
 * Visit the [releases page](https://github.com/FarmBot/farmbot_os/releases) and convert the draft to a release. **Uncheck the pre-release checkbox.** The next step will not work if you do not.
 * Run `rake releases:publish` and publish the release to the `stable` channel by following the instructions provided.

# Publish an FBOS Release Candidate

 * Create a feature branch off of the `staging`. **The branch name must begin with `qa/`.**
 * Implement feature(s) as required.
 * Commit changes and push to the newly created `qa/***` branch.
 * The CI system will begin a new _draft_ release. The draft will appear on the [releases page](https://github.com/FarmBot/farmbot_os/releases).
 * Once the build completes (~5 minutes), convert the draft to a release. **Do not uncheck the pre-release checkbox.**
 * Run `rake releases:publish` and follow the instructions.

---
title: "FarmBot OS Development"
slug: "farmbot-os-development"
---

Most development will be done in "host" environment. This means that rather than making a change on your computer, then pushing it to the device, we can rapidly develop things from the luxury of our own machine. See this [Nerves getting started guide](https://hexdocs.pm/nerves/getting-started.html) for more information about this. But as a side effect, we will need to be able to configure (at least) two different environment/target combos where:

`environment` is one of:

|environment                   |Description                   |
|------------------------------|------------------------------|
|`prod` - The production environment|* No developer features enabled (such as logs, local fw updates etc).<br>* No remote shell<br>* No remote firmware updates.<br>* Must be digitally signed.
|`dev` - The development environment|* Logs most things to the console.<br>* Remote shell<br>* Remote firmware updates.
|`test` - The test environment |* Only exists for running tests on the `host` target currently.

And `target` (where the `environment` will run) is one of:

|target                        |Use                           |
|------------------------------|------------------------------|
|`host`                        |For development
|`rpi3`                        |For running on a Raspberry Pi 3
|`rpi`                         |For running on a Raspberry Pi Zero

{%
include callout.html
type="info"
title="Note"
content="You will need to configure your Farmbot API, Frontend, and MQTT services for the below commands to work. You _can_ however use the default `my.farm.bot` servers. see `config/host/auth_secret_template.exs` for more information."
%}

# Running unit tests

Tests should be ran while developing features. You should have a *local* Farmbot stack up and running and configured for this to work. `config/host/auth_secret_template.exs` will have more full instructions.

```bash
MIX_ENV=test mix deps.get # Fetch test env specific deps.
mix test
```

# Feature development

If you plan on developing features, you will probably want to develop them with the `dev` and `host` combo. These are both the default values, so you can simply do:
```bash
mix deps.get # You should only need to do this once.
iex -S mix # This will start an interactive shell.
```

# Development on device

Sometimes features will need to be developed and tested on the device itself. This is accomplished with the `dev` and `rpi3` combo. It is *highly* recommended that you have an FTDI cable for this such as [this](https://www.digikey.com/product-detail/en/ftdi/TTL-232R-RPI/768-1204-ND) one

```bash
MIX_TARGET=rpi3 mix deps.get # Get deps for the rpi3 target. You should only need to do this once.
MIX_TARGET=rpi3 mix firmware # Produce a firmware image.
# Make sure you SDCard is plugged in before the following command.
MIX_TARGET=rpi3 mix firmware.burn # Burn the sdcard. You may be asked for a password here.
```

# Local firmware updates

If you're bot is connected to your local network, you should be able to push updates over the network to your device.

```bash
# make some changes to the code...
MIX_TARGET=rpi3 mix firmware # Build a new fw.
MIX_TARGET=rpi3 mix firmware.push <your device ip address> # Push the new fw to the device.
```
Your device should now reboot into that new code. As long as you don't cause a factory reset somehow, (bad init code, typo, etc) you should be able continuously push updates to your device.

# Updating Rollbar tokens

Rollbar is used to track production runtime errors on FarmBot OS. The errors are reported using a rollbar token that is compiled into the FBOS release image.
Over time, the token must be rotated because Rollbar will continue to receive error reports from legacy versions of FarmBot OS that are not of interest.

 * Create a new project token in the Rollbar administrative settings page. `https://rollbar.com/ORG/PROJECT/settings/access_tokens/`
 * Copy the token into the ROLLBAR_TOKEN environment variable in Circle CI project for FarmBot OS.
 * New releases of FarmBot OS will use the new token.

**Ensure that you set a reasonable rate limit for the token.**

# Publish an FBOS release candidate

 * Create a feature branch off of the `staging`. **The branch name must begin with `qa/`.**
 * Implement feature(s) as required.
 * Commit changes and push to the newly created `qa/***` branch.
 * The CI system will begin a new _draft_ release. The draft will appear on the [releases page](https://github.com/FarmBot/farmbot_os/releases).
 * Once the build completes (~5 minutes), convert the draft to a release. **Do not uncheck the pre-release checkbox.**
 * Run `rake releases:publish` and follow the instructions.

# Publish an FBOS stable release

 * Create a new pull request from `staging` to `main` and merge it after CI passes.
 * Merging a commit into staging will trigger a CI build.
 * After 5 minutes, a draft release will be created.
 * Visit the [releases page](https://github.com/FarmBot/farmbot_os/releases) and convert the draft to a release. **Uncheck the pre-release checkbox.** The next step will not work if you do not.
 * Run `rake releases:publish` and publish the release to the `stable` channel by following the instructions provided.

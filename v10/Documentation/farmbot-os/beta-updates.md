---
title: "Beta Updates"
slug: "beta-updates"
---


{%
include callout.html
type="warning"
title="Not for everyone"
content="Please only opt into beta updates if you are working with FarmBot staff to report bugs. Beta updates may be unstable and are not intended for daily usage. They are intended primarily for testing bug fixes and features."
%}

# Usage
When opting into a beta update, please be aware of the changes being made. The [changelog](https://github.com/FarmBot/farmbot_os/blob/staging/CHANGELOG.md#changelog) will have information on what changes will be in the update.

If something doesn't work properly please report the issue in [this forum topic](https://forum.farmbot.org/t/using-farmbotos-beta-updates/3951) or to the FarmBot staff person you are in contact with. Include as much information as possible. At least the following:

* Current production version
* Beta version
* Beta commit SHA
* What you expected to happen
* What actually happened
* Any relevant logs

If your bot rebooted or failed to boot, please [gather a log dump](gathering-a-log-dump.md) and **privately** share it with a FarmBot staff person.

# Opting in to beta updates
Now that you've read the warnings and usage documentation, you are ready to actually opt into beta updates.

* Click the FarmBotOS Version on the [device](https://my.farm.bot/app/device) panel.
* Change the **OS RELEASE CHANNEL** option to `beta`.
* Agree to the warning.
* Click <span class="fb-button fb-green">Update</span>
   * You may need to wait up to 30 minutes for this to take effect.

![out.gif](_images/out.gif)


# Downgrading
Currently one may opt out of beta updates, but not downgrade. This may change in the future, but for now you will either have to wait for the production version to be released, or manually re-flash the microSD card.

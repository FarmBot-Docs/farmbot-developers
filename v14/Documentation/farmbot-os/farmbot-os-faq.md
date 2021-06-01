---
title: "Frequently Asked Questions"
slug: "farmbot-os-faq"
---

* toc
{:toc}

# Why can't I update my Arduino Firmware?
As of version 3.8.0 we decided to bundle the arduino firmware into FarmBot OS. There was a couple reasons for this:
* There are no more version conflicts between the firmware and operating system.
* Applying updates during FarmBot OS runtime can be dangerous and was leaving peoples bots unusable because of broken firmwares.

# Can the shell run on HDMI
No. FarmBot is designed to operate without the use of a monitor.

# Why aren't [X] or [Y] packages included?
See the above answer. [Raise an issue](https://github.com/FarmBot/farmbot_os/issues/new) to request a package. Future versions of FarmBot OS may provide a plugin system. It is not implemented yet.

# Setting up SSH
FarmBot can be configured to start an SSH server to aid in debugging and development. During configuration of Network, select `Advanced Settings` and paste your [ssh public key](https://git-scm.com/book/en/v2/Git-on-the-Server-Generating-Your-SSH-Public-Key) into the optional input section labeled: `id_rsa.pub`. FarmBot requires a public key and will not allow a username + password combination. FarmBot also only allows one key to be configured for security reasons.

## Connecting
From the same machine that owns the `id_rsa.pub` key and associated private key you can simply `ssh <ip address>`. If your machine supports `mdns`, you can also do `ssh farmbot-<node_name>` where `node_name` can be found by clicking the FarmBot OS version in the `FarmBot` section of the settings panel in the FarmBot web app.

## Usage
The console a user will be presented with is _not_ a Linux console. There are pretty much no Linux utilities built-in. This includes but is not limited to:
* `bash`
* `apt-get`
* `make`
* `screen`
* `vi`
* `cp`
* `mkdir`
* `ln`
* `echo`
* etc

What is available is a console to the FarmBot OS runtime. You will need to be familiar with the FarmBot OS source code for this to be helpful.

If all you are looking for is Logs, you will probably want to do:
```elixir
RingLogger.attach()
```

After that command you will see logs come across the screen in real time.

To exit the SSH session, type `~.`. This is an ssh escape sequence (See the ssh man page for other escape sequences). Typing `Ctrl+D` or logoff at the IEx prompt to exit the session aren't implemented.

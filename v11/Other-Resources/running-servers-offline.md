---
title: "Running Servers Offline"
slug: "running-servers-offline"
---

* toc
{:toc}


{% include callout.html type="danger" title="Not Recommended" content="This is not a simple alternative for users behind a firewall. If you are running FarmBot in an organization with strict security policies or firewalls, see our notes [for IT security professionals](https://software.farm.bot/docs/for-it-security-professionals).

Do not run an offline setup unless you are a software developer intending to modify (fork) the FarmBot software suite." %}


# NTP and offline servers
Since the Raspberry Pi does not have a real-time clock, FarmBot OS _must_ have access to an [NTP server](https://en.wikipedia.org/wiki/Network_Time_Protocol) for proper operation. This is essential for functionality such as encryption and proper scheduling of Events. Without a reliable network time source, FarmBot's clock will skew rapidly, leading to system failure.

Under normal conditions, FarmBot OS will use the publicly accessible `pool.ntp.org` server.

If you wish to run a server offline, you will be required to host your own NTP server. When running WiFi configuration, you will need to set the server address manually under the "Advanced Network Settings" panel.

An internet search will reveal many self-hosted NTP server packages. We do not provide assistance to end-users with NTP server setup.

# Support
Running FarmBot completely offline is not a use case that FarmBot Inc targets when developing software. It is highly likely you will encounter bugs since this is not the default use case for a FarmBot.

Please [raise an issue](https://github.com/FarmBot/Farmbot-Web-App/issues/new?title=Offline%20Setup%20Issues) if you find a bug while running FarmBot in an offline-only setup. Reporting offline setup issues helps us fix problems in future releases, but be advised that offline setups are a lower priority than internet-enabled setups. As such, **we may not have the resources to fix offline-only setup issues**. Bug fixes from community members (in the form of pull requests) are highly appreciated.

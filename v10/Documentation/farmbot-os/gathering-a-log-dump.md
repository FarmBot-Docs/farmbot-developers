---
title: "Gathering a Log Dump"
slug: "gathering-a-log-dump"
---


{%
include callout.html
type="danger"
title="Exercise caution"
content="The following instructions will tell you how to make a log dump file that contains private information about your FarmBot, your network credentials, and other personally identifiable information. **Never publicly share this file as it could give an attacker access to your FarmBot and network.**"
%}

If your bot did not boot properly and you ended back up in Configurator, there will be a dump of log files from the previous boot. *BEFORE* trying to reconfigure, navigate to [http://192.168.24.1/logs](http://192.168.24.1/logs) while connected to Configurator. This will give you a file called: `[VERSION]-[MD5SUM]-logs.sqlite3`. Do *NOT* post that file on the forum or anywhere public. Either email it or send it as a private message on the forum to FarmBot staff.

{%
include callout.html
type="danger"
title="Do not publicly share the [VERSION]-[MD5SUM]-logs.sqlite3 file"
content="This file may contain private information that could give an attacker access to your FarmBot and network. Only share this file with FarmBot staff using private communications (such as email)."
%}


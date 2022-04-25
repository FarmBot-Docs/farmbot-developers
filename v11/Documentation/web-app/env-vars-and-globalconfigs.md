---
title: "ENV Vars and GlobalConfigs"
slug: "env-vars-and-globalconfigs"
---


# Why?

FarmBot is an Open Source project that can be self hosted by third party developers. The way that FarmBot, inc. configures its servers for public use might not meet the needs of self hosting users. Additionally, there are security implications to configuration management in an Open Source project; We would not want to leak our database password into source control, for example.

Farmbot attempts to decouple configuration from code as much as possible, in keeping with the [12 Factor Methodology](https://12factor.net/config):

 > The twelve-factor app stores config in [environment variables](https://en.wikipedia.org/wiki/Environment_variable) (often shortened to env vars or env). Env vars are easy to change between deploys without changing any code; unlike config files, there is little chance of them being checked into the code repo accidentally; and unlike custom config files, or other config mechanisms such as Java System Properties, they are a language- and OS-agnostic standard.

 -- 12 Factor Methodology Homepage

By using ENV vars as the first choice for server configuration, we can:

 * Allow for server customization
 * Safely share the application source code with the public
 * Reap all the other [benefits that the 12 Factor Methodology](https://thenewstack.io/12-factor-app-streamlines-application-development/) provides.

# How?

For most parts of the app, environment variables are loaded into a `.env` file.

 * Information about the `.env` file format can be found [here](https://docs.docker.com/compose/env-file/)
 * Documentation on legal values can be found [here](https://github.com/FarmBot/Farmbot-Web-App/blob/staging/example.env#L7).

{%
include callout.html
type="info"
title="Important Note"
content="The app also exposes a [secondary configuration system](https://github.com/FarmBot/Farmbot-Web-App/blob/staging/app/models/global_config.rb) called `GlobalConfig`. This secondary system addresses use cases where ENV variables are not appropriate. The system is discussed later in this document."
%}



# Real World Examples

FarmBot, Inc. requires validation of user email addresses. Most self hosting users do not want this behavior, however. To allow server admins to choose between verifying emails or not, the application exposes a `ENV["NO_EMAILS"]` variable. When present, this ENV var will disable email verification.

Another example is the `EXTRA_DOMAINS` variable. It can be set to a comma separated list of alternative domain names that a server may control. This allows the same server to be hosted on more than one domain name (`my.farm.bot`, `my.farmbot.io`, etc..).

These examples are for illustrative purposes. The full list of variables is available [here](https://github.com/FarmBot/Farmbot-Web-App/blob/staging/example.env#L7).

# Problems

ENV vars work for _most_ configuration use cases, but there are some caveats:

 * Changing ENV vars requires a server restart. In many cases, this creates an unacceptable downtime period, particularly for servers with high uptime requirements.
 * Environment variables are a server-side concern. When a client loads the FarmBot Web App in their browser, it is not possible to see the server's ENV vars. If this were not the case, it would be possible for users to steal database credentials quite easily.
 * Not all customization happens on the server side ("back end"). There are many use cases that require ENV passing information from the server to the client.

# Solutions

## Solution: Runtime Reloading of ENV Vars

As stated previously, ENV variables require a process restart to take effect. For some values, a restart is not practical.

For values that must change after the server has started, the FarmBot Web App uses a model (database table) known as `GlobalConfig`. The `GlobalConfig` source code can be found [here](https://github.com/FarmBot/Farmbot-Web-App/blob/staging/app/models/global_config.rb).

Some `GlobalConfig` values (such as `"TOS_URL"`) are bootstraped using ENV vars if no value can be found in the `global_configs` table.

A `GlobalConfig`s value can be changed at runtime from the [Rails console](https://guides.rubyonrails.org/command_line.html#rails-console):

```
GlobalConfig.create!(key: "FAVORITE_VEGGIE", value: "Carrots")
```

{%
include callout.html
type="danger"
title="WARNING"
content="Unlike traditional ENV vars, `GlobalConfig` values are _not hidden from the public._ Do not store sensitive data in `GlobalConfig`!"
%}

## Solution: Sharing ENV Vars with Clients

{%
include callout.html
type="info"
title="NOTE"
content="This section requires knowledge from the previous section."
%}

As stated in the "Problems" section, exposing _all_ ENV vars to a browser would be an extreme security risk. We want to expose _some_ ENV vars to clients, but not all of them.

To get around this problem the Web App's UI exposes a global variable to the browser: `window.globalConfig`. This variable contains all `GlobalConfig` items, but not necessarily all ENV vars. For this reason it is important that you **do not store sensitive data in the GlobalConfig table**.

We can inspect the value of `globalConfig` in our browser:

```javascript
console.log(window.globalConfig);
```

On production, `globalConfig` contains the following values:


__globalConfig:__

```javascript

  // Current application environment:
  "NODE_ENV":"production",

  // Terms of Service URL:
  "TOS_URL":"https://farm.bot/tos/",

  // Privacy Policy URL:
  "PRIV_URL":"https://farm.bot/privacy/",

  // Lowest FarmBot OS versions the server supports:
  "MINIMUM_FBOS_VERSION":"7.0.0",
  "FBOS_END_OF_LIFE_VERSION":"7.0.1",

  // Web App version the server runs:
  "LONG_REVISION":"191b0ead3dfe1cc43ee416a5ff27a064af556192",
  "SHORT_REVISION":"191b0ead"
```

As stated, the server's environment variables are not exposed to the public. We also mentioned that we had a second configuration system that complements traditional server ENV vars- the `GlobalConfig` database table.

`GlobalConfig` values are transferred from the server to the client using server-side templating.

When the Web App loads a web page that needs ENV vars, it injects a a `<script>` tag that declares the `globalConfig` variable.

`app/views/dashboard/_common_assets.html.erb`:


__app/views/dashboard/_common_assets.html.erb:__

```html
<script>
  // ---SNIP!---

  // THIS IS WHERE ENV VARIABLES CROSS OVER
  // From the server to the client:

  window.globalConfig = <%= raw(@global_config) %>

  // The @global_config contains all database entries
  // for the `GlobalConfig` table (but not all ENV
  // vars).

  // ---SNIP!---

</script>
```

Please note that the `<%= %>` is [Ruby ERB syntax](https://en.wikipedia.org/wiki/ERuby)

The value of `@global_config` is set in `app/controllers/dashboard_controller.rb`:


__app/controllers/dashboard_controller.rb:__

```ruby
class DashboardController < ApplicationController
  before_action :set_global_config
  layout "dashboard"

# --- SNIP! ---

private

  def set_global_config
    # THIS IS WHERE @global_config is created:
    @global_config = GlobalConfig.dump.to_json
  end
end
```

With these systems in place, we can now add and remove ENV variables from the Rails console via:

```ruby
GlobalConfig.create!(key: "FAVORITE_PLANT", value: "cabbage")
=> #<GlobalConfig:0x0000 key: "FAVORITE_PLANT", value: "cabbage">
```

To view the variable from the browser, we can simply type:

```javascript
globalConfig.FAVORITE_PLANT;
// => "cabbage"
```

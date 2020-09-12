---
title: "User Interface"
slug: "user-interface"
hidden: false
createdAt: "2018-05-23T14:51:36.865Z"
updatedAt: "2019-12-13T08:09:46.196Z"
---

__:__
This document is intended for software developers. For end-user documentation, please see the [Web App User Documentation](https://software.farm.bot/docs/the-farmbot-web-app)

The FarmBot web app's **user interface** is a [single page application](https://en.wikipedia.org/wiki/Single-page_application) that allows users to control a FarmBot remotely. It supports editing of [sequences](https://software.farm.bot/docs/sequences), [regimens](https://software.farm.bot/docs/regimens), [events](https://software.farm.bot/docs/farm-events), a virtual garden map, and much more.

![c2365c9-Web-App-on-Different-Devices.png](/images/c2365c9-Web-App-on-Different-Devices.png)

## At a glance
 * **Programming Language:** [TypeScript](https://www.typescriptlang.org/index.html)
 * **UI Library:** [ReactJS](https://reactjs.org)
 * **Build System:** [WebPack](https://webpack.js.org)
 * **State Management:** [Redux JS](https://redux.js.org)
 * **Repository:** [FarmBot-Web-App](https://github.com/FarmBot/Farmbot-Web-App)

# Useful developer utilities
 * `window.store.getState()` Get the current Redux store state from the browser's Javascript console.
 * `window.current_bot` The current FarmBot instance created by [FarmBot JS](/v11/Documentation/farmbot-js.md) from the browser's Javascript console.
 * `sudo docker-compose run web npm run typecheck` Runs the TypeScript type checker against the codebase in your terminal. Pull requests can not be accepted unless this step passes.
 * `sudo docker-compose run web npm run test` Runs [unit tests](https://en.wikipedia.org/wiki/Unit_testing) to prevent [regressions](https://en.wikipedia.org/wiki/Software_regression). This check must pass for a pull request to be accepted.

# FAQ
## How do I update or add translations?
Thanks for your interest in internationalizing the FarmBot web app! To add translations:

1. Fork the repo
2. Navigate to `/public/app-resources/languages` and run the command `node _helper.js yy` where `yy` is your language's [language code](http://www.science.co.il/Language/Locale-codes.php). Eg: `ru` for Russian.
3. Edit the translations in the file created in the previous step: `"phrase": "translated phrase"`.
4. When you have updated or added new translations, commit/push your changes and submit a pull request.

## My code is generating a "content security warning"
The web app implements a [content security policy](https://en.wikipedia.org/wiki/Content_Security_Policy) to prevent certain types of security violations, such as cross-site scripting and token theft. Unfortunately, this means that some code may not execute as intended. Please [raise an issue](https://github.com/FarmBot/Farmbot-Web-App/issues/new) if you have any questions.

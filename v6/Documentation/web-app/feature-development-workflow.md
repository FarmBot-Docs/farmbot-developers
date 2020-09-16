---
title: "Development Workflow"
slug: "feature-development-workflow"
---

* toc
{:toc}

When developing new features for the Web App, a fast development workflow is essential.

This document outlines the common development practices of developers at FarmBot, Inc.

The practices listed below are recommendations and may not fit the needs of every developer.

# Development Workflow

When developing new features and bug fixes for FarmBot, a typical workflow is to:

1. Start the server as usual.
2. Implement the feature or fix.
3. Run type checks (`npm run typecheck`).
4. Run tests (`rspec spec` and `npm run test`).
5. Commit changes and propose a pull request.

We will take a deeper look at steps 2-5 in the sections below.

# Preventing Bugs

Reducing [regressions](https://en.wikipedia.org/wiki/Software_regression) is an important aspect of any software development cycle. The Web App has a number of systems in place to prevent the (re)introduction of bugs:

## Type Checks

The [User Interface](/v6/Documentation/web-app/user-interface.md) is written in [Typescript](https://www.typescriptlang.org). Because it is a statically typed language, it is possible to quickly [type check](https://en.wikipedia.org/wiki/Type_system#Static_type_checking) the application by running `npm run typecheck`. This will catch a large number of bugs, such as spelling errors and type mismatches (such as passing `"1"` instead of `1` in a function call).

When developing features for the Web App, consider running `npm run typecheck` regularly. An even more effective strategy is to **use an editor that has good Typescript integration**, such as [Visual Studio Code](https://code.visualstudio.com). Such editors are able to find type errors in code _as you write the feature_, which can provide a much better development experience.

## Unit Tests

Type checking is able to detect many problems, but it cannot verify the accuracy of a program's business logic. [Unit testing](https://en.wikipedia.org/wiki/Unit_testing) is required To verify that the logic of the application is functioning as intended.

Running unit tests is an ideal way to determine if a change to the application will break existing functionality.

### Typescript Tests

The [User Interface](/v6/Documentation/web-app/user-interface.md) unit tests use [jest](https://github.com/facebook/jest) for the majority of testing. Tests can be run via `npm run test`.

### Ruby Tests

Ruby tests are written with [RSpec](http://rspec.info). You can run the Ruby test suite via `rspec spec`.

## Code Coverage

Checking the percentage of a codebase that has unit tests is known as [code coverage](https://en.wikipedia.org/wiki/Code_coverage). Code coverage for Ruby files is [monitored on codecov.io](https://codecov.io/gh/FarmBot/Farmbot-Web-App) while Typescript coverage is [monitored on coveralls.io](https://coveralls.io/github/FarmBot/Farmbot-Web-App).

To view Typescript code coverage locally, run `npm run test-slow`. When the tests finish, a report will be available in `coverage/index.html`. You can open this file and view the results in any browser.

To view Ruby code coverage, you may run `rspec spec` and open the same file listed above.

## Continuous Integration

To prevent accidental introduction of bugs and also to ensure that the build system is always compatible with the current version of the Web App, the project runs a [continuous integration](https://en.wikipedia.org/wiki/Continuous_integration) (CI) service.

FarmBot, Inc. runs the CI service prior to merging any new feature into the application. Continuous integration can find a number of issues such as:

 * Failing tests.
 * Failing type checks.
 * A drop in test coverage.
 * Dependency/versioning problems.
 * Changes that would cause installation problems for new developers.

# Environments and Configuration

Most of the configuration values for the API are set through the use of [ENV variables](https://en.wikipedia.org/wiki/Environment_variable), which are easy to change based on wether you are developing features or trying to use the application with a real device. A list of ENV variables used in the app can be found [here](https://github.com/FarmBot/Farmbot-Web-App/blob/staging/config/application.example.yml).

Since the Web App is a Rails application, it can switch between production and development modes by setting the `RAILS_ENV` variable (eg. `RAILS_ENV=development`). It also has three environments (and databases) like most Rails apps: `production`, `development` and `test`.

To learn more about Rails configuration and environments, see the [Rails configuration guide](http://guides.rubyonrails.org/configuring.html#creating-rails-environments).

**For the majority of Web App feature development and testing, a physical device is not required.** This is also true for all unit tests, where [stub methods](https://en.wikipedia.org/wiki/Method_stub) can be used in place of a real FarmBot.

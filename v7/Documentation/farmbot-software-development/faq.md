---
title: "Frequently Asked Questions"
slug: "faq"
---

* toc
{:toc}

# I’m a software developer. Where can I download FarmBot source code?

Like most open source projects, we host our software on [GitHub](https://github.com/farmbot). Here are the most popular source code links:
  * [Web App](https://github.com/FarmBot/Farmbot-Web-App) (Ruby, Typescript) - Cloud storage, REST API and user interface.
  * [FarmBot OS](https://github.com/FarmBot/farmbot_os) (Elixir) - Embedded operating system that runs on the Raspberry Pi. The “glue” between the API, frontend and firmware.
  * [Firmware](https://github.com/FarmBot/farmbot-arduino-firmware) (C++) - Arduino source code. Controls stepper motors, pins, etc.

# Does the web API support ARM-based processors?

Not at this time. The only software that supports Raspberry Pi is FarmBot OS

# What language is FarmBot written in?

FarmBot is comprised of many different software systems and the language used varies across projects. Generally speaking, we use a combination of C++, [Ruby](https://www.ruby-lang.org/en/), [Elixir](https://elixir-lang.org), and [TypeScript](https://www.typescriptlang.org).

# Do I need to know Elixir to program FarmBot?

No. FarmBot provides a system for plugins known as "Farmware". Farmware may be written in other languages, such as Python. See [Farmware](/v7/Documentation/farmware.md) documentation for details.

An alternative approach is to write a standalone application that interacts with FarmBot externally via [REST API](/v7/Documentation/web-app/rest-api.md) calls or [FarmBot JS](/v7/Documentation/farmbot-js.md).

# Should I clone FarmBot OS on GitHub or use the image?

You almost certainly want the image. The only exception is if you plan on modifying the FarmBot OS source code.

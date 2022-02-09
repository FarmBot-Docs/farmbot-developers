---
title: "Lua"
slug: "intro"
description: "Insert Lua code fragments directly into sequences"
---

* toc
{:toc}

The [sequence editor](https://software.farm.bot/docs/sequences) is an easy to use tool for automating FarmBot operations. However, advanced users who are familiar with computer programming concepts may opt for a more advanced interface. For these users, we provide several methods to insert **Lua code fragments** directly into sequences:

# Lua commands

Using a <span class="fb-step fb-lua">Lua</span> command is the most straightforward and universal way to use Lua in your sequences. With the Lua command, you can execute up to 3000 characters worth of code - enough to operate FarmBot's motors, sensors, peripherals, and camera, and even use 3rd party APIs.

![lua command](_images/lua_command.png)

# Assertion commands

The <span class="fb-step fb-assertion">Assertion</span> command also allows for long-form Lua code execution as well as the ability to execute a subsequence or abort execution depending on the `return`. ([Learn more](https://software.farm.bot/docs/advanced-sequence-commands)).

![assertion command](_images/assertion_command.png)

# Formulas

You can also execute Lua by using the **formula** option in a <span class="fb-step fb-move">Move</span> command's **OVERRIDE** or **X, Y, Z** input fields. This option is generally best for short-form code that only deals with positioning.

![move command with formula](_images/move_command_with_formula.png)

# What's next?

 * [Lua Functions](functions.md)
 * [Lua Examples](examples.md)

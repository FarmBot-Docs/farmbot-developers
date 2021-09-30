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

# A Note About Long-Running Lua Scripts

Lua, like many scripting languages, has automatic [garbage collection](https://en.wikipedia.org/wiki/Garbage_collection_(computer_science)).
Although the FarmBot Lua runtime does support garbage collection, it will never run the garbage collector automatically. Determining the appropriate time to run garbage collection is the end user's responsibility, which is quite different from most Lua environments.

If you have a long-running Lua script that appears to slow down over time, or you find that FarmBot OS runs out of memory while a script runs, this most likely means that you need to run the garbage collector.

End users can trigger a garbage collector sweep by running `collectgarbage()`. Most users do not need to do this, and this advice only applies to long-running and memory-intensive Lua scripts.

# What's next?

 * [Lua Functions](functions.md)
 * [Lua Examples](examples.md)

---
title: "CeleryScript"
slug: "celery-script"
---

* toc
{:toc}


{% include callout.html type="success" title="CeleryScript is an actively maintained standard" content="CeleryScript nodes are added, modified and removed often. The latest list of Celery Script nodes can be found [here](https://github.com/FarmBot/farmbot-js/blob/master/dist/corpus.d.ts)." %}

The FarmBot system has [many moving parts](/v10/Documentation/farmbot-software-development/high-level-overview.md). Data must be exchanged between systems in a way that is predictable and asynchronous. Sometimes, this data is even used for telling the bot what to do in a similar fashion to traditional programming languages. To accomplish this, we use a special [remote procedure call](https://en.wikipedia.org/wiki/Remote_procedure_call) and data interchange format called "CeleryScript".

CeleryScript nodes are specially formatted JSON documents. FarmBot uses these documents for a variety of storage and communication use cases and also as an internal programming language for sequence scripting.

It is a programming language, serialization format and RPC protocol unified under a single schema known as a "corpus".

With adequate experience, it is possible for a developer to read and write Celeryscript manually, but this is an uncommon occurrence. Celeryscript is typically read and written by automated tools such as servers, FarmBots, compilers, and interpreters. Celeryscript's main goal is uniformity and ease of development when authoring said tools. It has a structure that is optimized for ease of consumption by developer tools which sometimes comes at the expense of human readability. Please keep this design tradeoff in mind as you read the documentation.

# Intended audience

This document is intended for advanced software development and debugging. Many software developers can avoid the low level details of Celery Script by using the [FarmBotJS library](https://github.com/FarmBot/farmbot-js). All of the low-level details of CeleryScript are abstracted away when using a wrapper library.

CeleryScript knowledge is required only if you prefer to not use the wrapper library, are developing new features for the FarmBot platform, or are trying to debug specific problems with the system. It's also a great way for an intrepid software developer to learn FarmBot system internals.

Javascript developers are encouraged to use [FarmBot JS](/v10/Documentation/farmbot-js.md) instead of raw CeleryScript for most use cases.

**If you are writing CeleryScript for a new or unsupported language** you are highly encouraged to write your own wrapper library, as writing CeleryScript by hand is tedious, error-prone and likely to have future compatibility issues. Conversely, migrating and managing auto-generated CeleryScript is often a trivial task that can be accomplished via scripting.


# Where is CeleryScript used?

Celery Script is used:

 * To build an [abstract syntax tree](https://astexplorer.net) of commands in the [sequence editor](https://software.farm.bot/docs/sequences), which get stored and served by the [REST API](/v10/Documentation/web-app/rest-api.md)'s `/sequences` endpoint.
 * To send one-off [movement commands](https://software.farm.bot/docs/controls) and other messages between users and devices over the [message broker](/v10/Documentation/web-app/message-broker.md).
 * To build [Farmware](/v10/Documentation/farmware.md) (plugins) that talk directly to FarmBot.
 * Internal functionality such as changing device configuration on-the-fly and triggering firmware updates.

# Example sequence

The most prominent use case for CeleryScript is the Sequence Editor. A sequence is a collection of nested celery script nodes.

Creating this sequence in the web app...


![example_1.png](example_1.png)

...results in the creation of the following CeleryScript:



__Celery Script Sequence Example:__

```json

  "kind": "sequence",
  "name": "Example 1",
  "color": "gray",

  // These values are set by the server.
  "id": 1,
  "created_at": "2000-01-01T00:00:00.000Z",
  "updated_at": "2000-01-01T00:00:00.000Z",
  "in_use": false,

  "args": {
    // Set by the server; Tells us the Celery Script version of this sequence.
    "version": 20000101,
    "locals": {
      "kind": "scope_declaration",
      "args": { }
    }
  },
  "body": [
    // Each body item is what the user sees as a "step" in the editor.
    // "If statement" step
    {
      "kind": "_if",
      "args": {
        // "left hand side"
        "lhs": "pin1",
        // Operator
        "op": "is",
        // "right hand side"
        "rhs": 1,
        // Main branch
        "_then": {
          "kind": "execute",
          "args": {
            // The `id` of the "Water all plants" sequence
            "sequence_id": 2
          }
        },
        // Else branch
        "_else": {
          "kind": "nothing",
          "args": {
          }
        }
      }
    },
    // "Wait" step: Pause for 2.3 seconds.
    {
      "kind": "wait",
      "args": {
        "milliseconds": 2300
      }
    }
  ]
```


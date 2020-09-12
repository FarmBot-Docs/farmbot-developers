---
title: "Nodes"
slug: "nodes"
hidden: false
createdAt: "2019-01-18T04:05:13.071Z"
updatedAt: "2019-07-16T20:16:48.489Z"
---
With exception to the [REST API](/v7/Documentation/web-app/rest-api.md) and some other edge cases, all communication that happens between FarmBot users, devices and systems is wrapped in a Celery Script node.

A node is a specially formatted JSON document. It is a composable building block that can be nested and arranged to create trees of commands, similar to the way an [abstract syntax tree](https://en.wikipedia.org/wiki/Abstract_syntax_tree) is used to create programming languages.

Here is an example of an `install_farmware` Celery Script node, which tells a device to download and install a 3rd party add-on:


__install_farmware Celery Script node example:__

```json

    // THE "kind" ATTRIBUTE:
    // Every CS node MUST have a "kind" attribute.
    // This is the nodes name.
    // Legal "kind" types are listed here:
    // https://github.com/FarmBot/farmbot-js/blob/7044292a6591753b3edad3ed7bf3a8a08a41fac4/dist/corpus.d.ts#L418
    "kind": "install_farmware",

    // THE "args" (arguments) FIELD:
    // Every node has an "args" object. It is REQUIRED.
    // The arguments for a node will vary based on the "kind".
    "args": { url: "http://foo.bar/manifest.json" },

    // THE "comment" FIELD:
    // You do not need to use this (or even include it), but you can if it is helpful.
    // We use comments for tracing and debugging.
    "comment": "Optional. Useful when debugging, but ignored by the system.",

    // THE "body" FIELD:
    // Not every node will have a body.
    // If a node does have a body, it will ONLY contain other celery script nodes.
    // Example: The body of a "sequence" node may contain a "move_relative" node.
    body: []
}
```

At a minimum, every node has a `kind` and `args` attribute, which will vary based on the use case. It may also have a `body` and `comment` in some circumstances. No other attributes are allowed.

The types of nodes that are available, as well as the format of arguments is available within the [corpus.d.ts](https://github.com/FarmBot/farmbot-js/blob/master/dist/corpus.d.ts) file.



# Notable CeleryScript nodes

As noted above, a CeleryScript node is comprised of:

 * A `kind` (string) that determines a node's purpose
 * An `args` object that contains key/value pairs (some of these values will be child nodes, others will be simple primitive values such as numbers). If a node requires a particular `arg`, it will always be present. There is no such thing as an optional arg in CeleryScript. This simplifies many aspects of the standard.
 *  An optional `body` argument which, if defined, will contain a list of other CeleryScript nodes. A body will only ever contain CeleryScript nodes and will never contain primitive values such as strings or numbers.
 * An optional `comment` (string) field to aid developer readability.

Some common CeleryScript nodes include:

 * `move_relative`, `move_absolute`
 * `execute` - Runs a sequence via the `sequence_id` arg.
 * `rpc_request`, `rpc_ok`, `rpc_error` - discussed later in this document.

For a full listing, see this [auto-generated list of nodes](https://github.com/FarmBot/farmbot-js/blob/master/dist/corpus.d.ts).

__Not every CeleryScript node represents a device command:__
Some nodes, such as the `"coordinate"` node, are used to represent data.



# The "rpc_request" node

The CeleryScript specification defines three nodes used for real-time control of a device. These nodes are used extensively in the [User Interface](/v7/Documentation/web-app/user-interface.md) for one-off commands, such as device position adjustments.

 * `rpc_request` -  Initiated by a user (or occasionally, the [REST API](/v7/Documentation/web-app/rest-api.md)) when requesting the device do something. The desired action (eg: `move_relative`, `install_farmware`, etc..) is held in the `body` of this node.
 * `rpc_ok` - Sent by a device to an end user. Indicates that the request operation has succeeded.
 * `rpc_error` - Indicates that the request operation has failed. The body of an `rpc_error` will often contain a number of `explanation` nodes describing the circumstances of the failure.

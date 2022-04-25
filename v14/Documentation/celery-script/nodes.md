---
title: "Nodes"
slug: "nodes"
---

With exception to the [REST API](../web-app/rest-api.md) and some other edge cases, all communication that happens between FarmBot users, devices, and systems is wrapped in a **CeleryScript node**.

A node is a specially formatted JSON document. It is a composable building block that can be nested and arranged to create trees of commands, similar to the way an [abstract syntax tree](https://en.wikipedia.org/wiki/Abstract_syntax_tree) is used to create programming languages.

# Format

A CeleryScript node is comprised of:

 * A `kind` (string) that determines a node's purpose.
 * An `args` object that contains key/value pairs (some of these values will be child nodes, others will be simple primitive values such as numbers). If a node requires a particular `arg`, it will always be present. There is no such thing as an optional arg in CeleryScript. This simplifies many aspects of the standard.
 *  An optional `body` argument which, if defined, will contain a list of other CeleryScript nodes. A body will only ever contain CeleryScript nodes and will never contain primitive values such as strings or numbers.
 * An optional `comment` (string) field to aid developer readability.

Here is an example `reboot` node, which tells a device to restart the specified app:


__reboot Celery Script node example:__

```json
{
    // THE "kind" ATTRIBUTE:
    // Every CS node MUST have a "kind" attribute.
    // This is the nodes name.
    // Legal "kind" types are listed here:
    // https://github.com/FarmBot/farmbot-js/blob/7044292a6591753b3edad3ed7bf3a8a08a41fac4/dist/corpus.d.ts#L418
    "kind": "reboot",

    // THE "args" (arguments) FIELD:
    // Every node has an "args" object. It is REQUIRED.
    // The arguments for a node will vary based on the "kind".
    "args": { package: "farmbot_os" },

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

Some common CeleryScript nodes include:

 * `move_relative`, `move_absolute`
 * `execute` - Runs a sequence via the `sequence_id` arg.
 * `rpc_request`, `rpc_ok`, `rpc_error` - discussed later in this document.

{%
include callout.html
type="info"
title="Not every CeleryScript node represents a device command"
content="Some nodes, such as the `coordinate` node, are used to represent data."
%}



# Available nodes

See also the [corpus.d.ts](https://github.com/FarmBot/farmbot-js/blob/main/dist/corpus.d.ts) file.

|kind                   |type   |also known as     |Description                   |
|-----------------------|-------|------------------|------------------------------|
|`assertion`            |command|                  |Command for assertion style automated testing ([more info](https://software.farm.bot/docs/advanced-sequence-commands#assertion))
|`calibrate`            |command|find axis length  |Command for performing an axis [calibration (find axis length)](https://software.farm.bot/docs/movement-sequence-commands#calibrate)
|`change_ownership`     |command|                  |Transfers ownership of a FarmBot device from one web app account to another
|`channel`              |       |                  |
|`check_updates`        |command|update            |Instructs FarmBot to check for (and install) software updates
|`coordinate`           |       |                  |
|`emergency_lock`       |command|e-stop            |Emergency stops the FarmBot
|`emergency_unlock`     |command|unlock            |Unlocks the FarmBot from being emergency stopped
|`execute`              |command|execute sequence  |Command for executing a sequence ([more info](https://software.farm.bot/docs/logic-sequence-commands#execute-sequence))
|`execute_script`       |command|                  |
|`explanation`          |       |                  |Description of `rpc_error`
|`factory_reset`        |command|soft reset        |Instructs the FarmBot to factory reset
|`find_home`            |command|                  |Command for [finding home](https://software.farm.bot/docs/movements-sequence-commands#find-home) along an axis
|`flash_firmware`       |command|                  |Instructs FarmBot to flash firmware to the microcontroller
|`home`                 |command|move to home      |Command instructing FarmBot to go to the home position (this is different than finding home)
|`identifier`           |       |                  |
|`if`                   |command|                  |Allows FarmBot to evaluate if a condition is true or false and take a corresponding action
|`internal_entry_point` |       |                  |
|`internal_farm_event`  |       |                  |
|`internal_regimen`     |       |                  |
|`lua`                  |command|                  |see [lua documentation](../../lua/intro.md)
|`move`                 |command|                  |Command for moving FarmBot ([more info](https://software.farm.bot/docs/movements-sequence-commands#move))
|`move_absolute`        |command|move to           |Command for moving FarmBot to an absolute coordinate position ([more info](https://software.farm.bot/docs/movements-sequence-commands#move-to))
|`move_relative`        |command|                  |Command for moving FarmBot a relative amount from the current location ([more info](https://software.farm.bot/docs/movements-sequence-commands#move-relative))
|`named_pin`            |       |                  |
|`nothing`              |       |                  |
|`pair`                 |       |                  |
|`parameter_application`|       |                  |
|`parameter_declaration`|       |                  |
|`point`                |       |                  |Represents a point (location) in the farm designer map such as a plant, weed, point, or tool slot
|`point_group`          |       |                  |A group of points (locations) in the farm designer map
|`power_off`            |command|shutdown          |Instructs FarmBot to shutdown completely
|`read_pin`             |command|read sensor       |Command for [reading a pin (read sensor)](https://software.farm.bot/docs/peripherals-and-sensors-sequence-commands#read-sensor)
|`read_status`          |command|                  |Instructs FarmBot to send a status message with a full state tree
|`reboot`               |command|                  |Instructs FarmBot to reboot
|`rpc_error`            |       |                  |Indicates that the request operation has failed
|`rpc_ok`               |       |                  |Indicates that the request operation has succeeded
|`rpc_request`          |       |                  |Requests the device do something
|`scope_declaration`    |       |                  |
|`send_message`         |command|                  |Command for [sending a message](https://software.farm.bot/docs/logic-sequence-commands#send-message)
|`sequence`             |       |                  |
|`set_servo_angle`      |command|control servo     |Command for moving servo motors
|`set_user_env`         |       |                  |
|`sync`                 |command|                  |Instructs FarmBot to sync with the API
|`take_photo`           |command|                  |Instructs FarmBot to [take a photo](https://software.farm.bot/docs/image-proceessing-sequence-commands#take-photo) and upload it to the API
|`toggle_pin`           |command|toggle peripheral |Command for toggling the state of a pin (toggle peripheral)
|`tool`                 |       |                  |
|`update_resource`      |command|mark as           |see documentation for [mark as](https://software.farm.bot/docs/logic-sequence-commands#mark-as) command
|`variable_declaration` |       |                  |
|`wait`                 |command|                  |Command for [waiting](https://software.farm.bot/docs/logic-sequence-commands#wait) a time in milliseconds
|`write_pin`            |command|control peripheral|Command for [writing (control peripheral)](https://software.farm.bot/docs/peripherals-and-sensors-sequence-commands#control-peripheral) a digital or analog value to a pin
|`zero`                 |command|set home          |Command for setting the current location to [zero (set home)](https://software.farm.bot/docs/movements-sequence-commands#set-zero) along an axis



# rpc_request

The CeleryScript specification defines three nodes used for real-time control of a device. These nodes are used extensively in the [user interface](../web-app/user-interface.md) for one-off commands, such as device position adjustments.

 * `rpc_request` -  Initiated by a user (or occasionally, the [REST API](../web-app/rest-api.md)) when requesting the device do something. The desired action (eg: `move_relative`, `reboot`, etc..) is held in the `body` of this node.
 * `rpc_ok` - Sent by a device to an end user. Indicates that the request operation has succeeded.
 * `rpc_error` - Indicates that the request operation has failed. The body of an `rpc_error` will often contain a number of `explanation` nodes describing the circumstances of the failure.

# What's next?

 * [Identifying Success and Failure](identifying-success-and-failure.md)

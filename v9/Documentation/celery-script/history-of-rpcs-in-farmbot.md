---
title: "History of RPCs in FarmBot"
slug: "history-of-rpcs-in-farmbot"
---

* toc
{:toc}


{% include callout.html type="info" title="Information contained in this page is for historical context and reference" content="" %}

In the early days of FarmBot, we chose [JSON RPC](http://json-rpc.org/wiki/specification) as a means of passing messages between systems. It accomplished the job, but suffered from some issues:

 * JSON RPC 1.0 used positional arguments, which were easily placed in the wrong order and difficult to teach to new developers. It did not lend itself well to strongly typed languages such as Typescript.
 * JSON RPC 2.0 was built with a server/client architecture in mind, which did not represent the relation between users, devices, and APIs well.
 * FarmBot features a visual sequence builder, which had its own data format to represent custom built sequences. Having a separate data format for stored sequences essentially created two RPC formats.
 * Sequences were far more complex than traditional RPCs. Sequences built within FarmBot required recursion and other features that JSON RPC was not intended to address.
 * As the number of commands increased, it became increasingly difficult to spot spelling errors and out-of-date messages between systems.
 * As the platform feature count increased, so too did the number of communication protocols between software components. Disparate and unrelated protocols increased code duplication and decreased overall maintainability.

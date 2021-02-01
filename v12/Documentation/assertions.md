---
title: "Assertions"
slug: "assertions"
description: "FarmBot's native automated testing tool"
---

* toc
{:toc}

The **Assertion** command allows FarmBot to test if a condition is true or false for automated testing purposes. For example, you could set up a FarmBot to move back and forth repeatedly along an axis, and check the position after each movement. This type of test is useful for high-cycle hardware testing, and for continuous integration testing of software changes.

![Assertion step](_images/assertion_step.jpeg)

Assertions must be written in **Lua**, and will be evaluated against a Lua 5.2 interpreter. In the event that a **TEST FAILS**, FarmBot can either `Continue` execution, `Recover and continue`, `Abort and recover`, or just `Abort` execution altogether. The **RECOVERY SEQUENCE** allows you to reset FarmBot to a known state after a failure, send a message, or perform any other desired operations.

# Available Functions and Variables

Please see the [Lua scripting reference](lua-scripting.md).

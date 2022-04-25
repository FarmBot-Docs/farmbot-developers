---
title: "CeleryScript Glossary"
slug: "celeryscript-glossary"
---

# Primary Node
Sometimes referred to simply as "node". This is a JSON object with a `kind`, `args` and optional `body` key. It is the basic building block of CeleryScript structures.

# Edge Node
Any item found in the CeleryScript document that is not a fully formed Primary Node. This includes values like strings, numbers, and booleans.

# Corpus
A JSON document that describes the allowed format of every possible CeleryScript node. The most recent version is available at https://my.farm.bot/api/corpus

# Canonical Representation
The traditional format of CeleryScript discussed in this document. The root of the JSON document is a primary node that has more primary nodes and edge nodes nested within.

# Flat Intermediate Representation
A special format of CeleryScript where nodes are not nested and all information is stored in a single flat array. This is essential for storage of nodes in relational (SQL) databases and for easy execution of nodes on a device. As of June 2018, the format is not fully documented and is mostly used for [internal tools](https://github.com/FarmBot-Labs/Celery-Slicer).

# kind
A string identifier used to distinguish between the different types of CeleryScript primary nodes.

# args
A set of key value pairs found on the "args" property of a primary node. The key is a string. The value is either a primary node or an edge node. CeleryScript args are **never optional**.

# body
A property found on primary nodes. It is always optional. The length is always flexible and is never fixed in size. If populated, it only contains primary nodes and never contains raw edge nodes.

# comment
An optional string field on the root level of a primary node. It is used similarly to a comment in a traditional programming language. It is often removed during runtime. It is considered poor practice to store data in the `comment` field of a node.

# uuid
An optional string field that is always stripped from a node prior to storage or execution. It is an implementation detail due to technical limitations and is not considered part of the specification.

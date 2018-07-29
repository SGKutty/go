---
layout: page
title: 19 - Constants
---
***

<!-- markdownlint-disable MD002 -->

> __Constants__ are a way to create a named identifier whose value can never change. They also provide an incredible amount of flexibility to the language. The way constants are implemented in Go is very unique.

* Constants are not variables.

* They exist only at compilation.

* Named like variables

  * PascalCase for exported constants.

  * CamelCase for internal constants.

* __Typed Constants__([playground](https://play.golang.org/p/asoFAnY07Q2))

  * Typed constants work like immutable variables.

  * Can interoperable only with same types.

* __UnTyped Constants__([playground](https://play.golang.org/p/5EakJUjVekw))

  * Untyped constants work like literals.

  * Can interoperable with similar types.

  * Untyped constants can be implictly converted where typed constants and variables can't.

  * Think of untyped constants as having a Kind, not a Type.

* __Enumerated Constants__([file size example](https://play.golang.org/p/AiWOy1Kb_Nw))

  * Special symbol __iota__ allows related constants to be created easily.

  * Iota start at 0 in each const block and increments by one.
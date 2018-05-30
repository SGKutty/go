---
layout: page
title: Packaging
---

> Can you tell us about the worse features of C, from your point of view?

***

> `Brian Kernighan` said,  I think that the real problem with C is that it doesn’t give you enough mechanisms for structuring really big programs, for creating `firewalls` within programs so you can keep the various pieces apart. It’s not that you can’t do all of these things, that you can’t simulate object-oriented programming or other methodology you want in C. You can `simulate` it, but the compiler, the language itself isn’t giving you any help.

* Packaging creates `firewalls` within Go programs such that:

  * The various pieces of the program can be kept apart.
  * Large teams can work on large projects.
  * The compiler and the language itself can provide support and help
---
layout: page
title: Packaging
---
***

<!-- markdownlint-disable MD002 -->

> Can you tell us about the worse features of C, from your point of view?

***

> `Brian Kernighan` said,  I think that the real problem with C is that it doesn’t give you enough mechanisms for structuring really big programs, for creating `firewalls` within programs so you can keep the various pieces apart. It’s not that you can’t do all of these things, that you can’t simulate object-oriented programming or other methodology you want in C. You can `simulate` it, but the compiler, the language itself isn’t giving you any help.

&nbsp;

* Packaging creates `firewalls` within Go programs such that:

  * The various pieces of the program can be kept apart.
  * Large teams can work on large projects.
  * The compiler and the language itself can provide support and help

&nbsp;

## ✰ Language Mechanics

***

* In `Go`, each folder that contains source code is considered a package, and packages provide that `firewall`. As part of the language definition, Go turns each package into an individual `static` library, and it’s the static library that creates the physical `firewall`.

* This behavior is not something you can `circumvent`, it’s built into the language. The creation of static libraries in other languages is optional and achieved through tooling. You can think of packaging as applying the idea of `microservices` on a source tree. Each folder representing a self contained piece of functionality.

* In other languages, the source tree represents a `monolithic` application. If you want to break up the application, you need to create multiple source trees and use tooling to stitch it back together.

* Go has `no` concept of `sub-packages`. All folders, regardless of their physical location, are built into these static libraries and flattened out during compilation.

* Given that packages are standalone and their contents are `firewalled` there needs to be a way to `open` parts of the package to the outside world. This is where the idea of `exporting` and `unexporting` comes in.

* There is one more important language mechanic about Go packages. Two packages can’t `cross-import` each other. Imports are a one way street. As a result, when two packages need to import each other, it’s a smell that the packages need to be merged or decoupled.

## ✰ Design Philosophies
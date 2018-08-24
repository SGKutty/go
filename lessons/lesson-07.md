---
layout: page
title: 07 - Packaging
---
***

> **Brian Kernighan** said,  "I think that the real problem with C is that it doesn’t give you enough mechanisms for structuring really big programs. You can simulate Object Oriented Programming or other methodology if you want, but the compiler, the language itself isn’t giving you any help"

➩ **Packaging** creates `firewalls` within Go programs such that:

- The various pieces of the program can be kept apart.
- Large teams can work on large projects.
- The compiler and the language itself can provide support and help.

&nbsp;

## Language Mechanics
***

- In **Go**, each folder that contains source code is considered a package, and packages provide that `firewall`. Go turns each package into an individual `static` library, and it’s the static library that creates the physical firewall.

- This behavior is not something you can `circumvent`, it’s built into the language. The creation of static libraries in other languages is optional and achieved through tooling. You can think of packaging as applying the idea of microservices on a source tree. Each folder representing a self contained piece of functionality.

- In other languages, the source tree represents a monolithic application. If you want to break up the application, you need to create multiple source trees and use tooling to stitch it back together.

- Go has `no` concept of `sub-packages`. All folders, regardless of their physical location, are built into these static libraries and flattened out during compilation.

- Given that packages are standalone and their contents are firewalled, there needs to be a way to open parts of the package to the outside world. This is where the idea of `exporting` and `unexporting` comes in.

- There is one more important language mechanic about Go packages. Two packages can’t `cross-import` each other. Imports are a one way street. As a result, when two packages need to import each other, it’s a smell that the packages need to be merged or decoupled.

&nbsp;

## Design Philosophies
***

- **Purpose**

  - To be **purposeful**, packages must provide, not contain.

  - Package must be named with the intent to describe what it provides.

&nbsp;

- **Usability**

  - To be **usable**, packages must be designed with the user as their focus.

  - Package must be intuitive and simple to use.

  - Packages must respect their impact on resources and performance.

  - Packages must protect the user's application from cascading changes.

  - Packages must prevent the need for type assertion to be concrete.

  - Packages must reduce, minimize and simplify its code base.

&nbsp;

- **Portability**

  - To be **portable**, packages must be designed with reusability in mind.

  - Packages must aspire for the highest level of portability.

  - Packages must reduce taking on opinions when it's reasonable and practical.

  - Packages must not become a single point of dependency.

---
layout: page
title: 10 - Interface
---
***

➩ **Interfaces** provide a way to declare types that define only behavior. This behavior can be implemented by concrete types, such as struct or named types, via methods.

➩ When a concrete type implements the set of methods for an interface, values of the concrete type can be assigned to variables of the interface type.

➩ Then method calls against the interface value actually call into the equivalent method of the concrete value.

➩ Since any concrete type can implement any interface, method calls against an interface value are polymorphic in nature.

* The method set for a value, only includes methods implemented with a value receiver.

* The method set for a pointer, includes methods implemented with both pointer and value receivers.

* Methods declared with a pointer receiver, only implement the interface with pointer values.

* Methods declared with a value receiver, implement the interface with both a value and pointer receiver.

* The rules of method sets apply to interface types.

* Interfaces are reference types, don't share with a pointer.

* This is how we create polymorphic behavior in go.

* Polymorphism means that you write a certain program and it behaves differently depending on the data that it operates on
---
layout: page
title: 08 - Struct Types
---
***

<!-- markdownlint-disable MD002 -->

➩ __Struct Types__ are a way of creating complex types that group fields of data together. They are great way of organizing and sharing the different aspects of the data your program consumes.

➩ A computer architecture’s potential performance is determined predominantly by its word length (the number of bits that can be processed per access) and, more importantly, memory size, or the number of words that it can access.

&nbsp;

* We can use the struct `literal` form to initialize a value from a struct type.

* The dot (.) operator allows us to access individual field values.

* We can create anonymous structs.

* No inheritance, but can use composition via embedding([playground](https://play.golang.org/p/GA_4_P5Ik-I)).

* A tag for a field allows you to attach meta-information to the field which can be acquired using reflection([playground](https://play.golang.org/p/rOSzGGPeVug)).
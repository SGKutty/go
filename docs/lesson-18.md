---
layout: page
title: 18 - Primitives
---
***

<!-- markdownlint-disable MD002 -->

> In computing, language __primitives__ are the simplest elements available in a programming language. A primitive is the smallest `unit of processing` available to a programmer of a given machine, or can be an atomic element of an expression in a language.

## Boolean([playground](https://play.golang.org/p/_z_CE_DZbs8))

***

* Values are `true` or `false`.

* Not an alias for other types.

* Zero value is false.

&nbsp;

## Numeric types ([playground](https://play.golang.org/p/wn89FZH7THF))

***

* Signed integers

  * `int` type has varying size.

  * 8 bit(int8) through 34 bit(int64).

* Unsigned integers

  * 8 bit (uint8) through 32 bit (uint32).

* Supported Arithmetic operations:

  * Addition.

  * Subtraction.

  * Multiplication.

  * Division.

  * Remainder.

* Integer will support bit-wise operations.

* Zero value is 0.

* Can't mix types in same family! (uint16+uint32 = error).

* We can combine constant and any integer family.

  ```go
    const a = 10

    var b int64=20

    res = a+b
  ```

&nbsp;

## Floating point numbers([playground](https://play.golang.org/p/yXFO8yO8P79))

***

* Follow IEEE-754 standard.

* Zero value is 0.

* 32 and 64 bit version.

* Literal styles

  * Decimal(`3.14`).

  * Exponential(`13e18` or `2E10`).

  * Mixed(`13.7e12`).

* Supported Arithmetic operations;

  * Addition.

  * Subtraction.

  * Multiplication.

  * Division.

&nbsp;

## Complex numbers([playground](https://play.golang.org/p/hrQBC48LGxk))

***

* Zero value is (0+0i).

* 64 and 128 bit version.

* Built-in functions

  * `complex` - make complex number from two floats.

  * `real` - get real part as float.

  * `imag` - get imaginary part as float.

* Arithmetic operations

  * Addition.

  * Subtraction.

  * Multiplication.

  * Division.

&nbsp;

## Text Types([playground](https://play.golang.org/p/OQhqHJYDz9X))

***

* Strings

  * UTF-8.

  * Immutable.

  * Can be concatenated with plus(+) operator.

  * Can be converted to []bytes.

* Rune

  * UTF-32.

  * Alias for int32.

  * Special methods normally required to process, eg. `strings.Reader` #ReadRune.
---
layout: page
title: 19 - Understanding Type in Go
---
***

- The Go language provides these basic `numeric` types:

  ```sh
    * Unsigned Integers: uint8, uint16, uint32, uint64

    * Signed Integers: int8, int16, int32, int64

    * Real Numbers: float32, float64

    * Predeclared Integers: uint, int, uintptr
  ```

- The names for these keywords provide both pieces of the type `information`.

- The uint8 contains a `base` 10 number using one byte of `memory`. The value can be between 0 to 255.

- The int32 contains a base 10 number using 4 bytes of memory. The value can be between -2147483648 to 2147483647.

- The predeclared integers get mapped based on the `architecture` you are building the code against. On a 64 bit OS, int will map to int64 and on a 32 bit OS, it will be mapped to int32.

- Everything that is stored in memory comes back to one of these numeric types. `Strings` in Go are just a series of `uint8` types, with rules around stringing those bytes together and identifying end of string positions.

- A `pointer` in Go is of type `uintptr`. Again, based on the OS architecture this will be a uint32 or uint64. It is good that Go created a special type for pointers.

  > In the old days many C programmers would write code that assumed a pointer value would always fit inside an unsigned int. With upgrades to the language and architectures over time, that eventually was no longer true. A lot of code broke because addresses became larger than the predeclared unsigned int.

- `Struct` types are just combinations of know types that also eventually resolve to a numeric type.

  ```go
    type Example struct{
      BoolValue bool
      IntValue  int16
      FloatValue float32
    }
  ```

- This structure represents a complex type. It represents `7 bytes` with three different numeric representations.

- The bool is one byte, the int16 is 2 bytes and the float32 adds 4 more bytes. However, `8 bytes` are `actually` allocated in memory for this struct.

- All memory is allocated on an alignment boundary to minimize memory `defragmentation`.

- To determine the alignment boundary Go is using for your architecture, you can run the `unsafe.Alignof` function.

- The alignment boundary in Go for the `64bit` Darwin `platform` is `8 bytes`.

- So when Go determines the memory allocation for our structs, it will `pad` bytes to make sure the final memory footprint is a multiple of 8. The compiler will determine where to add the padding.

- This [program](https://github.com/g-kutty/go-code/blob/master/language/structs/example5/example5.go) shows the padding that Go inserted into the memory footprint for the Example type struct:
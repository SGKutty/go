---
layout: page
title: 19 - Understanding Type in Go
---
***

- The Go language provides these basic `numeric` types:

    ```sh
    * Unsigned Integers
      uint8, uint16, uint32, uint64

    * Signed Integers
      int8, int16, int32, int64

    * Real Numbers
      float32, float64

    * Predeclared Integers
      uint, int, uintptr
    ```  

- The names for these keywords provide both pieces of the type information.

- The uint8 contains a base 10 number using one byte of memory. The value can be between 0 to 255.

- The int32 contains a base 10 number using 4 bytes of memory. The value can be between -2147483648 to 2147483647.

- The predeclared integers get mapped based on the architecture you are building the code against. On a 64 bit OS, int will map to int64 and on a 32 bit OS, it will be mapped to int32.

- Everything that is stored in memory comes back to one of these numeric types. Strings in Go are just a series of uint8 types, with rules around stringing those bytes together and identifying end of string positions.
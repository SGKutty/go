---
layout: page
title:
---
***

- The Go language provides these basic `numeric` types:

  ```sh
    Unsigned Integers: uint8, uint16, uint32, uint64

    Signed Integers: int8, int16, int32, int64

    Real Numbers: float32, float64

    Predeclared Integers: uint, int, uintptr
  ```

- The names for these keywords provide both pieces of the type information.

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

- All memory is allocated on an alignment boundary to minimize memory [defragmentation](https://g-kutty.github.io/go-tour/lessons/20-memory_management/defragmentation/).

- To determine the alignment boundary Go is using for your architecture, you can run the `unsafe.Alignof` function.

- The alignment boundary in Go for the 64bit Darwin platform is 8 bytes.

- So when Go determines the memory allocation for our structs, it will `pad` bytes to make sure the final memory footprint is a multiple of 8. The compiler will determine where to add the padding.

- This [program](https://github.com/g-kutty/go-code/blob/master/language/structs/3-padding/example2/example.go) shows the padding that Go inserted into the memory footprint for the Example type struct.

  ```go
    type Example struct {
      BoolValue  bool
      IntValue   int16
      FloatValue float32
    }

    func main() {
      example := &Example{
        BoolValue:  true,
        IntValue:   10,
        FloatValue: 3.141592,
      }

      exampleNext := &Example{
        BoolValue:  true,
        IntValue:   10,
        FloatValue: 3.141592,
      }

      alignmentBoundary := unsafe.Alignof(example)

      sizeBool := unsafe.Sizeof(example.BoolValue)
      offsetBool := unsafe.Offsetof(example.BoolValue)

      sizeInt := unsafe.Sizeof(example.IntValue)
      offsetInt := unsafe.Offsetof(example.IntValue)

      sizeFloat := unsafe.Sizeof(example.FloatValue)
      offsetFloat := unsafe.Offsetof(example.FloatValue)

      sizeBoolNext := unsafe.Sizeof(exampleNext.BoolValue)
      offsetBoolNext := unsafe.Offsetof(exampleNext.BoolValue)

      fmt.Printf("Alignment Boundary: %d\n", alignmentBoundary)
      fmt.Printf("BoolValue  = Size: %d Offset: %d Addr: %v\n", sizeBool, offsetBool, &example.BoolValue)
      fmt.Printf("IntValue   = Size: %d Offset: %d Addr: %v\n", sizeInt, offsetInt, &example.IntValue)
      fmt.Printf("FloatValue = Size: %d Offset: %d Addr: %v\n", sizeFloat, offsetFloat, &example.FloatValue)
      fmt.Printf("Next 	   = Size: %d Offset: %d Addr: %v\n", sizeBoolNext, offsetBoolNext, &exampleNext.BoolValue)
    }
  ```

- Here is the output:

  ```go
    Alignment Boundary: 8
    BoolValue  = Size: 1 Offset: 0 Addr: 0xc000090000
    IntValue   = Size: 2 Offset: 2 Addr: 0xc000090002
    FloatValue = Size: 4 Offset: 4 Addr: 0xc000090004
    Next       = Size: 1 Offset: 0 Addr: 0xc000090008  
  ```

- This `size` value shows how much memory, for that field, will be read and written to.
  As expected, the size is inline with the type information.

- The `offset` value shows how many bytes into the memory footprint we will find the
  start of that field.

- The `address` is where the start of each field, within the memeory footprint, can be found.

- We can see that Go is `padding` 1 byte between the BoolValue and IntValue fields. The offset value and difference between the two address is 2 bytes. You can also see that the next allocation of memory is starting 4 bytes away from the last field in the struct.

- Let's prove the 8 byte alignment rule by only keeping the 1 byte bool field in the struct.

  ```go
    type Example struct {
      BoolValue bool
    }

    func main() {
      example := &Example{
        BoolValue: true,
      }

      exampleNext := &Example{
        BoolValue: true,
      }

      alignmentBoundary := unsafe.Alignof(example)

      sizeBool := unsafe.Sizeof(example.BoolValue)
      offsetBool := unsafe.Offsetof(example.BoolValue)

      sizeBoolNext := unsafe.Sizeof(exampleNext.BoolValue)
      offsetBoolNext := unsafe.Offsetof(exampleNext.BoolValue)

      fmt.Printf("Alignment Boundary: %d\n", alignmentBoundary)
      fmt.Printf("BoolValue = Size: %d Offset: %d Addr: %v\n", sizeBool, offsetBool, &example.BoolValue)
      fmt.Printf("Next      = Size: %d Offset: %d Addr: %v\n", sizeBoolNext, offsetBoolNext, &exampleNext.BoolValue)
    }
  ```

- And the output:

  ```sh
    Alignment Boundary: 8
    BoolValue = Size: 1 Offset: 0 Addr: 0xc0000160f8
    Next      = Size: 1 Offset: 0 Addr: 0xc0000160f9
  ```

- Subtract the two address and you will see there is an 8 byte difference between the two type struct allocations. Go padding 7 bytes to the struct to maintain the alignment boundary.

- We can only manipulate memory when we are working with a numeric type and the assignment operator (=) is how we do it. To make life easier for us, Go has created some complex types that support the assignment operator directly. Some of these types are strings, arrays and slices. To see a complete list of these types check out this [document](https://golang.org/ref/spec#Types).

- These complex types abstract the manipulation of the underlining numeric types that can be found in each implementation. In doing so, These complex types can be used like numeric types that directly read and write to memory.

- Go is type `safe` language. This means that the compiler will always enforce like types on each side of an assignment operator. This is really important because it prevents us from reading or writing to memory incorrectly.

- Imagine if we could do the following. If you try to compile this code you will get an `error`.

  ```go
    type Example struct{
        BoolValue bool
        IntValue  int16
        FloatValue float32
    }

    example := &Example{
        BoolValue:  true,
        IntValue:   10,
        FloatValue: 3.141592,
    }

    var pointer *int32
    pointer = *int32(&example.IntValue)
    *pointer = 20
  ```

- What I am trying to do is get the memeory address of the 2 byte IntValue field and store it in a pointer of type int32.

    ![memory_1.png](https://g-kutty.github.io/go-tour/lessons/19-understanding_types/images/memory_1.png?raw=true)

- Then I am trying to use the pointer to write 4 byte integer into that memory address. If I was able to use that pointer, I would be voilating the type rules for the IntValue field and corrupting memory along the way.

    ![memory_2.png](https://g-kutty.github.io/go-tour/lessons/19-understanding_types/images/memory_2.png?raw=true)

- Based on the memory footprint above, the pointer would be writing the value of 20 across the 4 bytes between FFE3 and FFE6.

    ![memory_3.png](https://g-kutty.github.io/go-tour/lessons/19-understanding_types/images/memory_3.png?raw=true)

- The value of IntValue would be 20 as expected but the value of FloatValue would now be 0. Imagine if writing those bytes went outside the memory allocation for this struct and started to corrupt memory in other areas of the application. The bugs that would follow would appear random and unpredictable.

- The Go compiler will always make sure assigning memory and casting is safe.

- In this casting example the compiler is going to complain:

  ```go
    package main

    import (
        "fmt"
    )

    type int32Ext int32

    func main() {
        var jill int32Ext = 10

        //cannot use jill (type int32Ext) as type int32 in assignment
        var jack int32 = jill

        var jack int32 = int32(jill)
        fmt.Printf("%d\n", jack)
    }
  ```

- The compiler respects that jill is of type int32Ext and makes no assumptions about the safeness of the assignment.

- Now we use casting and the compiler allows the assignment and the value prints as expected. When we perform the cast the compiler checks the safeness of the assignment. In our case it identifies the values are of the same type and allows the assignment.
---
layout: page
title: 06 - Int to String
---

***
&nbsp;

> We can convert this int to string by using methods `Itoa`, `FormatInt` from `strconv` package.

<!-- markdownlint-disable MD002 -->
&nbsp;

## ✰ FormatInt

***

* This is the opposite conversion as ParseInt. With FormatInt, we must pass an int64 value.

* Go [program](https://play.golang.org/p/UQNe9Hga47C) that uses **strconv.FormatInt**.

    ```go
    package main

    import (
        "fmt"
        "strconv"
    )

    func main() {
        v := int64(-42)

        //convert with base 10
        s10 := strconv.FormatInt(v, 10)
        fmt.Printf("%T, %v\n", s10, s10)

        // convert with base 64
        s16 := strconv.FormatInt(v, 16)
        fmt.Printf("%T, %v\n", s16, s16)
    }
    ```

* FormatInt returns the string representation of i in the given base, for 2 <= base <= 36. The result uses the lower-case letters 'a' to 'z' for digit values >= 10.

<!-- markdownlint-disable MD002 -->
&nbsp;

## ✰ Itoa

***

* Itoa is shorthand for FormatInt(int64(i), 10).

* Go [program](https://play.golang.org/p/gV0vpFrVbUK) that uses **strconv.Itoa**

    ```go
    package main

    import (
        "fmt"
        "strconv"
    )

    func main() {
        i := 10
        s := strconv.Itoa(i)
        fmt.Printf("%T, %v\n", s, s)
    }
    ```
&nbsp;

## ✰ Benchmark test

***

* Often we need to convert an int into a string. This benchmark compares `FormatInt` and `Itoa`. It converts `1234` into a string with each method.

* This test based on go version `go1.10.1 linux/amd64`

    ```go
    package main

    import (
        "runtime"
        "strconv"
        "testing"
    )

    var val = 1234

    // BenchmarkItoa check performance of Itoa
    func BenchmarkItoa(b *testing.B) {

        // run garbage collector and reset timer
        runtime.GC()
        b.ResetTimer()

        // use Itoa
        for i := 0; i < b.N; i++ {
            _ = strconv.Itoa(val)
        }
    }

    // BenchmarkFormatInt check performance of FormatInt
    func BenchmarkFormatInt(b *testing.B) {

        // run garbage collector and reset timer
        runtime.GC()
        b.ResetTimer()

        // use ParseInt
        for i := 0; i < b.N; i++ {
            _ = strconv.FormatInt(int64(val), 10)
        }
    }
    ```

* Result

  ```sh
    BenchmarkItoa-4        50000000     62.0 ns/op
    BenchmarkFormatInt-4   100000000    58.1 ns/op
  ```

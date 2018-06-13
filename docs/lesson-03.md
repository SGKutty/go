---
layout: page
title: String to Int
---

***
&nbsp;

> A string contains digit characters like `123`. We can convert this string to a number (an `int`) with using methods `ParseInt`, `Atoi` from `strconv` package.

<!-- markdownlint-disable MD002 -->
&nbsp;

## ✰ ParseInt

***

* Go [program](https://play.golang.org/p/S3OQYXWocQC) that uses **strconv.ParseInt**.

    ```go
    package main

    import (
        "fmt"
        "strconv"
    )

    func main() {
        value := "123"

        // convert string to int
        number, err := strconv.ParseInt(value, 10, 0)
        if err != nil {
            fmt.Println(err)
        }

        // we now have an int
        fmt.Println("Result:", number)
        if number == 123 {
            fmt.Println("Is number:", true)
        }
    }
    ```

* ParseInt interprets a string `s` in the given `base` (0, 2 to 36) and bit `size` (0 to 64) and returns the corresponding value i.

* If base == 0, the base is implied by the string's prefix: base 16 for `0x`, base 8 for `0`, and base 10 otherwise. For bases 1, below 0 or above 36 an error is returned.

* The `bitSize` argument specifies the integer type that the result must fit into. Bit sizes 0, 8, 16, 32, and 64 correspond to int, int8, int16, int32, and int64. For a bitSize below 0 or above 64 an error is returned.

<!-- markdownlint-disable MD002 -->
&nbsp;

## ✰ Atoi

***

* This function bears the same name as the one from the `C` standard library. In Go it invokes ParseInt with a base of 10 and a bit size of 0.

* Go [program](https://play.golang.org/p/S3OQYXWocQC) that uses **strconv.Atoi**.

    ```go
    package main

    import (
        "fmt"
        "strconv"
    )

    func main() {
        value := "123"

        // convert string to int
        number, err := strconv.Atoi(value)
        if err != nil {
            fmt.Println(err)
        }

        // we now have an int
        fmt.Println("Result:", number)
        if number == 123 {
            fmt.Println("Is number:", true)
        }
    }
    ```
&nbsp;

## ✰ Benchmark test

***

* Often we need to convert a string into an integer. This benchmark compares `ParseInt` and `Atoi`. It converts `"1234"` into an integer with each method.

* This test based on go version `go1.10.1 linux/amd64`.

    ```go
    package main

    import (
        "log"
        "runtime"
        "strconv"
        "testing"
    )

    var val = "1234"

    // BenchmarkAtoi check performance of Atoi
    func BenchmarkAtoi(b *testing.B) {

        // run garbage collector and reset timer
        runtime.GC()
        b.ResetTimer()

        // use Atoi
        for i := 0; i < b.N; i++ {
            _, err := strconv.Atoi(val)
            if err != nil {
                log.Fatal(err)
            }
        }
    }

    // BenchmarkParseInt check performance of ParseInt
    func BenchmarkParseInt(b *testing.B) {

        // run garbage collector and reset timer
        runtime.GC()
        b.ResetTimer()

        // use ParseInt
        for i := 0; i < b.N; i++ {
            _, err := strconv.ParseInt(val, 10, 0)
            if err != nil {
                log.Fatal(err)
            }
        }
    }
    ```

* Result

  ```sh
    BenchmarkAtoi-4       300000000     13.8 ns/op
    BenchmarkParseInt-4   200000000     27.4 ns/op
  ```

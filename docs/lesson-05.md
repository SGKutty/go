---
layout: page
title: String Concatenation
---

***
&nbsp;

* Concatenate string literals (string enclosed in double quotes).

* To concatenate strings simply, use `+` operator.

* However, if strings are concatenated by + operator, new string object is generated.

* We can prevent unnecessary string object from generation by using `bytes.Buffer`.

* [Play ground](https://play.golang.org/p/YIPv0mLSsRb)

    ```go
        package main

        import (
            "bytes"
            "fmt"
        )

        func main() {
            var buffer bytes.Buffer

            for i := 0; i < 100; i++ {
                buffer.WriteString("a")
            }

            fmt.Println(buffer.String())
        }
    ```
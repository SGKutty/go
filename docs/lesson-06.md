---
layout: page
title: Execute external command
---

***
&nbsp;

* Execute external command which does not need standard input/output.

* In this sample, execute `touch` command on Linux to create a file `panda.txt`, by golang.

    ```go
        package main

        import (
            "fmt"
            "os/exec"
        )

        func main() {
            cmd := exec.Command("touch", "panda.txt")
            err := cmd.Run()
            if err != nil {
                fmt.Printf("Error occurs")
            }
        }

    ```
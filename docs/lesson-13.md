---
layout: page
title: 13 - Go Files
---
***
<!-- markdownlint-disable MD002 -->

## ✰ bufio

***

> A file contains many lines. In Go we can use the __bufio__ package to read in all the lines in this file inside a loop. With `Scan` and `Text` we get a string for each line.

&nbsp;

### ✰ Example

***

➭ [os.Open](https://golang.org/pkg/os/#Open)

* This returns a `*File` descriptor. We can pass the result of Open() to the bufio.NewScanner method.

➭ [bufio.NewScanner](https://golang.org/pkg/bufio/#NewScanner)

* This create a new `*Scanner`. The File we pass to this method is accessed through its Reader interface.

➭ [bufio.Scanner.Scan](https://golang.org/pkg/bufio/#NewScanner)

* This advances to the next part of the file and returns true if there is more data. And `Text()` creates a string from the current line.

```go
    package main

    import (
        "bufio"
        "fmt"
        "os"
    )

    func main() {
        // open file.
        f, err := os.Open("sample.txt")
        if err != nil {
            panic(err)
        }

        // read each lines.
        scanner := bufio.NewScanner(f)
        for scanner.Scan() {
            line := scanner.Text()
            fmt.Println(line)
        }
    }
```

➭ [bufio.ScanWords](https://golang.org/pkg/bufio/#ScanWords)

* A file sometimes contains words. We can get each word separately as a string with the Scan() and Text() methods. First we must call Split.

```go
    package main

    import (
        "bufio"
        "fmt"
        "os"
    )

    func main() {
        // open file.
        f, err := os.Open("sample.txt")
        if err != nil {
            panic(err)
        }

        // new scanner.
        scanner := bufio.NewScanner(f)

        // set the Split method to ScanWords.
        scanner.Split(bufio.ScanWords)

        // scan each words.
        for scanner.Scan() {
            line := scanner.Text()
            fmt.Println(line)
        }
    }
```

&nbsp;

## ✰ ioutil

***

> With [ioutil.ReadAll](https://golang.org/pkg/io/ioutil/#ReadAll) we can get the entire contents of a file in a byte slice or a string.

➭ [bufio.NewReader](https://golang.org/pkg/bufio/#NewReader)

* NewReaderSize returns a new Reader whose buffer has at least the specified size. If the argument io.Reader is already a Reader with large enough size, it returns the underlying Reader.

➭ [ioutil.ReadAll](https://golang.org/pkg/io/ioutil/#ReadAll)

* ReadAll reads until an error or EOF and returns the data it read as slice of byte.

```go
    package main

    import (
        "bufio"
        "fmt"
        "io/ioutil"
        "os"
    )

    func main() {
        // open file.
        f, err := os.Open("sample.txt")
        if err != nil {
            panic(err)
        }

        // get reader.
        reader := bufio.NewReader(f)

        // read all content.
        content, err := ioutil.ReadAll(reader)
        if err != nil {
            panic(err)
        }

        // file content.
        fmt.Println(string(content))
    }
```

➭ [ioutil.ReadFile](https://golang.org/pkg/io/ioutil/#ReadFile)

* If you just want the content as `string`, then the simple solution is to use the `ReadFile` function from the io/ioutil package. This function returns a slice of bytes which you can easily convert to a string.

```go
    package main

    import (
        "fmt"
        "io/ioutil"
    )

    func main() {

        // read file content.
        b, err := ioutil.ReadFile("file.txt")
        if err != nil {
            fmt.Print(err)
        }

        // file content.
        fmt.Println(string(b))
    }
```
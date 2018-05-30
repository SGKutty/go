---
layout: page
title: Setup
---

***
<!-- markdownlint-disable MD002 -->

## ✰ Linux, Mac OS X, and FreeBSD tarballs:

***

* [Download the archive](https://golang.org/dl/) and extract it into `/usr/local` and creating a Go tree in `/usr/local/go`

  ```sh
    tar -C /usr/local -xzf go$VERSION.$OS-$ARCH.tar.gz
  ```

* Choose the archive file appropriate for your installation. 

* If you are installing Go version `1.10.1` for [64-bit x86](https://golang.org/dl) on Linux, The archive you want is called   go1.10.1.linux-amd64.tar.gz

* Typically these commands must be run as root or through `sudo`

* Add `/usr/local/go/bin` to the PATH environment variable. 

* You can do this by adding this line to `/etc/profile` (system-wide) or `$HOME/.profile`

     ```sh
       export PATH=$PATH:/usr/local/go/bin
     ```
&nbsp;

## ✰ Installing to a custom location

***

* The Go binary distributions assume they will be installed in `/usr/local/go`, but it is possible to install the Go tools to a different location. 

* In this case you must set the `GOROOT` environment variable to point to the directory in which it was installed.

* For example, if you installed Go to your `Home` directory you should add commands like the following to `$HOME/.profile`

   ```sh
   export GOROOT=$HOME/go1.X
   export PATH=$PATH:$GOROOT/bin
   ```

&nbsp;

## ✰  Test your installation

***

* Check that Go is installed correctly by setting up a workspace and building a simple program, as follows.

* Create your [workspace](https://golang.org/doc/code.html#Workspaces) directory in $HOME/go.

* If you'd like to use a different directory, you will need to set the [GOPATH](https://golang.org/doc/code.html#GOPATH)    environment variable.

* Next, make the directory `src/test` inside your [workspace](https://golang.org/doc/code.html#Workspaces) and in that directory create a file named `hello.go` that looks like:

    ```golang
    package main

    import "fmt"

    func main() {
      fmt.Printf("Welcome to Golang")
    }
    ```

* Then build it with the go tool

    ```sh
      cd $GOPATH/src/test
      go build
    ```

* The command above will build an executable named `test` in the directory alongside your source code. Execute it to see the greeting:

  ```sh
   ./test
  ```

* If you see the `Welcome to Golang` message then your Go installation is successful.

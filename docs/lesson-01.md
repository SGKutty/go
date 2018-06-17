---
layout: page
title: 01 - Setup
---

***
<!-- markdownlint-disable MD002 -->

## ✰ Linux, Mac OS X, and FreeBSD tarballs

***

* [Download the archive](https://golang.org/dl/) and extract it into `/usr/local` and creating a Go tree in `/usr/local/go`.

  ```sh
    tar -C /usr/local -xzf go$VERSION.$OS-$ARCH.tar.gz
  ```

* Choose the archive file appropriate for your installation.

* If you are installing Go version `1.10.1` for [64-bit x86](https://golang.org/dl) on Linux, The archive you want is called   `go1.10.1.linux-amd64.tar.gz`.

* Typically these commands must be run as root or through `sudo`.

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

* For example, if you installed Go to your `Home` directory you should add commands like the following to `$HOME/.profile`.

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

* The command above will build an executable named `test` in the directory alongside your source code. Execute it to see the greeting.

  ```sh
   ./test
  ```

* If you see the `Welcome to Golang` message then your Go installation is successful.

&nbsp;

## ✰ How I use GOPATH with multiple workspace

***

* First off, I want to make it clear I have a fixed **GOPATH** that I do not change per project.

* I do make use of the fact that the GOPATH environment variable is defined as a list of places rather than a single folder.

* The [GOPATH](https://golang.org/cmd/go/#hdr-GOPATH_environment_variable) environment variable lists places to look for Go code. On Unix, the value is a colon-separated string. On Windows, the value is a semicolon-separated string.

* My GOPATH consists of 3 `workspaces`, The **first** one is my **landing workspace**. Since it's listed first, whenever I go get any new package, it always ends up in this workspace.

* Go searches each directory listed in GOPATH to find source code, but new packages are always downloaded into the first directory in the list.

  ```sh
    export GOPATH=/home/kutty/golib
    export PATH=$PATH:$GOPATH/bin
  ```

* I make it a rule to never do any development in there, so it's always completely safe to clean this folder whenever it gets too large.

* My **second** workspace is for **all my personal Go packages** and any other packages I may want to favorite or do some development on.

  ```sh
    export GOPATH=$GOPATH:/home/kutty/gocode
  ```

* My **third** workspace is dedicated to the **private Go packages** from my work, and their dependencies. It's convenient to have my work packages separate from all my personal stuff.

  ```sh
   export GOPATH=$GOPATH:/home/kutty/gopbm
  ```

* With that setup, multiple GOPATH workspaces feel a lot like `namespaces`. The reason I have more than one is quite similar why one might want to break a large Go package into several `.go` files.

* The result is effectively the same since multiple .go files share the same scope but allow one to have `namespaces`.
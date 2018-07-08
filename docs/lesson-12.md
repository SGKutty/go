---
layout: page
title: 12 - Go List Files
---

***
<!-- markdownlint-disable MD002 -->

> Here we explain how to get a list of files inside a folder on the filesystem.

&nbsp;

<!-- markdownlint-disable MD002 -->

## ✰ [filepath.Walk](https://golang.org/pkg/path/filepath/#Walk)

***

* The `path/filepath` stdlib package provides the handy Walk function. It automatically scans subdirectories too.

    ```go
        package main

        import (
            "fmt"
            "os"
            "path/filepath"
            "strings"
        )

        func main() {
            var files []string

            // path
            root := "/some/folder/to/scan"

            // go through each folder
            err := filepath.Walk(root, func(path string, info os.FileInfo, err error) error {

                // error check.
                if err != nil {
                    fmt.Printf("prevent panic by handling failure accessing a path %q: %v\n", path, err)
                    return err
                }

                // filer mp4 files.
                if filepath.Ext(path) == ".mp4" {
                    files = append(files, path)
                }
                return nil
            })
            if err != nil {
                panic(err)
            }
            for _, file := range files {
                fmt.Println(file)
            }
        }
    ```

* __filepath.Walk__ accepts a string pointing to the root folder, and a `func` with signature

    ```go
        type WalkFunc func(path string, info os.FileInfo, err error) error
    ```

* This function is called for each iteration of the folder scan.

* The `info` variable of type [os.FileInfo](https://golang.org/pkg/os/#FileInfo). This variable will provide many information about files like name, size, mode, last-modified time and underlying data source.

* For example we could avoid processing folders by adding

    ```go
        if info.IsDir() {
            return nil
        }
    ```

* You can exclude (or include) files to the slice based on their extension, by using [filepath.Ext](https://golang.org/pkg/path/filepath/#Ext) and passing the file path.

    ```go
        if filepath.Ext(path) == ".dat" {
            return nil
        }
    ```

* We could store the file name instead of the file path using:

    ```go
        files = append(files, info.Name())
    ```

* And we could also define the __WalkFunc__ in a separate closure. We just need to pass a pointer to files in visit:

    ```go
        package main

        import (
            "fmt"
            "os"
            "path/filepath"
        )

        func main() {
            var files []string

            // path
            root := "/some/folder/to/scan"

            // walk through files
            err := filepath.Walk(root, visit(&files))
            if err != nil {
                panic(err)
            }

            // all files
            for _, file := range files {
                fmt.Println(file)
            }
        }

        // go through each folder.
        func visit(files *[]string) filepath.WalkFunc {
            return func(path string, info os.FileInfo, err error) error {
                // error check.
                if err != nil {
                    fmt.Printf("prevent panic by handling failure accessing a path %q: %v\n", path, err)
                    return err
                }

                // filer mp4 files.
                if filepath.Ext(path) == ".mp4" {
                    *files = append(*files, path)
                }
                return nil
            }
        }
    ```

&nbsp;

## ✰ [ioutil.ReadDir](https://golang.org/pkg/io/ioutil/#ReadDir)

***

> ReadDir reads the directory named by dirname and returns a list of directory entries sorted by filename.

* Here is an example from the docs. `ioutil.ReadDir` takes a folder path as a string and returns a slice of [os.FileInfo](https://golang.org/pkg/os/#FileInfo), Which we described above.

    ```go
        package main

        import (
            "fmt"
            "io/ioutil"
            "log"
        )

        func main() {
            // path
            root := "/home/kutty/Videos"

            // read dir
            files, err := ioutil.ReadDir(root)
            if err != nil {
                log.Fatal(err)
            }

            // display all files and dirs
            for _, file := range files {
                fmt.Println(file.Name())
            }
        }
    ```

&nbsp;

## ✰ [os.File.Readdir](https://golang.org/pkg/os/#File.Readdir)

***

* Internally, `ioutil.ReadDir` is implemented as

    ```go
        // ReadDir reads the directory named by dirname and returns
        // a list of directory entries sorted by filename.
        func ReadDir(dirname string) ([]os.FileInfo, error) {

            // open dir
            f, err := os.Open(dirname)
            if err != nil {
                return nil, err
            }

            // read dir
            list, err := f.Readdir(-1)

            // close
            f.Close()
            if err != nil {
                return nil, err
            }

            // sort items
            sort.Slice(list, func(i, j int) bool { return list[i].Name() < list[j].Name() })
            return list, nil
        }
    ```
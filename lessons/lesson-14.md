---
layout: page
title: 14 - Testing
---
***

➩ **Testing** is built right into the go tools and the standard library. Testing needs to be a vital part of the development process because it can save you a tremendous amount of time throughout the life cycle of the project.

➩ **Benchmarking** is also a very powerful tool tied to the testing functionality. Aspect of your code can be setup to be benchmarked for performance reviews

➩ **Profiling** provides a view of the interactions between functions and which functions are most heavily used.

&nbsp;

## Code Review
***

- Basic Unit [Test](https://github.com/g-kutty/go-code/blob/master/testing/tests/example1/download_test.go).

- Table Unit [Test](https://github.com/g-kutty/go-code/blob/master/testing/tests/example2/table_test.go).

- Mocking [Web Server](https://github.com/g-kutty/go-code/blob/master/testing/tests/example3/web_test.go) Response.

- Testing Internal [Endpoints](https://github.com/g-kutty/go-code/blob/master/testing/tests/example4/handlers/handler_test.go).

- Example [Test](https://github.com/g-kutty/go-code/blob/master/testing/tests/example4/handlers/handler_example_test.go):

  - Example tests is also used to show `examples` in godoc.

    > godoc -http=:6060

- Sub Tests:

  - Sub [Test](https://github.com/g-kutty/go-code/blob/master/testing/tests/example5/sub_test.go)

    - Real power of sub test, we can limit test case by name.

        > go test -run TestParallelDownload/statusok -v

  - Parallel [Test](https://github.com/g-kutty/go-code/blob/master/testing/tests/example5/sub_parallel_test.go)

&nbsp;

## Coverage
***

- Making sure your tests cover as much of your code as possible is critical. Go's testing tool allows you to create a profile for the code that is executed during all the tests and see a visual of what is and is not covered.

  ```sh
    go test -coverprofile cover.out
    go tool cover -html=cover.out
  ```

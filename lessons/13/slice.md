---
layout: page
title: 14 - Slice
---
***

➩ __Slices__ are an incredibly important data structure in Go. They form the basis for how we manage and manipulate data in a flexible, performing and dynamic way. It is incredibly important for all Go programmers to learn how to uses slices.

&nbsp;

- Slices are like dynamic arrays with special and built-in functionality.

- There is a difference between a slices length and capacity and they each service a purpose.

- Slices allow for multiple __views__ of the same underlying array.

- Slices can grow through the use of the built-in function append.

- Creation styles ([playground](https://play.golang.org/p/gk_yXh8PE6a))

  - Literal styles

    ```go
      friends := []string{"Tony", "Cyril", "Jishnu", "Eldho"}
    ```

  - Via make function

    ```go
      a := make([]int, 10) //create slice with capacity and length == 10

      b := make([]int, 10, 100) //slice with length == 10 and capacity == 100
    ```
- `len` function returns length of slice.

- `cap` function returns length of underlying array.

- `append` function to add element to slice.

- The `copy` function copies elements from a source slice into a destination slice.

- May cause expensive copy operation if underlying array is too small.

- Copies refer to __same__ underlying array.
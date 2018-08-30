---
layout: page
title: 10 - Arrays
---
***

➩ __Arrays__ are a special data structure in Go that allow us to allocate contiguous blocks of fixed size memory.

➩ Arrays have some special features in Go related to how they are declared and viewed as types.

&nbsp;

- Collection of items with same type.

- Arrays are fixed length data structures that can't change([playground](https://play.golang.org/p/ohzYmfBKYTC)).

- Declaration styles

    ```go
        a := [3]int{1,2,3}

        a := [...]int{1,2,3}

        var a [3]int
    ```

- Access via zero-based index.

    ```go
        a := [3]int{1,2,3}

        if a[1] == 3{

            print(true)

        }
    ```

- `len` function returns size of array.

- Copies refer to different underlying data.

- Arrays of different sizes are considered to be of different types([playground](https://play.golang.org/p/ZZqgWTnN-a-)).

- Memory is allocated as a contiguous block([playground](https://play.golang.org/p/mO_zQWtpFNC)).

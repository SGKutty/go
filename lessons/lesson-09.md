---
layout: page
title: 09 - Functions
---
***

<!-- markdownlint-disable MD002 MD022-->

➩ __Functions__ are at the core of the language. They provide a mechanism to group and organize our code to separate and distinct pieces of functionality.

➩ They can be used to provide an API to the packages we write and are a core component to concurrency.

&nbsp;

## Basic Syntax
***

```go
    func foo(){
        ....
    }
```

&nbsp;

## Parameters
***

- Comma delimited list of variables and types([playground](https://play.golang.org/p/SoeZTEgCV4h)).

    ```go
        func foo(a string, b int){
            ....
        }
    ```

- Parameters of same type list type once.

    ```go
        func foo(a, b int){
            ....
        }
    ```
- When pointers are passed in, the function can change the value in the caller([playground](https://play.golang.org/p/H13Srx66yFO)).

  - This is always `true` for data of slices and maps.

- Use `variadic` parameters to send list of same types in([playground](https://play.golang.org/p/db6HYJKqFUf)).

  - Must be last parameter.

  - Received as a slice.

    ```go
        func foo (s string, v ...int){
            ....
        }
    ```
&nbsp;

## Return values
***

- Single return values just list type.

    ```go
        func foo () int{
            ....
        }
    ```
- Multiple return values list types surrounded by parentheses.

    ```go
        func foo () (int, error){
            ....
        }
    ```
- Can use named return values([playground](https://play.golang.org/p/a-91E5mSD_0)).

  - Initializes returned variables.

  - Return using return keyword on its own.

- Can return address of local variables([playground](https://play.golang.org/p/mGjVOxMMbtV).

  - Automatically promoted from local memory (`stack`) to shared memory (`heap`).

- The blank identifier can be used to ignore return values.

&nbsp;

## Anonymous functions ([playground](https://play.golang.org/p/0Zc39_sTM7K))
***

- Function don’t have names and can be Immediately invoked.

- Assigned to a variable or passed as an argument to a function.

- Type signature is like function signature, with no parameter names:

    ```go
        var f func (string, string, int) (int, error){
            ....
        }
    ```
---
layout: page
title: 05 - Pointers
---
***

<!-- markdownlint-disable MD002 MD022 -->

➩ __Pointers__ provide a way to share data across function boundaries. Having the ability to share and reference data with a pointer provides flexbility. 

➩ It also helps  our programs minimize the amount of memory they need and can add some extra performance.

&nbsp;

- Use pointers to share data.

- Values in Go are always pass by value.

- `Value of`, what's in the box. `Address of`( & ), where is the box.

- The (*) operator declares a pointer variable and the Value that the pointer points to.

&nbsp;

## Creating and Dereferencing([playground](https://play.golang.org/p/DFEm_CRBDXF))
***

- Pointer type use an asterisk(*) as a prefix to type pointed to.

  - `*int` - a pointer to an integer.

- Use addressof operator (&) to get address of variable .

- Dereferencing a pointer by preceding with an asterisk (*).

- Complex types (e.g structs) are automatically dereferenced.

&nbsp;

## Create pointer to objects
***

- Can use the addressof operator (&) if value type already exists.

  ```go
    ms := myStruct{foo : 42}

    p := &ms
  ```

- Use addressof operator before initializer.

  ```go
    ms := &myStruct{foo : 42}
  ```

- Use `new` keyword.

  - Can’t initialize fields at the same time

&nbsp;

## Types with internal pointers
***

- All assignment operations in go are `copy` operations.

- Slices and maps contain internal pointers, so copies point to same underlying data.
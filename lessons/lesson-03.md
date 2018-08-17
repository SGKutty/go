---
layout: page
title: 03 - Variables
---
***

<!-- markdownlint-disable MD002 -->

➩ __Variables__ are at the heart of the language and provide the ability to read from and write to memory.

➩ In Go, access to memory is type safe. This means the compiler takes type seriously and will not allow us to use variables outside the scope of how they are declared.

&nbsp;

- Understanding type is crucial to writing good code and understanding code.

- Variable declaration([playground](https://play.golang.org/p/OQVVV1RlNLe)):

  - var foo int

  - var foo int = 20

  - foo := 20

- Can’t redeclare variables, but can shadow them([playground](https://play.golang.org/p/DfLdVlFopd4))

  - All variable must be used.

- Visibility([playground](https://play.golang.org/p/FzcyhCCEWKD))

  - The scope of a constant or variable identifier declared inside a function begins at the end of the ConstSpec or VarSpec and ends at the end of the innermost containing block.

  - Package level variables with first letter start with lowercase is only available in that package.

  - Package level variables with first letter start with uppercase is for exporting.

- Naming conventions

  - Pascal or camelCase.

  - Capitalize acronyms (HTTP, URL etc..).

  - As short as reasonable.

  - Longer names for longer lives.

- Type Conversion([playground](https://play.golang.org/p/YBazA_jliwM))

  - T(v) converts the value v to the type T.

  - Use `strconv` package for strings.
---
layout: page
title: 16 - Goroutines
---
***

➩ **Goroutines** are functions that are created and scheduled to be run independently by the Go scheduler. The Go scheduler is responsible for the management and execution of goroutines.

- Goroutines are functions that are scheduled to run independently.

- We must always maintain an account of running goroutines and shutdown cleanly.

- Concurrency is not parallelism ([blog](https://blog.golang.org/concurrency-is-not-parallelism)).

  - **Concurrency** is about dealing with lots of things at once.

  - **Parallelism** is about doing lots of things at once.

&nbsp;

## Design Guidelines
***

- Learn about the design [guidelines](https://george-kj.github.io/go-tour/lessons/15/design_philosophy) for concurrency.

&nbsp;

## How the scheduler works
***

  ![scheduler_working](https://george-kj.github.io/go-tour/lessons/15/images/scheduler.png?raw=true)

&nbsp;

## Difference between concurrency and parallelism
***

  ![concurrency_vs_parallelism](https://george-kj.github.io/go-tour/lessons/15/images/parallel.png?raw=true)

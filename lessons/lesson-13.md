---
layout: page
title: 13 - Goroutines
---
***

<!-- markdownlint-disable MD002 MD022-->

➩ **Goroutines** are functions that are created and scheduled to be run independently by the Go scheduler. The Go scheduler is responsible for the management and execution of goroutines.

- `Goroutines` are functions that are scheduled to run independently.

- We must always maintain an account of running goroutines and shutdown cleanly.

- `Concurrency` is not parallelism.

  - **Concurrency** is about dealing with lots of things at once.
  
  - **Parallelism** is about doing lots of things at once.

&nbsp;

## Design Philosophy
***

### The application must `startup` and `shutdown` with integrity

- Know how and when every goroutine you create terminates.

- All goroutines you create should terminate before main returns.

- Applications should be capable of shutting down on demand, even under load, in a controlled way.

- You want to stop accepting new requests and finish the requests you have (load shedding).

&nbsp;

### Identify and monitor critical points of `back pressure` that can exist inside your application

- `Channels`, `mutexes` and `atomic functions` can create back pressure when goroutines are required to wait.

- A little back pressure is good, it means there is a good balance of concerns.

- A lot of back pressure is bad, it means things are `imbalanced`.

- Back pressure that is imbalanced will cause:

  - Failures inside the software and across the entire platform.

  - Your application to collapse, implode or freeze.

- Measuring back pressure is a way to measure the health of the application.

&nbsp;

### Rate limit to prevent overwhelming back pressure inside your application

- Every system has a `breaking point`, you must know what it is for your application.

- Applications should reject new requests as early as possible once they are overloaded.

  - Don’t take in more work than you can reasonably work on at a time.

  - Push back when you are at critical mass. Create your own external back pressure.

- Use an external system for rate limiting when it is reasonable and practical.

&nbsp;

### Use timeouts to release the back pressure inside your application

- No request or `task` is allowed to `take forever`.

- Identify how long users are willing to wait.

- Higher-level calls should tell lower-level calls how long they have to run.

- At the top level, the user should decide how long they are willing to wait.

- Use the Context package.

  - Functions that users wait for should take a Context.

    - These functions should select on <-ctx.Done() when they would otherwise block indefinitely.

  - Set a timeout on a Context only when you have good reason to expect that a function's execution has a real time limit.

  - Allow the upstream caller to decide when the Context should be canceled.

  - Cancel a Context whenever the user abandons or explicitly aborts a call.

&nbsp;

### Architect applications to:

- Identify problems when they are happening.

- Stop the bleeding.

- Return the system back to a normal state.

&nbsp;

## How the scheduler works
***
  ![scheduler_working](https://github.com/g-kutty/go-tour/blob/gh-pages/public/images/scheduler_working.png?raw=true)

&nbsp;

## Difference between concurrency and parallelism
***
  ![concurrency_vs_parallelism](https://github.com/g-kutty/go-tour/blob/gh-pages/public/images/concurrency_vs_parallelism.png?raw=true)
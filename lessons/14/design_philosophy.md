---
layout: page
title:
---

<!-- ➩ Design Guidelines -->

## Language Mechanics
***

- Use channels to orchestrate and coordinate goroutines.

  - Focus on the signaling semantics and not the sharing of data.

  - Signaling with data or without data.

- Unbuffered channels:

  - Receive happens before the Send.

  - Benefit: 100% guarantee the signal has been received.

  - Cost: Unknown latency on when the signal will be received.

- Buffered channels:

  - Send happens before the Receive.

  - Benefit: Reduce blocking latency between signaling.

  - Cost: No guarantee when the signal has been received.

    - The larger the buffer, the less guarantee.

    - Buffer of 1 can give you one delayed send of guarantee.

- Closing channels:

  - Close happens before the Receive. (like Buffered)

  - Signaling without data.

  - Perfect for signaling cancellations and deadlines.

- NIL channels:

  - Send and Receive block.

  - Turn off signaling.

  - Perfect for rate limiting or short term stoppages.

&nbsp;

## Design Philosophy
***

Depending on the problem you are solving, you may require different channel semantics. Depending on the semantics you need, different architectural choices must be taken.

- If any given Send on a channel `CAN` cause the sending goroutine to block:

  - Not allowed to use a Buffered channel larger than 1.

  - Buffers larger than 1 must have reason/measurements.

  - Must know what happens when the sending goroutine blocks.

- If any given Send on a channel `WON'T` cause the sending goroutine to block:

  - You have the exact number of buffers for each send.

    - Fan Out pattern

  - You have the buffer measured for max capacity.

    - Drop pattern

- Less is more with buffers.

  - Don’t think about performance when thinking about buffers.

  - Buffers can help to reduce blocking latency between signaling.

    - Reducing blocking latency towards zero does not necessarily mean better throughput.

    - If a buffer of one is giving you good enough throughput then keep it.

    - Question buffers that are larger than one and measure for size.

    - Find the smallest buffer possible that provides good enough throughput.
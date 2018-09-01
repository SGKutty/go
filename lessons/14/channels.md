---
layout: page
title: 14 - Channel
---
***

➩ **Channels** allow goroutines to communicate with each other through the use of signaling semantics.

➩ Channels accomplish this signaling through the use of sending/receiving data or by identifying state changes on individual channels.

➩ Don't architect software with the idea of channels being a queue, focus on signaling and the semantics that simplify the orchestration required.

&nbsp;

## Design Guidelines
***

- Learn about the design [guidelines](https://g-kutty.github.io/go-tour/lessons/14/design_philosophy) for channels.

&nbsp;

## Guarantee Of Delivery
***

- The Guarantee Of Delivery is based on one question: “Do I need a guarantee that the signal sent by a particular goroutine has been received?”

    ![guarantee_of_delivery](https://g-kutty.github.io/go-tour/lessons/14/images/guarantee_of_delivery.png?raw=true)

&nbsp;

## Signaling With Or Without Data
***

- When you are going to signal with `data`, there are three channel configuration options you can choose depending on the type of `guarantee` you need.

    ![signaling_with_data](https://g-kutty.github.io/go-tour/lessons/14/images/signaling_with_data.png?raw=true)

- Signaling without data serves the main purpose of cancellation. It allows one goroutine to signal another goroutine to cancel what they are doing and move on. Cancellation can be implemented using both `unbuffered` and `buffered` channels.

    ![signaling_without_data](https://g-kutty.github.io/go-tour/lessons/14/images/signaling_without_data.png?raw=true)

&nbsp;

## State
***

- The behavior of a channel is directly influenced by its current `State`. The state of a channel can be `nil`, `open` or `closed`.

    ![state](https://g-kutty.github.io/go-tour/lessons/14/images/state.png?raw=true)
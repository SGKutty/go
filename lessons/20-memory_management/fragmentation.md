---
layout: page
title:
---
***

- __Fragmentation__, in the context of a hard disk, is a condition in which the contents of a single file stored in different locations on the disk rather than in a contiguous space. This results in __inefficient__ use of storage space as well as occasional performance __degradation__.

- Let's say you write `document A`. Its gets placed in the next available space on your drive.

    ![doc_a.png](https://g-kutty.github.io/go-tour/lessons/20-memory_management/images/doc_a.png?raw=true)

- Then you write `document B`. It gets placed right next to document A.

    ![doc_b.png](https://g-kutty.github.io/go-tour/lessons/20-memory_management/images/doc_b.png?raw=true)

- What happens if you then go add another page to `document A`?

- It has to go into the space at the other end of `document B`, Or somewhere even further away, If it has been awhile since you originally wrote document A.

    ![doc_a_expand.png](https://g-kutty.github.io/go-tour/lessons/20-memory_management/images/doc_a_expand.png?raw=true)

- The same steps will be retained. You are about to add another document or expand the existing document.

    ![doc_c.png](https://g-kutty.github.io/go-tour/lessons/20-memory_management/images/doc_c.png?raw=true)
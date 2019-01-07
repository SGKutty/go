---
layout: page
title: 15 - Map
---
***

## Introduction
***

- __Maps__ provide a data structure that allow for the storage and management of key/value pair data.

- Key type must have an == operation (no map, slice, or func as key).

- Operation run in constant expected time.

- Iterating over a map is always random.

- Operations:

  - __Construct__ : m := map[key]value{}

  - __Insert__ : m[k] = v

  - __Lookup__ : v = m[k]

  - __Delete__ : delete(m, k)

  - __Iterate__ : for k, v := range m

  - __Size__ : len(m)

  - __Availability__ : _, ok := m[k]

&nbsp;

## Map lookup implementation
***

- Maps in Go are implemented as a hash table.

- The hash table for a Go map is structured as an array of buckets. The number of buckets is always equal to a power of 2.

- When a map operation is performed, such as `map[key] = value`, a hash key is generated against the key that is specified.

- The low order bits (LOB) of the generated hash key is used to select a bucket.

    &nbsp;

    ![buckets.png](https://george-kj.github.io/go-tour/lessons/14-maps/images/buckets.png?raw=true)

    &nbsp;

- Once a bucket is selected, the key/value pair needs to be stored, removed or looked up, depending on the type of operation.

- If we look inside any bucket, we will find two data structures. __First__, there is an array with the top 8 high order bits (`HOB`) from the same hash key.

- This array distinguishes each individual key/value pair stored in the respective bucket.

- __Second__, there is an array of bytes that store the key/value pairs. The byte array packs all the keys and then all the values together for the respective bucket.

    &nbsp;

    ![map_hash_table.png](https://george-kj.github.io/go-tour/lessons/14-maps/images/map_hash_table.png?raw=true)

    &nbsp;

- When we are `iterating` through a map, the iterator walks through the array of buckets and then return the key/value pairs in the order they are laid out in the byte array. This is why maps are unsorted collections.

- The hash keys determines the walk order of the map because they determine which buckets each key/value pair will end up in.

    &nbsp;

    ![bucket.png](https://george-kj.github.io/go-tour/lessons/14-maps/images/bucket.png?raw=true)

    &nbsp;

## Memory and Bucket Overflow
***

- There is a reason to pack all the keys and then all the values together. If the keys and values were stored like key/value/key/value, `padding` allocations between each key/value pair would be needed to maintain proper alignment boundaries.

- An example where this would apply is with a map that looks like this:

    ```go
    map[int64]int8
    ```

- The 1 byte value in this map would result in 7 extra bytes of padding per key/value pair. By packing the key/value pairs as key/key/value/value, the padding only has to be appended to the end of the byte array and not in between.

- Eliminating the padding bytes saves the bucket and the map a good amount of memory. To learn more about alignment boundaries, read this post [![go_to.png](https://george-kj.github.io/go-tour/public/images/go_to.png?raw=true)](https://george-kj.github.io/go-tour/lessons/19-understanding_types/index)

- A bucket is configured to store only 8 key/value pairs. Is a ninth key needs to be added to a bucket that is full, an overflow bucket is created and reference from inside the respective bucket.

    &nbsp;
    ![growing_bucket.png](https://george-kj.github.io/go-tour/lessons/14-maps/images/growing_bucket.png?raw=true)
    &nbsp;

- As we continue to add or remove key/value pairs from the map, the efficiency of the map lookups begin to deteriorate. The load threshold values that determine when to grow the hash table are based on these four factors:

  - __Overflow__ : Percentage of buckets which have an overflow bucket.
  - __bytes/entry__ : Number of overhead bytes used per key/value pair.
  - __hitprobe__ : Number of entries that need to be checked when looking up a key.
  - __missprobe__ : Number of entries that need to be checked when looking up an absent key.

- Growing the hash table starts with assigning a pointer called the "old bucket" pointer to the current bucket array.

- Then a new bucket array is allocated to hold `twice` the number of existing buckets. This could result in large allocations, but the memory is not initialized so the allocation is fast.

- Once the memory for the new bucket array is available, the key/value pairs from the old bucket array can be moved or "evacuated" to the new bucket array.

- Evacuations happens as key/value pairs are added or removed from the map. The key/value pairs that are together in an old bucket could be moved to different buckets inside the new bucket array.

- The evacuation algorithm attempts to distribute the key/value pairs evenly across the new bucket array.

    &nbsp;
    ![map_growing.png](https://george-kj.github.io/go-tour/lessons/14-maps/images/map_growing.png?raw=true)
    &nbsp;

- This is a very delicate dance because iterators still need to run through the old bucket has been evacuated. This also affects how key/value pairs are returned during iteration operations. A lot of care has been taken to make sure iterators work as the map grows and expands.

    &nbsp;
    ![map_arch.png](https://george-kj.github.io/go-tour/lessons/14-maps/images/map_arch.png?raw=true)
    &nbsp;

## Compare with other language
***

  ![comparison.png](https://george-kj.github.io/go-tour/lessons/14-maps/images/comparison.png?raw=true)

&nbsp;

## Reference
***

[![image](https://george-kj.github.io/go-tour/public/images/youtube.png?raw=true)](https://www.youtube.com/watch?v=Tl7mi9QmLns&t=1414s_)

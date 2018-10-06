---
layout: page
title: 14 - Map
---
***

➩ __Maps__ provide a data structure that allow for the storage and management of key/value pair data.

&nbsp;

## Basic Syntax
***

- Construct: `m := map[key]value{}`

- Insert: `m[k] = v`

- Lookup: `v = m[k]`

- Delete: `delete(m, k)`

- Iterate: `for k, v := range m`

- Size: `len(m)`

- Availability: `_, ok := m[k]`

- Key type must have an == operation (no map, slice, or func as key).

- Operation run in constant expected time.

- Iterating over a map is always random.

&nbsp;

## Map lookup implementation
***

- Maps in Go are implemented as a hash table.

- The hash table for a Go map is structured as an array of buckets. The number of buckets is always equal to a power of 2.

- When a map operation is performed, such as `map[key] = value`, a hash key is generated against the key that is specified.

- The low order bits (LOB) of the generated hash key is used to select a bucket.

    &nbsp;

    ![buckets.png](https://g-kutty.github.io/go-tour/lessons/14-maps/images/buckets.png?raw=true)

    &nbsp;

- Once a bucket is selected, the key/value pair needs to be stored, removed or looked up, depending on the type of operation.

- If we look inside any bucket, we will find two data structures. __First__, there is an array with the top 8 high order bits (`HOB`) from the same hash key.

- This array distinguishes each individual key/value pair stored in the respective bucket.

- __Second__, there is an array of bytes that store the key/value pairs. The byte array packs all the keys and then all the values together for the respective bucket.

    &nbsp;

    ![map_hash_table.png](https://g-kutty.github.io/go-tour/lessons/14-maps/images/map_hash_table.png?raw=true)

    &nbsp;

- When we are `iterating` through a map, the iterator walks through the array of buckets and then return the key/value pairs in the order they are laid out in the byte array. This is why maps are unsorted collections.

- The hash keys determines the walk order of the map because they determine which buckets each key/value pair will end up in.

    &nbsp;

    ![bucket.png](https://g-kutty.github.io/go-tour/lessons/14-maps/images/bucket.png?raw=true)

    &nbsp;

## Memory and Bucket Overflow
***

- There is a reason to pack all the keys and then all the values together. If the keys and values were stored like key/value/key/value, `padding` allocations between each key/value pair would be needed to maintain proper alignment boundaries.

- An example where this would apply is with a map that looks like this:

    ```go
    map[int64]int8
    ```

- To learn more about `alignment` boundaries, [Go](https://g-kutty.github.io/go-tour/lessons/19-understanding_types/types/)

- The 1 byte value in this map would result in 7 extra bytes of padding per key/value pair. By packing the key/value pairs as key/key/value/value, the padding only has to be appended to the end of the byte array and not in between.

- Eliminating the padding bytes saves the bucket and the map a good amount of memory.

- When buckets get too full, we need to grow the map.

  - Allocate a new array of buckets of twice the size.

  - Copy entires over form the old buckets to the new buckets.

  - Use the new buckets.

- The process of copying is done incrementally, a little bit during each insert or      delete. during copying, operations on the map are bit more expensive.

    ![map_arch.png](https://g-kutty.github.io/go-tour/lessons/14-maps/images/map_arch.png?raw=true)

&nbsp;

## Compare with other language
***

  ![comparison.png](https://g-kutty.github.io/go-tour/lessons/14-maps/images/comparison.png?raw=true)

&nbsp;

## Reference
***

[![image](https://g-kutty.github.io/go-tour/public/images/youtube.png?raw=true)](https://www.youtube.com/watch?v=Tl7mi9QmLns&t=1414s_)
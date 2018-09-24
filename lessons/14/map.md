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

- Choose the bucket for each key so that entries are distributed as evenly as possible.

    ```go
    bucket = h(key)
    ```

&nbsp;

## Map Architecture
***

- Maps in Go are implemented as a hash table.

- The hash table for a Go map is structured as an array of buckets. The number of buckets is always equal to a power of 2.

- When a map operation is performed, such as `colors["Black"] = "#000000"`, a hash key is generated against the key that is specified.

- The low order bits (LOB) of the generated hash key is used to select a bucket.

- Once a bucket is selected, the key/value pair needs to be stored, removed or looked up, depending on the type of operation.

- If we look inside any bucket, we will find two data structures. First, there is an array with the top 8 high order bits (HOB) from the same hash key. This array distinguishes each individual key/value pair stored in the respective bucket

- Second, there is an array of bytes that store the key/value pairs. The byte array packs all the keys and then all the values together for the respective bucket.

&nbsp;

## Map lookup implementation
***

- `hash` := hashfn(key)

- `bucket` := hash % nbuckets

- `extra` := top 8 bits of hash

- `b` := &m.buckets[bucket]

- Check 8 extra bits.

- Pointer to ith key in the bucket.

    ![map_bucket](https://g-kutty.github.io/go-tour/lessons/14/images/map_bucket.png?raw=true)

&nbsp;

## Growing the map
***

- When buckets get too full, we need to grow the map.

  - Allocate a new array of buckets of twice the size.

  - Copy entires over form the old buckets to the new buckets.

  - Use the new buckets.

- The process of copying is done incrementally, a little bit during each insert or      delete. during copying, operations on the map are bit more expensive.

    ![map_in_go](https://g-kutty.github.io/go-tour/lessons/14/images/map_in_go.png?raw=true)

&nbsp;

## Compare with other language
***

  ![maps_in_other_lang](https://g-kutty.github.io/go-tour/lessons/14/images/maps_in_other_lang.png?raw=true)

&nbsp;

## Reference
***

[![image](https://g-kutty.github.io/go-tour/public/images/youtube.png?raw=true)](https://www.youtube.com/watch?v=Tl7mi9QmLns&t=1414s_)

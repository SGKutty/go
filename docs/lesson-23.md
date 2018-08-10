---
layout: page
title: 23 - Map
---
***

<!-- markdownlint-disable MD002 -->
> Maps provide a data structure that allow for the storage and management of key/value pair data.

* The map key must be a value that can be used in an assignment statement.

* Iterating over a map is always random.

&nbsp;

## Basic Syntax

***
  
* Construct: `m := map[key]value{}`

* Insert: `m[k] = v`

* Lookup: `v = m[k]`

* Delete: `delete(m, k)`

* Iterate: `for k, v := range m`

* Size: `len(m)`

* Availability: `_, ok := m[k]`

* Key type must have an == operation (no map, slice, or func as key).

* Operation run in constant expected time.

* Choose the bucket for each key so that entries are distributed as evenly as possible.

    ```go
    bucket = h(key)
    ```

&nbsp;

## Map lookup implementation

***

* `hash` := hashfn(key)

* `bucket` := hash % nbuckets

* `extra` := top 8 bits of hash

* `b` := &m.buckets[bucket]

* Check 8 extra bits.

* Pointer to ith key in the bucket.

    ![map_bucket](https://github.com/g-kutty/go-tour/blob/gh-pages/images/map_bucket.png?raw=true)

&nbsp;

## Growing the map

***

* When buckets get too full, we need to grow the map.

  * Allocate a new array of buckets of twice the size.

  * Copy entires over form the old buckets to the new buckets.

  * Use the new buckets.

* The process of copying is done incrementally, a little bit during each insert or      delete. during copying, operations on the map are bit more expensive.

    ![map_in_go](https://github.com/g-kutty/go-tour/blob/gh-pages/images/map_in_go.png?raw=true)

&nbsp;

## Compare with other language

***

  ![maps_in_other_lang](https://github.com/g-kutty/go-tour/blob/gh-pages/images/maps_in_other_lang.png?raw=true)

&nbsp;

* Reference: [youtube](https://www.youtube.com/watch?v=Tl7mi9QmLns&t=1414s_)

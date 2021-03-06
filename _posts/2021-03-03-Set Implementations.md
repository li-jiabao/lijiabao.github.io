---
title: Set Implementations
author: lijiabao
date: 2020-12-06 01:53:00.764595700 +0800
category: Collections
categories: Collections
tags: Collections
---

# Set Implementations

The `Set` implementations are grouped into general-purpose and special-purpose implementations.

## General-Purpose Set Implementations

There are three general-purpose 
[`Set`](https://docs.oracle.com/javase/8/docs/api/java/util/Set.html) implementations &#151; 
[`HashSet`](https://docs.oracle.com/javase/8/docs/api/java/util/HashSet.html), 
[`TreeSet`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeSet.html), and 
[`LinkedHashSet`](https://docs.oracle.com/javase/8/docs/api/java/util/LinkedHashSet.html). Which of these three to use is generally straightforward. `HashSet` is much faster than `TreeSet` (constant-time versus log-time for most operations) but offers no ordering guarantees. If you need to use the operations in the `SortedSet` interface, or if value-ordered iteration is required, use `TreeSet`; otherwise, use `HashSet`. It's a fair bet that you'll end up using `HashSet` most of the time.

`LinkedHashSet` is in some sense intermediate between `HashSet` and `TreeSet`. Implemented as a hash table with a linked list running through it, it provides **insertion-ordered** iteration (least recently inserted to most recently) and runs nearly as fast as `HashSet`. The `LinkedHashSet` implementation spares its clients from the unspecified, generally chaotic ordering provided by `HashSet` without incurring the increased cost associated with `TreeSet`.

One thing worth keeping in mind about `HashSet` is that iteration is linear in the sum of the number of entries and the number of buckets (the **capacity**). Thus, choosing an initial capacity that's too high can waste both space and time. On the other hand, choosing an initial capacity that's too low wastes time by copying the data structure each time it's forced to increase its capacity. If you don't specify an initial capacity, the default is 16. In the past, there was some advantage to choosing a prime number as the initial capacity. This is no longer true. Internally, the capacity is always rounded up to a power of two. The initial capacity is specified by using the `int` constructor. The following line of code allocates a `HashSet` whose initial capacity is 64.

```

Set&lt;String&gt; s = new HashSet&lt;String&gt;(64);

```

The `HashSet` class has one other tuning parameter called the **load factor**. If you care a lot about the space consumption of your `HashSet`, read the `HashSet` documentation for more information. Otherwise, just accept the default; it's almost always the right thing to do.

If you accept the default load factor but want to specify an initial capacity, pick a number that's about twice the size to which you expect the set to grow. If your guess is way off, you may waste a bit of space, time, or both, but it's unlikely to be a big problem.

`LinkedHashSet` has the same tuning parameters as `HashSet`, but iteration time is not affected by capacity. `TreeSet` has no tuning parameters.

## Special-Purpose Set Implementations

There are two special-purpose `Set` implementations &#151; 
[`EnumSet`](https://docs.oracle.com/javase/8/docs/api/java/util/EnumSet.html) and 
[`CopyOnWriteArraySet`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/CopyOnWriteArraySet.html).

`EnumSet` is a high-performance `Set` implementation for enum types. All of the members of an enum set must be of the same enum type. Internally, it is represented by a bit-vector, typically a single `long`. Enum sets support iteration over ranges of enum types. For example, given the enum declaration for the days of the week, you can iterate over the weekdays. The `EnumSet` class provides a static factory that makes it easy.

```

    for (Day d : EnumSet.range(Day.MONDAY, Day.FRIDAY))
        System.out.println(d);

```

Enum sets also provide a rich, typesafe replacement for traditional bit flags.

```

    EnumSet.of(Style.BOLD, Style.ITALIC)

```

`CopyOnWriteArraySet` is a `Set` implementation backed up by a copy-on-write array. All mutative operations, such as `add`, `set`, and `remove`, are implemented by making a new copy of the array; no locking is ever required. Even iteration may safely proceed concurrently with element insertion and deletion. Unlike most `Set` implementations, the `add`, `remove`, and `contains` methods require time proportional to the size of the set. This implementation is **only** appropriate for sets that are rarely modified but frequently iterated. It is well suited to maintaining event-handler lists that must prevent duplicates.

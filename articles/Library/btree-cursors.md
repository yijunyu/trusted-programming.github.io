---
layout: post
title: BTreeMap cursors
toc: true
---

# Cursor support for `BTreeMap`

```
Amanieu d'Antras
Trustworthiness Software Engineering & Open Source Lab
Huawei Technologies, Inc.
```

One of the fundamental properties of BTreeMap is that it maintains elements in sorted order and enables efficient element lookup in O(log(N)) time. However the current API is overly fitted towards a key-value API like a HashMap and fails to expose the ability to make queries about "nearby" keys. For example, finding the first element whose key is greater than X.

This proposal adds `Cursor` and `CursorMut` types to `BTreeMap` based on [similar](https://doc.rust-lang.org/nightly/std/collections/linked_list/struct.Cursor.html) [types](https://doc.rust-lang.org/nightly/std/collections/linked_list/struct.CursorMut.html) for `LinkedList`.

Benchmarks on a `RangeTree` type (map of non-overlapping ranges to values) show that this improves performance on insert/remove operations by 25% to 50%.

There are some more examples with a detailed explanation in the [ACP](https://github.com/rust-lang/libs-team/issues/141) and [pull request](https://github.com/rust-lang/rust/pull/105641).

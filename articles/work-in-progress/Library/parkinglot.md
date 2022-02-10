---
layout: post
title: parkinglot
---

# Standard Library incorporation of Mutex features

```
Amanieu d'Antras, Mara Bos
Trustworthiness Software Engineering & Open Source Lab
Huawei Technologies, Inc.
```

On most platforms, these structures are currently wrappers around their pthread equivalent, such as `pthread_mutex_t`. These types are not movable, however, forcing us to wrap them in a Box, resulting in an allocation and indirection for our lock types. This also gets in the way of a const constructor for these types, which makes static locks more complicated than necessary.  A proposal for improving `std::sync::{Mutex, RwLock, Condvar}` is
[tracked here](https://github.com/rust-lang/rust/issues/93740), the aim
is to incorporate `parkinglot` into the standard library so that eventually the size of binary will be significantly reduced while supporting the synchronization features.

## Updates
See this [issue](https://github.com/rust-lang/rust/issues/93740).

---
layout: post
title: fmtArg
---

# fmtArg

```
Mara Bos and Chen Chen
Trustworthiness Software Engineering & Open Source Lab
Huawei Technologies, Inc.
```
A proposal to reduce binary size is to modify the way how `std::fmt::Arguments` is implemented, as described in the following [issue](https://github.com/rust-lang/rust/issues/99012). 

An important part of this design is that most of it can be stored in static storage, to minimize the amount of work that a function that needs to create/pass a fmt::Arguments needs to do. It can just refer to the static data, and only fill in a slice of the arguments.

Some downsides:

A fmt::Arguments is still relatively big (six pointers in size), and not a great type to pass by value. It could be just two pointers in size (one to static data, one to dynamic data), such that it fits in a register pair.
It costs quite a lot of static storage for some simple format strings. For example, "a{}b{}c" needs a &["a", "b", "c"], which is stored in memory as a (ptr, size) pair referencing three (ptr, size) pairs referencing one byte each, which is a lot of overhead. Small string literals with just a newline or a space are very common in formatting.
When even just a single formatting placeholder uses any non-standard options, such as "{:?}", a relatively large array with all the (mostly default) formatting options is stored for all placeholders.
The non-static part that contains the pointers to the arguments contains the pointers to the relevant Display/Debug/etc. implementation as well, even though that second part is constant and could be static. (It's a bit tricky to split those, though.)
Even when formatting a simple &str argument with a simple "{}" placeholder, the full Display implementation for &str is pulled in, which include code for all the unused options like padding, alignment, etc.
Issues like those are often reason to avoid formatting in some situations, which is a shame.

None of these things are trivial to fix, and all involve a trade off between compile time, code size, runtime performance, and implementation complexity. It's also very tricky to make these tradeoffs for many different use cases at once, as the ways in which formatting is used in a program differs vastly per type of Rust program.

## Updates

- 


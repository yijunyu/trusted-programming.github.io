# Keyword Generics 
```
Bastian Kauschke (lcnr)
Trusted Programming
Huawei Technologies, Inc. & LCNR
```

## Description

The Keyword Generics Initiative is a new initiative in Rust with the goal researching the ability to abstract over the [color of functions](https://journal.stuffwithstuff.com/2015/02/01/what-color-is-your-function/) or "effects". See [the official announcement post](https://blog.rust-lang.org/inside-rust/2022/07/27/keyword-generics.html) for more details.

It is currently not possible to nicely abstract over "`const`-ness" and "`async`-ness" in stable Rust. This is an issue as, for example, it would requires duplication between `async` and not-`async` functions with the same behavior which is [blocking work of the Async Working Group](https://doc.rust-lang.org/nightly/nightly-rustc/rustc_session/session/struct.Session.html#method.delay_span_bug).

We hope to avoid duplicating large parts of the standard libraries API for `async`, and then duplicating some functions again to also optionally make them `const`. That would result in 4 different versions of the same function. While not the main goal, this might even be extended to more parts of the language, like fallability. We currently often add both an infallible and a fallible variant of the same function, for example [`fn array::map`](https://doc.rust-lang.org/nightly/std/primitive.array.html#method.map) and (the not yet stable) [`fn array::try_map`](https://doc.rust-lang.org/nightly/std/primitive.array.html#method.try_map).

This initiative is currently still in the exploration phase: figuring out the requirements and scope, looking at prior art and experimenting with potential solutions. While this research might not result in any changes to the language, it is still valuable and necessary as it unblocks future decisions in the impacted areas.

The reason why its important is best explained by [this (and the following) section of the announcement post](https://blog.rust-lang.org/inside-rust/2022/07/27/keyword-generics.html#memories-of-the-present-async-today).


## Updates

[ ] Finding out the requirements and scope
[ ] Finding out prior art and experimenting with potential solutions


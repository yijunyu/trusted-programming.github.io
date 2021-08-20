---
layout: post
title: Contributions to the clippy crate by Huawei Trusted Programming 
toc: true
---

Here is the list of the opensource contributions made by huawei employees on the [clippy crate](https://github.com/rust-lang/rust-clippy).

### (clippy) Add lint to check for boolean comparison in assert macro calls

This [pull request](https://github.com/rust-lang/rust-clippy/pull/7083) add a new lint (called `bool_assert_comparison`) which check cases like these:

```rust
assert_eq!("a".is_empty(), false);
debug_assert_ne!("b".is_empty(), true);
```

Because they can be rewritten like this:

```rust
assert!(!"a".is_empty());
debug_assert!(!"b".is_empty());
```

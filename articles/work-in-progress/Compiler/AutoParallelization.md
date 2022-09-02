---
layout: post
title: Auto parallelization for Rust code
---

# Auto parallelize Rust code

```
Li Yuan, Chunmiao Li, and Yijun Yu
Trusted Programming
Trusted Software Engineering & Open Source Lab
Huawei Technologies
```

Sequential programs in Rust can be parallelized into parallel programs using Rayon or Scoped Thread features
by simply adding a feature for the code to compile. 

For example, this code
```rust
fn count_prime(a: i32, b: i32) -> i32 {
    // other statements
    let mid = (a + b) / 2;
    let lo = count_prime(a, mid);
    let hi = count_prime(mid, b);
    lo + hi
}
```
will have the same effect as the following code
```rust
extern crate rayon;
fn count_prime(a: i32, b: i32) -> i32 {
    // other statements
    let mid = (a + b) / 2;
    let (lo, hi) = rayon::join(|| count_prime(a, mid), || count_prime(mid, b));
    lo + hi
}
```

## Updates
- [x] Proof of concept implementation on an example sequential program. [commit here](https://github.com/rust-lang/rust/commit/a6eb7fcbd51e2ae7415c830e3d255aa9a6db7804)
- [ ] Implement automatic transformation from serial iterators to rayon's parallel iterators.
- [ ] Test on AICPU and Ylong_RUST projects.
- [ ] Submit a pre-pre-RFC on the official Rust forum.
- [ ] Automatic granularity control through profile analysis.

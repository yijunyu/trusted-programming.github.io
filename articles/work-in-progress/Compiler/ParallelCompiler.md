---
layout: post
title: Parallelization for Rust compiler
---

# Parallel Compiler

```
Li Yuan
Trusted Programming
Trusted Software Engineering & Open Source Lab
Huawei Technologies
```

Give the Rust compiler the ability to execute in parallel to improve compilation efficiency.

See [compiler-team-ambitions-2022](https://blog.rust-lang.org/inside-rust/2022/02/22/compiler-team-ambitions-2022.html#faster-builds-aspirations--%EF%B8%8F) here.

## Updates
Fix bugs and UI test case failures of parallel compiler. See [issues here](https://github.com/rust-lang/rust/labels/WG-compiler-parallel)
- [x] fix 20/21 test failures. ([PR1](https://github.com/rust-lang/rust/pull/97307) [PR2](https://github.com/rust-lang/rust/pull/98570) [PR3](https://github.com/rust-lang/rust/pull/99457))
- [x] fix the ICE from `WorkerLocal` when query cycle error.
- [ ] fix the test failure of `warn` from `tracing` crate.

Update Rustc-dev-guide. 
- [x] Update Parallel Compilation Capture. [PR](https://github.com/rust-lang/rustc-dev-guide/pull/1432)

Complete the implementation of the parallel-queries. See the tracking issue [here](https://github.com/rust-lang/rust/issues/48685).
- [x] get rid of `RefCell` in `TransitiveRelation`. [PR](https://github.com/rust-lang/rust/pull/99702)
- [x] Refactor `GlobalCtxt::layout_depth`. [PR](https://github.com/rust-lang/rust/pull/100748)
- [ ] fix `EvaluationCache` overwrites its entries. [reviewing](https://github.com/rust-lang/rust/pull/100987)
- [ ] make `mk_attr_id` part of `ParseSess`. [reviewing](https://github.com/rust-lang/rust/pull/101313)
- [ ] review usages of `Session.lint_store` and `Session.buffered_lints`
- [ ] review `GlobalCtxt.rcache`, `OnDiskCache.file_index_to_file` and `OnDiskCache.synthetic_expansion_infos`
- [ ] find a way to deal with marking attributes as used
- [ ] ensure Rayon executes all remaining work when we panic
- [ ] refactor error message hading

[ ] Solve the problem of parallel compilation efficiency and make parallel compilation the default option for the compiler

[ ] Become a member of the Parallel Compilation Working Group (And the avatar is displayed on the governance page of the Rust official website :P)

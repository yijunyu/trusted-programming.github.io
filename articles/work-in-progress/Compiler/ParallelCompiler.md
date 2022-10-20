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
Solve the efficiency problem of parallel compiler under single thread
- [ ] Find out the specific reason for the loss of efficiency after using Mutex instead of RefCell in `rustc_date_structure`. Refer to the perf test results [here](https://github.com/rust-lang/rust/pull/101566#issuecomment-1276331871).
- [ ] Reduce the number of calls such as `Lock::lock()`, `Lock::borrow()` in rustc's code. We should start with the query system

Make the parallel compiler more available
- [ ] Allows users to use parallel compilers with components provided by the Rust community. For example, let users switch to the parallel compiler through a rustup command

Fix bugs and UI test case failures of parallel compiler. See [issues here](https://github.com/rust-lang/rust/labels/WG-compiler-parallel)
- [x] fix 20/21 test failures. ([PR1](https://github.com/rust-lang/rust/pull/97307) [PR2](https://github.com/rust-lang/rust/pull/98570) [PR3](https://github.com/rust-lang/rust/pull/99457))
- [x] fix the ICE from `WorkerLocal` when query cycle error.
- [ ] fix the test failure of `warn` from `tracing` crate.

Update Rustc-dev-guide. 
- [x] Update Parallel Compilation Capture. [PR](https://github.com/rust-lang/rustc-dev-guide/pull/1432)

parallel-queries
- [ ] Complete the implementation of the parallel-queries. See the tracking issue [here](https://github.com/rust-lang/rust/issues/48685).

Working-group
- [ ] Contact interested members of the compiler team to reorganize the Parallel Compiler Working Group.

MCP
- [ ] Write the above tasks into a new MCP, submit and get accepted in the community.
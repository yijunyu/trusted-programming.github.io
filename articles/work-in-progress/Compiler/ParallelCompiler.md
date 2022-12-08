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
**completed** MCP to re-creating the parallel rustc working group
- [x] Complete the MCP draft
- [x] Send private messages to various community members to get as much support as possible
- [x] Submit the [MCP](https://github.com/rust-lang/compiler-team/issues/567)
- [x] Get Approved

Become the lead of the working group

- [ ] Refer to RFC to prepare materials of parallel rustc, focusing on the roadmap
- [ ] Submit to compiler team and language team for review
- [ ] Get Approved

Solve the efficiency problem of parallel compiler under single thread
- [ ] Find out the reason for the loss of efficiency after using Mutex instead of RefCell in `rustc_date_structure`. 
Refer to the perf test results [here](https://github.com/rust-lang/rust/pull/101566#issuecomment-1276331871).
- [ ] Minimize the impact of switching to parallel mode code in the nightly compiler on compilation efficiency

Rustc perf support
- [ ] Measuring compiler efficiency in a multithreaded environment
- [ ] Benchmark for parallel compiler

Test for parallel compiler
- [x] fix 20/21 UI test failures when -Zthread=1. ([PR1](https://github.com/rust-lang/rust/pull/97307) [PR2](https://github.com/rust-lang/rust/pull/98570) [PR3](https://github.com/rust-lang/rust/pull/99457))
- [x] fix the ICE from `WorkerLocal` when query cycle error.
- [ ] fix the test failure of `warn` from `tracing` crate.
- [ ] collect and fix bugs for `-Zthreads=n` when n > 1
- [ ] Diagnostics under parallel compilation enables deterministic sequential output


Other parts of the compilation process with potential for parallelization
- [ ] Expansion and import resolving
- [ ] Lex parsing

Update Rustc-dev-guide. 
- [x] Update Parallel Compilation Capture. [PR](https://github.com/rust-lang/rustc-dev-guide/pull/1432)



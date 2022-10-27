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
MCP to re-creating the parallel rustc working group
- [ ] Complete the MCP draft on [hackmd](https://hackmd.io/@TKyxIWXBRqyDPLDPcP0qfg/parallel_rustc_mcp)
- [ ] Send private messages to various community members to get as much support as possible
- [ ] Submit the MCP, discuss on Zulip
- [ ] Get Approve

Solve the efficiency problem of parallel compiler under single thread
- [x] Find out the reason for the loss of efficiency after using Mutex instead of RefCell in `rustc_date_structure`. 
Refer to the perf test results [here](https://github.com/rust-lang/rust/pull/101566#issuecomment-1276331871).
- [ ] Minimize the impact of switching to parallel mode code in the nightly compiler on compilation efficiency

Other parts of the compilation process with potential for parallelization
- [ ] Expansion and import resolving
- [ ] Monomorphization
- [ ] Rustdoc

Other supporting facilities
- [ ] Let users switch to the parallel compiler through a rustup command
- [ ] Perf tool and benchmark for parallel compiler

Fix bugs and UI test case failures of parallel compiler. See [issues here](https://github.com/rust-lang/rust/labels/WG-compiler-parallel)
- [x] fix 20/21 test failures. ([PR1](https://github.com/rust-lang/rust/pull/97307) [PR2](https://github.com/rust-lang/rust/pull/98570) [PR3](https://github.com/rust-lang/rust/pull/99457))
- [x] fix the ICE from `WorkerLocal` when query cycle error.
- [ ] fix the test failure of `warn` from `tracing` crate.

Update Rustc-dev-guide. 
- [x] Update Parallel Compilation Capture. [PR](https://github.com/rust-lang/rustc-dev-guide/pull/1432)



---
layout: post
title: Removing LLVM blockers for Rust compiler
---

# Removing LLVM blockers for Rust compiler

```
Amanieu d'Antras
Principal Rust Expert
Trustworthy Open-Source Software Engineering Lab &
Ireland Research Centre

Wei Wei 
Central Software Institute

Huawei Technology, Inc.
```
[High Priority bugs in LLVM for the Rust compiler](https://github.com/rust-lang/rust/issues?q=is%3Aopen+label%3AA-LLVM+is%3Aissue+label%3AP-high) indicates that we need to ask Huawei's help to resolve these problems. 

At the following [thread](https://zulip-archive.rust-lang.org/stream/187780-t-compiler/wg-llvm/topic/Huawei's.20LLVM.20team.html) a heated discussion has revealed 5-10 issues that need to be addressed. 

## List of features as candidates for Huawei's LLVM team

A lot of these have examples on godbolt. Add `--emit llvm-ir` to the flags to
show the LLVM IR that rustc is generating.

### Rust insufficiently optimizes loop { match { } } state machines

https://github.com/rust-lang/rust/issues/80630

### align_to prefix max length not taken into account in optimization

Unnecessary auto-vectorization ie emitted when the max length of a loop is always less than 16.

https://github.com/rust-lang/rust/issues/72356

### Comparison of Option<NonZeroU*> is not fully optimized

https://github.com/rust-lang/rust/issues/49892

### cmov conversion hurts binary search performance

https://github.com/rust-lang/rust/issues/53823

https://bugs.llvm.org/show_bug.cgi?id=40027

### && operator chains (and ||, possibly) generates unoptimizable LLVM IR

https://github.com/rust-lang/rust/issues/83623

https://bugs.llvm.org/show_bug.cgi?id=51211

### rust can't serialize 11 fields efficiently

https://rust.godbolt.org/z/hfG734fGf

https://github.com/rust-lang/rust/issues/45068

### Compiler generating extra memcpy, inconsistently depending on used types

https://github.com/rust-lang/rust/issues/85094

https://godbolt.org/z/d5PKx3b1d

### Different (suboptimal) assembly generated for match expr vs if-else ifs

https://github.com/rust-lang/rust/issues/100562

### Rust 1.56.0+ no longer recognizes boundary checks as avoiding division overflow panic

https://github.com/rust-lang/rust/issues/99960

https://godbolt.org/z/x95rGbW4j

### Suboptimal codegen for snippet with Armv7 target

https://github.com/rust-lang/rust/issues/98157

https://godbolt.org/z/ehxabaq38

## Resolved issues

### Inefficient compilation of ? operator

https://github.com/rust-lang/rust/issues/88616

This comment shows a simple example of this issue:

https://github.com/rust-lang/rust/issues/88616#issuecomment-913877197

### NonZero prevents values from being const-propagated properly

Specifically the example in this comment is not being optimized.

https://github.com/rust-lang/rust/issues/51346#issuecomment-394443610

See the godbolt examples here:

https://godbolt.org/z/fPjn9zxo6

### SimplifyCFG doesn't preserve information about exhaustive switch 

The example LLVM IR that fails to optimize is in this comment:

https://github.com/rust-lang/rust/issues/85133#issuecomment-904185574

## Updates

- [x] elicited 6 issues of LLVM to be addressed, all of them have examples with tasks on LLVM IR to be optimized properly
- [x] confirmed to commit on addressing these issues by Huawei's LLVM team
- [x] Two issues have been patched on LLVM
- [x] Evaluated on the Rust compiler, the [https://github.com/rust-lang/rust/pull/88759](pull request) has been merged into the Rust compiler, which will be available along with the next LLVM 15 release
- [ ] LLVM team is working on the remaining 3 patches which has been evaluating it for generalizability
- [ ] Long-term maintenance plan is being discussed with the LLVM team


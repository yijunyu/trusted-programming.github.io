---
layout: post
title: stdarch
---

# stdarch

```
Yuan Li, Shuo Chen, Amanieu d'Antras
Trustworthiness Software Engineering & Open Source Lab
Huawei Technologies, Inc.
```
A project group proposal for portable SIMD in std has [an open RFC](https://github.com/rust-lang/rust/issues/48556), 
see our [pull request](https://github.com/rust-lang/rust/pull/86546).

The library is ready as nightly in November and stabilized in end of December, 4400 instructions
have been done, rolling out in February major release.

## Updates
- [x] Completed most of the support work for the arm/aarch64 module. 
- [x] Updating code generation tools (a separate tool from the compiler).  These 80 instructions are blocked by issues in LLVM, which needs further discussion with the Rust Library team to address the remaining 80 instructions.
- [x] stablised for AARCH64 which will be in the main release around Feburary
- [x] Stabilize the ARM and ARMx64 intrinsics.
- [ ] Writing a RFC about F16 platform and unblock some features by making the type available to every platform as a new `struct` (a change to the compiler StdArch)

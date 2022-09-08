---
layout: post
title: Contributions to the stdarch crate by Huawei Trusted Programming 
toc: true
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

Here is the list of the opensource contributions made by huawei employees on the [stdarch crate](https://github.com/rust-lang/stdarch).

### (stdarch) add neon intrinsics support

Solved the ARM support issue of the SIMD acceleration library. You can see the list of the pull requests [here](https://github.com/rust-lang/stdarch/pulls?q=is%3Apr+is%3Amerged+neon+author%3ASparrowLii) and [here](https://github.com/rust-lang/stdarch/pulls?q=is%3Apr+is%3Amerged+neon+author%3ASureChen).

## Updates
- [x] Completed most of the support work for the arm/aarch64 module. 
- [x] Updating code generation tools (a separate tool from the compiler).  These 80 instructions are blocked by issues in LLVM, which needs further discussion with the Rust Library team to address the remaining 80 instructions.
- [x] stablised for AARCH64 which will be in the main release around Feburary
- [x] Stabilize the ARM and ARMx64 intrinsics.

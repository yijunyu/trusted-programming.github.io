---
layout: post
title: Contributions to the rustc_codegen_gcc project by Huawei Trusted Programming 
toc: true
---

Here is the list of the opensource contributions made by huawei employees on [rustc_codegen_gcc](https://github.com/rust-lang/rustc_codegen_gcc).

### Add more intrinsic translations

To generate GCC intrinsics, we use LLVM intrinsics as a base. (An [LLVM pull request](https://reviews.llvm.org/D127460) was also made for this.)

It was done in the following pull requests:

 * [#151](https://github.com/rust-lang/rustc_codegen_gcc/pull/151)
 * [#152](https://github.com/rust-lang/rustc_codegen_gcc/pull/152)
 * [#153](https://github.com/rust-lang/rustc_codegen_gcc/pull/153)
 * [#171](https://github.com/rust-lang/rustc_codegen_gcc/pull/171)
 * [#175](https://github.com/rust-lang/rustc_codegen_gcc/pull/175)
 * [#181](https://github.com/rust-lang/rustc_codegen_gcc/pull/181)
 * [#182](https://github.com/rust-lang/rustc_codegen_gcc/pull/182)
 * [#186](https://github.com/rust-lang/rustc_codegen_gcc/pull/186)
 * [#187](https://github.com/rust-lang/rustc_codegen_gcc/pull/187)

### Improve CI

The CI was taking a lot of time to run because all jobs were runnning all tests. Instead of doing this, we splitted into smaller jobs. The pull requests are:

 * [#188](https://github.com/rust-lang/rustc_codegen_gcc/pull/188)
 * [#193](https://github.com/rust-lang/rustc_codegen_gcc/pull/193)
 * [#195](https://github.com/rust-lang/rustc_codegen_gcc/pull/195)
 * [#196](https://github.com/rust-lang/rustc_codegen_gcc/pull/196)
 * [#200](https://github.com/rust-lang/rustc_codegen_gcc/pull/200)
 * [#201](https://github.com/rust-lang/rustc_codegen_gcc/pull/201)

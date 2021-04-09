---
layout: post
title: Recent Contributions to the Open Source Communities by Huawei Trusted Programming 
toc: true
---

* toc
{:toc}


Here is the list of opensource contributions made by huawei employees:

### (rustc/LLVM/libc) Add support for big-endian and ILP32 variants of AArch64

This added compilation support of Rust programs for big-endian and [ILP32](https://developer.arm.com/documentation/dai0490/latest/)
variants of AArch64.  These changes enable Huawei and other hardware companies to run Rust code on networking hardware which commonly
uses these architecture variants.

It was through pull requests to [the LLVM compiler](https://reviews.llvm.org/rG21bfd068b32ece1c6fbc912208e7cd1782a8c3fc),
[the libc crate](https://github.com/rust-lang/libc/pull/2039), and [the Rust compiler itself](https://github.com/rust-lang/rust/pull/81455).

These changes introduce new end-to-end cross-compilation targets for the Rust compiler, making it easier to build Rust products for bespoke
hardware using a single command:

```bash
cargo build --target aarch64_be-unknown-linux-gnu
cargo build --target aarch64-unknown-linux-gnu_ilp32
cargo build --target aarch64_be-unknown-linux-gnu_ilp32
```

### (rustdoc) Codeblock tooltip position

The goal of this PR was to fix the position of the tooltip "i" which appears when a rust documentation codeblock is marked as "ignore" or "compile_fail". You can see screenshots directly in the pull request [here](https://github.com/rust-lang/rust/pull/83393).

### (rustdoc) Add documentation for rustdoc GUI tests

There are multiple test suites to ensure that rustdoc is working as expected:
 * test/rustdoc: checks parts of the HTML and that some elements are present as expected
 * test/rustdoc-js: checks the documentation search
 * test/rustdoc-js-std: checks the documentation search (in the std specifically)
 * test/rustdoc-ui: checks the cli output (errors, warnings, etc)
 * test/rustdoc-json: checks the validity of the JSON output (you can generate either HTML or JSON)
 * test/rustdoc-gui: browse the generated HTML using a chrome instance (with the framework [browser-ui-test](https://github.com/GuillaumeGomez/browser-UI-test/))

This [PR](https://github.com/rust-lang/rust/pull/83420) is about adding documentation about the **rustdoc-gui** test suite.

### (rust) Fix error code checks

When the rust compiler generates an error, they have an associated code which then allows you to get more information by using `rustc --explain [ERROR_CODE]`. You can see the full list of the error codes [here](https://doc.rust-lang.org/nightly/error-index.html).

Just like a lot of things in the compiler, we need to ensure that the code doesn't become obsolete or out of date. It's very common for error codes to not be needed anymore and we need a check to be sure that they have been cleaned up correctly.

Because of some changes in the way the test suites are run, part of this check was not run because the target folder wasn't the right one. So the check was run, just not in the correct folder. With this [pull request](https://github.com/rust-lang/rust/pull/83451), it shouldn't happen again silently.

### (rust-GSL) Multiple fixes/improvements and upgrade crate version to 4.0

This crate provides bindings for the GSL (GNU Scientific library). With the new Rust release came new lints. This [pull request](https://github.com/GuillaumeGomez/rust-GSL/pull/97) fixed them and made some small improvements.

### (libc) Add new structures, constants and types around processor API for macOS

The [libc](https://github.com/rust-lang/libc/) project provides FFI (Foreign Function Interface) bindings to platforms' system libraries. It's one of the most used crate in the Rust ecosystem because as soon as you want to write low-level code, it's very likely that you'll need it.

This [pull request](https://github.com/rust-lang/libc/pull/2127) provided the following new items:
 * processor_cpu_load_info
 * processor_cpu_load_info_t
 * processor_cpu_load_info_data_t
 * processor_basic_info
 * processor_basic_info_t
 * processor_basic_info_data_t
 * processor_set_basic_info
 * processor_set_basic_info_t
 * processor_set_basic_info_data_t
 * processor_set_load_info
 * processor_set_load_info_t
 * processor_set_load_info_data_t
 * natural_t
 * mach_msg_type_number_t
 * PROCESSOR_BASIC_INFO
 * PROCESSOR_CPU_LOAD_INFO
 * PROCESSOR_PM_REGS_INFO
 * PROCESSOR_TEMPERATURE
 * PROCESSOR_SET_BASIC_INFO
 * PROCESSOR_SET_LOAD_INFO

And this [pull request](https://github.com/rust-lang/libc/pull/2129) added the following type aliases:
 * processor_flavor_t
 * processor_info_t
 * processor_info_array_t

### (sysinfo) Fix invalid CPU usage on new mac processors

The [sysinfo](https://github.com/GuillaumeGomez/sysinfo) crate provides information on your system, such as CPU, memory, disk and network usage. It also provides information on users and components whenever it's provided by the OS.

With the arrival of the new mac processors, the computation for the CPU usage on mac needed to be updated. Before, it was using `mach_absolute_time` to get how much time the processors "used" and then, by subtracting the previous time, you could know how much a process used of that time. Unfortunately, it seems that the time returned by this function is inaccurate with the new processors. So instead, we get the "raw" information from the processors (the "ticks") and we then convert it to time to be able to compute the processes usage.

You can see the pull request [here](https://github.com/GuillaumeGomez/sysinfo/pull/453).

### (rustdoc) Add a button to copy the "use statement"

It's very common, when reading an item's documentation to want to then import it into your code to use it. This [pull request](https://github.com/rust-lang/rust/pull/83721) adds a button to do it.

### (rustdoc) Merge idents in paths to make source code pages DOM smaller

This [pull request](https://github.com/rust-lang/rust/pull/83992) ensures to not have a span for each part of a path in the source code pages (for example [here](https://docs.rs/sysinfo/0.17.0/src/sysinfo/lib.rs.html#7-283)). Before this change, for `a::b::c` we generated `<span>a</span>::<span>b</span>::<span>c</span>`, now we generate `<span>a::b::c</span>`.

### (libc) Add new constant and functions for Android

This [pull request] added the following functions:

 * __system_property_set
 * __system_property_get

And the following constant:

 * PROP_VALUE_MAX

### (tempfile) Ensure that README code examples are tested

This [pull request](https://github.com/Stebalien/tempfile/pull/144) added the usage of [doc-comment](https://crates.io/crates/doc-comment) to ensure that the README code examples are tested (which prevents them to get outdated). You can see more explanations on how to easily test a markdown file code examples by reading this [blog post](https://blog.guillaume-gomez.fr/articles/2019-04-13+Keeping+Rust+projects%27+README.md+code+examples+up-to-date).

### (sysinfo) Add fallback when calculating OS version on linux

On linux, the version ID isn't always set (nor mandatory) in the `/etc/os-release` file. To fix this issue in case this information is missing, this [pull request](https://github.com/GuillaumeGomez/sysinfo/pull/457) go get it from `/etc/lsb-release`.

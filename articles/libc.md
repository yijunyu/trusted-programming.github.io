---
layout: post
title: Contributions to the libc crate by Huawei Trusted Programming 
toc: true
---

Here is the list of the opensource contributions made by huawei employees on the [libc crate](https://github.com/rust-lang/libc).


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

### (libc) Add new constant and functions for Android

This [pull request] added the following functions:

 * `__system_property_set`
 * `__system_property_get`

And the following constant:

 * PROP_VALUE_MAX

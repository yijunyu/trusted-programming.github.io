---
layout: post
title: Contributions to the libc crate by Huawei Trusted Programming 
toc: true
---

Here is the list of the opensource contributions made by huawei employees on the [libc crate](https://github.com/rust-lang/libc).

The [libc](https://github.com/rust-lang/libc/) project provides FFI (Foreign Function Interface) bindings to platforms' system libraries. It's one of the most used crate in the Rust ecosystem because as soon as you want to write low-level code, it's very likely that you'll need it.


### Add new structures, constants and types around processor API for macOS

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

### Add new constant and functions for Android

This [pull request](https://github.com/rust-lang/libc/pull/2142) added the following functions:

 * `__system_property_set`
 * `__system_property_get`

And the following constant:

 * PROP_VALUE_MAX

### Add more items for Apple

This [pull request](https://github.com/rust-lang/libc/pull/2401) added the following type aliases:

 * task_info_t
 * host_info_t
 * task_flavor_t
 * rusage_info_t
 * vm_offset_t
 * vm_size_t
 * vm_address_t
 * mach_task_basic_info_data_t
 * mach_task_basic_info_t
 * task_thread_times_info_data_t
 * task_thread_times_info_t

The following types:

 * task_thread_times_info
 * rusage_info_v0
 * rusage_info_v1
 * rusage_info_v2
 * rusage_info_v3
 * rusage_info_v4
 * mach_task_basic_info

The following constants:

 * TASK_THREAD_TIMES_INFO
 * HOST_CPU_LOAD_INFO_COUNT
 * MACH_TASK_BASIC_INFO
 * MACH_PORT_NULL
 * RUSAGE_INFO_V0
 * RUSAGE_INFO_V1
 * RUSAGE_INFO_V2
 * RUSAGE_INFO_V3
 * RUSAGE_INFO_V4
 * TASK_THREAD_TIMES_INFO_COUNT
 * MACH_TASK_BASIC_INFO_COUNT
 * HOST_VM_INFO64_COUNT
 * TASK_THREAD_TIMES_INFO_COUNT
 * MACH_TASK_BASIC_INFO_COUNT
 * HOST_VM_INFO64_COUNT

The following functions:

 * proc_pid_rusage
 * vm_deallocate
 * task_for_pid
 * task_info
 * host_statistics

And the following static:

 * vm_page_size

### Add more items for Apple

This [pull request](https://github.com/rust-lang/libc/pull/2332) added the following types:

 * vinfo_stat
 * vnode_info
 * vnode_info_path
 * proc_vnodepathinfo

And the following constants:

 * PROC_PIDTBSDINFO
 * PROC_PIDVNODEPATHINFO
 * PROC_PIDPATHINFO_MAXSIZE
 * MAXPATHLEN

### Add mach_task_self function

This [pull request](https://github.com/rust-lang/libc/pull/2368) added the `mach_task_self` function (which needed the `mach_task_self_` static to work).

### Add more types and functions for Apple

This [pull request](https://github.com/rust-lang/libc/pull/2369) added the following type aliases:

 * host_t
 * host_flavor_t
 * host_info64_t
 * vm_statistics_t
 * vm_statistics_data_t
 * vm_statistics64_t
 * vm_statistics64_data_t

The following types:

 * vm_statistics
 * if_data64
 * if_msghdr2
 * vm_statistics64

And the following functions:

 * host_statistics64
 * host_processor_info

### Add constants for Apple

This [pull request](https://github.com/rust-lang/libc/pull/2370) added the following constants:

 * HOST_LOAD_INFO
 * HOST_VM_INFO
 * HOST_CPU_LOAD_INFO
 * HOST_VM_INFO64
 * HOST_EXTMOD_INFO64
 * HOST_EXPIRED_TASK_INFO
 * VM_PAGE_QUERY_PAGE_PRESENT
 * VM_PAGE_QUERY_PAGE_FICTITIOUS
 * VM_PAGE_QUERY_PAGE_REF
 * VM_PAGE_QUERY_PAGE_DIRTY
 * VM_PAGE_QUERY_PAGE_PAGED_OUT
 * VM_PAGE_QUERY_PAGE_COPIED
 * VM_PAGE_QUERY_PAGE_SPECULATIVE
 * VM_PAGE_QUERY_PAGE_EXTERNAL
 * VM_PAGE_QUERY_PAGE_CS_VALIDATED
 * VM_PAGE_QUERY_PAGE_CS_TAINTED
 * VM_PAGE_QUERY_PAGE_CS_NX

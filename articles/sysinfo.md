---
layout: post
title: Contributions to the sysinfo crate by Huawei Trusted Programming 
toc: true
---

Here is the list of the opensource contributions made by huawei employees on the [sysinfo crate](https://github.com/GuillaumeGomez/sysinfo).

The [sysinfo](https://github.com/GuillaumeGomez/sysinfo) crate provides information on your system, such as CPU, memory, disk and network usage. It also provides information on users and components whenever it's provided by the OS.

### Fix invalid CPU usage on new mMac processors

With the arrival of the new mac processors, the computation for the CPU usage on mac needed to be updated. Before, it was using `mach_absolute_time` to get how much time the processors "used" and then, by subtracting the previous time, you could know how much a process used of that time. Unfortunately, it seems that the time returned by this function is inaccurate with the new processors. So instead, we get the "raw" information from the processors (the "ticks") and we then convert it to time to be able to compute the processes usage.

You can see the pull request [here](https://github.com/GuillaumeGomez/sysinfo/pull/453).

### Add fallback when calculating OS version on Linux

On Linux, the version ID isn't always set (nor mandatory) in the `/etc/os-release` file. To fix this issue in case this information is missing, this [pull request](https://github.com/GuillaumeGomez/sysinfo/pull/457) go get it from `/etc/lsb-release`.

### Fix CPU usage on Windows

This [pull request](https://github.com/GuillaumeGomez/sysinfo/pull/466) fixed the CPU usage on Windows by changing the way it is computed by using `GetSystemTimes` in addition to `GetProcessTimes`.

### Improve network code on Mac and Windows

This [pull request](https://github.com/GuillaumeGomez/sysinfo/pull/484) was mostly a clean up which also improved performance a little bit.

### Rework `Signal` enum and remove `#[repr(C)]` on it

This [pull request](https://github.com/GuillaumeGomez/sysinfo/pull/490) allows to prevent cast between the `Signal` enum and the C function. It prevents to generate invalid C values which might not exist (on Mac and Windows mostly). Instead, the `kill` method converts the enum "manually".

### Add SytemExt::IS_SUPPORTED

This [pull request](https://github.com/GuillaumeGomez/sysinfo/pull/494) added the `IS_SUPPORTED` constant to the `SystemExt` trait, allowing to check directly from the code if a target is supported.

### Add CHANGELOG

This [pull request](https://github.com/GuillaumeGomez/sysinfo/pull/507) added a CHANGELOG. It was something that a lot of people asked so it was finally added.

### Set executable path from command line if not found on Linux

This [pull request](https://github.com/GuillaumeGomez/sysinfo/pull/512) added a fallback to retrieve the executable path from the command line directly if the information isn't available otherwise.

### Add support for removable disk on Linux

This [pull request](https://github.com/GuillaumeGomez/sysinfo/pull/525) added a check to see if a device is removable or not on Linux.

### Fix CPU usage subtraction overflow on Linux

If a process was running for long enough, it was possible to get a subtraction overflow when computing the CPU usage. This [pull request](https://github.com/GuillaumeGomez/sysinfo/pull/532) fixed it.

### Add SWAP memory information on Windows

Before this [pull request](https://github.com/GuillaumeGomez/sysinfo/pull/535), this information was simply not available on Windows. It was followed by a fix for the SWAP memory computation in this [pull request](https://github.com/GuillaumeGomez/sysinfo/pull/540).

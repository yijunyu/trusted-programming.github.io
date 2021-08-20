---
layout: post
title: Contributions to the sysinfo crate by Huawei Trusted Programming 
toc: true
---

Here is the list of the opensource contributions made by huawei employees on the [sysinfo crate](https://github.com/GuillaumeGomez/sysinfo).

### (sysinfo) Fix invalid CPU usage on new mac processors

The [sysinfo](https://github.com/GuillaumeGomez/sysinfo) crate provides information on your system, such as CPU, memory, disk and network usage. It also provides information on users and components whenever it's provided by the OS.

With the arrival of the new mac processors, the computation for the CPU usage on mac needed to be updated. Before, it was using `mach_absolute_time` to get how much time the processors "used" and then, by subtracting the previous time, you could know how much a process used of that time. Unfortunately, it seems that the time returned by this function is inaccurate with the new processors. So instead, we get the "raw" information from the processors (the "ticks") and we then convert it to time to be able to compute the processes usage.

You can see the pull request [here](https://github.com/GuillaumeGomez/sysinfo/pull/453).

### (sysinfo) Add fallback when calculating OS version on linux

On linux, the version ID isn't always set (nor mandatory) in the `/etc/os-release` file. To fix this issue in case this information is missing, this [pull request](https://github.com/GuillaumeGomez/sysinfo/pull/457) go get it from `/etc/lsb-release`.

---
layout: post
title: Speed Up Compilation Time
---

# Speed up compilation time

```
Amanieu d'Antras, Yijun Yu
Trustworthy Open-Source Software Engineering Lab &
Ireland Research Centre
Huawei Technology, Inc.
```

**Aim**: gain performance improvement on benchmarks over the status of 2021-07-23. 

https://perf.rust-lang.org/compare.html?start=2021-07-23

## Improve the speed of compiling common (standard) libraries, such as the `syn` crate, by aborting if a `panic()` happens in a `drop()`. 

The performance gain has been achieved for crates such as `syn opt`, see the full report below:

https://perf.rust-lang.org/compare.html?start=c9db3e0fbc84d8409285698486375f080d361ef3&end=1f815a30705b7e96c149fc4fa88a98ca04e2deee 

## Updates

- [x] an estimate of 10% performance gain can be obtained for the benchmarks: the option is not on by default, but when the option is on it does improve the performance. 
- [x] A further update by Nov 24 by the language team to decide whether the feature will be made into a default. 
- [x] Merge in improvements has been confirmed.
- [x] Confirmed 10% of performance gain achieved. 
- [ ] Will be available in the next Rust compiler release.


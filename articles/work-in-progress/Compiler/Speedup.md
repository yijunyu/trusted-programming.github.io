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

## Updates

- [x] an estimate of 10% performance gain can be obtained for the benchmarks: the option is not on by default, but when the option is on it does improve the performance. 
- [x] A further update by Nov 24 by the language team to decide whether the feature will be made into a default. 
- [x] Merge in improvements has been confirmed.
- [ ] Evaluating performance improvement

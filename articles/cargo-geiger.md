---
layout: post
title: Contributions to the cargo-geiger crate by Huawei Trusted Programming 
toc: true
---

Here is the list of the opensource contributions made by huawei employees on the [cargo-geiger crate](https://github.com/rust-secure-code/cargo-geiger).

### (cargo-geiger) Generate reports of the safe code ratios in addition to the unsafe code counts

![Architecture](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/trusted-programming/trusted-programming.github.io/main/articles/cargo-geiger.md&idx=0)
```
@startuml
file code as "Rust \n source code"
file report as "Rust safe ratio \n report"
code -> [Cargo-Geiger]
[Cargo-Geiger] -> report
@enduml
```

When you run cargo-geiger, it will output the counts of unsafe code elements for functions, expressions, etc. We created [this pull request](https://github.com/rust-secure-code/cargo-geiger/pull/167) to report the safe code ratios.

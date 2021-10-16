---
layout: post
title: Contributions to the cargo-geiger crate by Huawei Trusted Programming 
toc: true
---

Here is the list of the opensource contributions made by huawei employees on the [cargo-geiger crate](https://github.com/rust-secure-code/cargo-geiger).

### (cargo-geiger) Generate reports of the safe code ratios in addition to the unsafe code counts

![Architecture]({{site.plantuml}}/articles/cargo-geiger.md&idx=0)
```
@startuml
file code as "Rust\nproject"
file report as "Report of safe ratios in Rust code"
component geiger as "cargo-geiger --output-format=Ratio"
code -> geiger
geiger -> report
@enduml
```

<img uml='
code -> [Cargo-Geiger]
'>

When you run cargo-geiger, it will output the counts of unsafe code elements for functions, expressions, etc. We created [this pull request](https://github.com/rust-secure-code/cargo-geiger/pull/167) to report the safe code ratios.

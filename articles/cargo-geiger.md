---
layout: post
title: Contributions to the cargo-geiger crate by Huawei Trusted Programming 
toc: true
---

Here is the list of the opensource contributions made by huawei employees on the [cargo-geiger crate](https://github.com/rust-secure-code/cargo-geiger).

### (cargo-geiger) Generate reports of the safe code ratios in addition to the unsafe code counts

![]({{site.plantuml}}{{page.url | replace:'.html','.md'}}&idx=0)<!--@startuml
file code as "Rust\nproject"
file report as "Report of \nunsafe counts"
file report2 as "Report of \nsafe ratios"
component geiger as "cargo-geiger"
component geiger2 as "cargo-geiger --output-format=Ratio"
code -> geiger
code -> geiger2
geiger -> report
geiger2 -> report2
@enduml-->

When you run cargo-geiger, it will output the counts of unsafe code elements for functions, expressions, etc. We created [this pull request](https://github.com/rust-secure-code/cargo-geiger/pull/167) to report the safe code ratios.

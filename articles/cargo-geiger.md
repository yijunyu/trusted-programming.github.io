---
layout: post
title: Contributions to the cargo-geiger crate by Huawei Trusted Programming 
toc: true
---

Here is the list of the opensource contributions made by huawei employees on the [cargo-geiger crate](https://github.com/rust-secure-code/cargo-geiger).

### (cargo-geiger) Generate reports of the safe code ratios in addition to the unsafe code counts

{% plantuml %}
[Rust source code] - [Cargo-Geiger] - [Rust safe ratio report]
{% endplantuml %}

When you run cargo-geiger, it will output the counts of unsafe code elements for functions, expressions, etc. We created [this pull request](https://github.com/rust-secure-code/cargo-geiger/pull/167) to report the safe code ratios.

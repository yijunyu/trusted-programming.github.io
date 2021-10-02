---
layout: post
title: Contributions to the GSL crate by Huawei Trusted Programming 
toc: true
---

Here is the list of the opensource contributions made by huawei employees on the [GSL crate](https://github.com/GuillaumeGomez/rust-GSL).

### Multiple fixes/improvements and upgrade crate version to 4.0

This crate provides bindings for the GSL (GNU Scientific library). With the new Rust release came new lints. This [pull request](https://github.com/GuillaumeGomez/rust-GSL/pull/97) fixed them and made some small improvements.

### Fix invalid callback storage

This [pull request](https://github.com/GuillaumeGomez/rust-GSL/pull/109) fixed the invalid storage of callback in the `Minimizer` type. Before that, it was pointing to a temporary closure which was dropped before being used.

### Fix invalid matrix methods

This [pull request](https://github.com/GuillaumeGomez/rust-GSL/pull/117) fixed some matrix types methods. It was using invalid type or calling the wrong C function (or both).

### Fix multiple issues and add more CI checks

This [pull request](https://github.com/GuillaumeGomez/rust-GSL/pull/118) did a lot of things:

 * Updated the remote repository used to generate the FFI bindings.
 * Greatly improved the FFI bindings generator.
 * Fixed some namings (by removing the `get_` prefix for example).
 * Added CI checks to ensure that:
   * The functions are calling the right C function.
   * The doc alias is the right one.
   * No doc alias was forgotten.
   * That the Rust function name is matching the C function's name.
 * Generated more FFI items.

All in all, it was a massive pull request which brought a lot of improvements.

### Added headers check in CI

This [pull request](https://github.com/GuillaumeGomez/rust-GSL/pull/121) added a CI check that all files had the correct header.

### Extend checks to methods

This [pull request](https://github.com/GuillaumeGomez/rust-GSL/pull/123) extended the checks initiated [here](https://github.com/GuillaumeGomez/rust-GSL/pull/118) by checking the methods as well.

### Extend checks to traits

This [pull request](https://github.com/GuillaumeGomez/rust-GSL/pull/124) is the final piece of work initiated in [here](https://github.com/GuillaumeGomez/rust-GSL/pull/118). It extended the checks to traits as well.

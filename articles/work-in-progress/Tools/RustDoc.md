---
layout: post
title: Rustdoc improvements
---

# Rustdoc improvement

```
Guillaume Gomez
Trustworthy Open-Source Software Engineering Lab &
Ireland Research Centre
Huawei Technology, Inc.
```

### Add "copy to clipboard" and "show hidden lines" for codeblocks

This [pull request](https://github.com/rust-lang/rust/pull/86892) adds both features in the title. It's common to copy code from the code block examples and also common to want to see the "full" code (including the eventual wrappers and so on).

### Improve search

This [pull request](https://github.com/rust-lang/rust/pull/90630) does two things:
 * Write a parser for the rustdoc search.
 * Extend the rustdoc search capabilities.


- [x] Code navigation
- [x] Improve Rustdoc UI: there are four ways to enhance UI, needs to decide which one is the best
- [ ] Implementations need to be done.
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

### Add "show hidden lines" for codeblocks

This [pull request](https://github.com/rust-lang/rust/pull/86892) adds both features in the title. It's common to copy code from the code block examples and also common to want to see the "full" code (including the eventual wrappers and so on).

### Implement TyKind::TyAlias in compiler

It would allow to finally fix the display of type aliases of dependencies.

### Finish Rustdoc UI rework

 * [ ] Improve settings menu display to look like Firefox Pocket
 * [ ] Add search "helpers" to help users enter rustdoc search

### Continue rustdoc search improvements

 * [ ] Support for `-> *` queries

### Stabilize "jump to definition"

 * [ ] Open RFC (in progress)
 * [ ] Implement RFC

---
layout: post
title: Docs.rs improvements
---

# Docs.rs improvement

```
Guillaume Gomez
Trustworthy Open-Source Software Engineering Lab &
Ireland Research Centre
Huawei Technology, Inc.
```

### Fix UI

There are two pull requests in progress for that:

 * <https://github.com/rust-lang/docs.rs/pull/1720>
 * <https://github.com/rust-lang/docs.rs/pull/1719>

### Add GUI test suite to prevent regression

This is a common issue on docs.rs: the website UI is breaking because of rustdoc changes. However, we only hear about these breakages when people open issues. So instead, we want to add a GUI testsuite so it can be detected automatically and fixed as quickly as possible.

The pull request starting this is [here](https://github.com/rust-lang/docs.rs/pull/1698).

---
layout: post
title: Rustup CI improvement
---

# (rustup) Add freebsd CI check

```
Guillaume Gomez
Trustworthy Open-Source Software Engineering Lab &
Ireland Research Centre
Huawei Technology, Inc.
```

rustup recently got some issues on freebsd, adding this [CI check](https://github.com/rust-lang/rustup/pull/2783) will allow to prevent issues to be released unnoticed.

## Updates

 - [x] Have all libc pull requests merged
 - [x] Publish new sysinfo version
 - [x] Update rustup dependencies to use sysinfo
 - [x] Update rustup dependencies versions
 - [ ] Add freebsd CI on rustup ([pull request](https://github.com/rust-lang/rustup/pull/2955))

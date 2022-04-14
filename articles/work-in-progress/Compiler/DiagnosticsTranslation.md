---
layout: post
title: Diagnostic Translation
---

# Diagnostic Translation

```
David Wood
Edinburgh Research Centre, UK
Huawei Technology, Inc.
```

# Diagnostic Translation

[Diagnostic translation](https://github.com/rust-lang/rust/pull/95512) enables rustc to emit error messages in the language of
a user's choice, increasing Rust's accessibility to non-native speakers of
English. Diagnostic translation is optional and will only be enabled if
explicitly requested by the user.

The core infrastructure for diagnostic translation is currently being
implemented (so that the compiler can replace error messages with a
translation). After this is completed, all of the compiler's diagnostics will
need to be modified so that they can be translated, and then translation teams
will need to work to translate the actual diagnostic messages.

## Updates

- [x] Initial PR has been accepted, using Fluent
- [x] Addressing [errors: lazily load fallback fluent bundle](https://github.com/rust-lang/rust/pull/95968)
- [ ] update of Rust language diagnostics
- [ ] update of Rust infrastructure

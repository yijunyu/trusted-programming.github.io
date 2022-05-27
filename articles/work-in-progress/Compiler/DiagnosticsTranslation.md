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

Diagnostic translation enables rustc to emit error messages in the language of
a user's choice, increasing Rust's accessibility to non-native speakers of
English. Diagnostic translation is optional and will only be enabled if
explicitly requested by the user.

The core infrastructure for diagnostic translation is already implemented in
rustc ([#95512], [#95716], [#95968]), enabling diagnostics to be translatable.

However, every diagnostic in rustc has to be ported to use the new
infrastructure before its diagnostic message can be translated. To facilitate
this transition (and to align with other efforts from the diagnostics working
group), various additional infrastructure is being implemented to simplify the
work of porting diagnostics for compiler contributors, such as: diagnostic and
subdiagnostic derives ([#95512], [#96468], [#96760], [#96853]) and compile-time
validation of translation resources and generation of typed identifiers for
translation messages ([#97327], [#97357]). Transition to translatable
diagnostic infrastructure is ongoing.

Once all diagnostics have been ported to the new infrastructure, translation
teams will be able to translate the diagnostic messages into different
languages.

## Updates
- [x] Implement core infrastructure enabling translation and update diagnostic
      derive ([#95512])
- [x] Improve loading of translation resources from sysroot ([#95716])
- [x] Improve performance of loading default translation resources ([#95968])
- [x] Update developer documentation for translation infrastructure/diagnostic
      derive ([rustc-dev-guide#1333])
- [x] Minor improvements to existing translatable diagnostics ([#96269])
- [x] Implement subdiagnostic derive to make porting some diagnostics easier
      ([#96468])
- [x] Port some diagnostics and add `Vec` field support to diagnostic derives
      ([#96760])
- [x] Port some more diagnostics and add `()` field support to diagnostic
      derives ([#96853])
- [x] Add compile-time validation of translation resources and typed
      identifiers for translated messages ([#97327])
- [x] Simplify referring to subdiagnostic messages with typed identifiers
      ([#97357])
- [ ] Finish porting diagnostics to translatable infrastructure
- [ ] Translate all diagnostic messages to desired languages
- [ ] Build infrastructure to ship rustc language packs via rustup (specific
      details yet undecided)

[#95512]: https://github.com/rust-lang/rust/pull/95512
[#95716]: https://github.com/rust-lang/rust/pull/95716
[#95968]: https://github.com/rust-lang/rust/pull/95968
[#96269]: https://github.com/rust-lang/rust/pull/96269
[#96468]: https://github.com/rust-lang/rust/pull/96468
[#96760]: https://github.com/rust-lang/rust/pull/96760
[#96853]: https://github.com/rust-lang/rust/pull/96853
[#97327]: https://github.com/rust-lang/rust/pull/97327
[#97357]: https://github.com/rust-lang/rust/pull/97357
[rustc-dev-guide#1333]: https://github.com/rust-lang/rustc-dev-guide/pull/1333

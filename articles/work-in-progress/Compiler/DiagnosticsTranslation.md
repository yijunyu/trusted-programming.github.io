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
rustc, enabling diagnostics to be translatable.

However, every diagnostic in rustc has to be ported to use the new
infrastructure before its diagnostic message can be translated. To facilitate
this transition (and to align with other efforts from the diagnostics working
group), various additional infrastructure is being implemented to simplify the
work of porting diagnostics for compiler contributors, such as: diagnostic and
subdiagnostic derives; migration lints; and compile-time validation of
translation resources and generation of typed identifiers for translation
messages.

Transition to translatable diagnostic infrastructure is ongoing. An effort has
[been started][blog_post] which has attracted many new contributors and a
significant number of pull requests ([full list][prs]).

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
- [x] Update developer documentation again for the typed identifiers and
      subdiagnostic derive ([rustc-dev-guide#1363])
- [x] Add compiler-internal lints to ensure that migrated modules/crates don't
      regress and to help in making sure modules/crates are entirely migrated
      ([#97948]).
- [x] Port `rustc_privacy` crate's diagnostics and fix a bug in the lints
      ([#98420]).
- [x] Update diagnostic and subdiagnostic derive to use the typed identifiers -
      enabling use of the derives to benefit from compile-time validation of
      Fluent messages ([#98428]).
- [x] Wrote documentation for new contributors to get involved in the
      diagnostic translation effort ([link][intro_doc]).
- [x] Started collecting list of all contributions to the diagnostic
      translation effort ([link][contributions_doc]).
- [x] Update dev guide to refer to diagnostic structs with typed identifiers
      ([rustc-dev-guide#1377]).
- [x] Port most of `rustc_lint` ([#98624])
- [x] Implement `LintDiagnostic` derive which shares infrastructure with
      existing derive diagnostics and allows lints to be represented as
      diagnostic structs ([#98884])
- [x] Migrate `rustc_passes::check_attr` diagnostics ([#99213] and [#99712]);
      add `MultiSpan` support to diagnostic derives; support warning
      subdiagnostics in the diagnostic derive; and trigger internal lints on
      lint construction ([#99213])
- [x] Publish blog post ([link][blog_post])
- [x] Don't fail on broken primary translations ([#100366])
- [x] Avoid linting diagnostic functions with diagnostic lints ([#101230])
- [x] Migrate `rustc_incremental` ([#100754])
- [x] Extend diagnostic derive with support for enums ([#102189])
- [x] Remove unnecessary `#[allow]`s of diagnostic migration lints ([#102356])
- [x] Rename `typeck.ftl` to `hir_analyis.ftl` ([#102395])
- [x] Implement eager translation ([#102623])
- [ ] Experiment with distributing Fluent resources across crates ([#103042])
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
[#97948]: https://github.com/rust-lang/rust/pull/97948
[#98420]: https://github.com/rust-lang/rust/pull/98420
[#98428]: https://github.com/rust-lang/rust/pull/98428
[#98624]: https://github.com/rust-lang/rust/pull/98624
[#98884]: https://github.com/rust-lang/rust/pull/98884
[#99213]: https://github.com/rust-lang/rust/pull/99213
[#99712]: https://github.com/rust-lang/rust/pull/99712
[#100366]: https://github.com/rust-lang/rust/pull/100366
[#101230]: https://github.com/rust-lang/rust/pull/101230
[#100754]: https://github.com/rust-lang/rust/pull/100754
[#102189]: https://github.com/rust-lang/rust/pull/102189
[#102356]: https://github.com/rust-lang/rust/pull/102356
[#102395]: https://github.com/rust-lang/rust/pull/102395
[#102623]: https://github.com/rust-lang/rust/pull/102623
[#103042]: https://github.com/rust-lang/rust/pull/103042
[rustc-dev-guide#1333]: https://github.com/rust-lang/rustc-dev-guide/pull/1333
[rustc-dev-guide#1363]: https://github.com/rust-lang/rustc-dev-guide/pull/1363
[rustc-dev-guide#1377]: https://github.com/rust-lang/rustc-dev-guide/pull/1377
[intro_doc]: https://hackmd.io/@davidtwco/Bk0wTF2u5
[contributions_doc]: https://hackmd.io/@davidtwco/rkXSbLg95
[blog_post]: https://blog.rust-lang.org/inside-rust/2022/08/16/diagnostic-effort.html
[prs]: https://github.com/rust-lang/rust/pulls?q=is%3Apr+sort%3Aupdated-desc+label%3AA-translation+-label%3Arollup

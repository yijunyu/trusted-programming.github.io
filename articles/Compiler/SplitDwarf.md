---
layout: post
title: Split DWARF
---

# Split DWARF
```
David Wood
Edinburgh Research Centre, UK
Huawei Technology, Inc.
```

Split DWARF is a feature being added to rustc which enables debugging
information to be split at compile time on Unix platforms, improving link times
and reducing total object size.

## Rationale
Rust's "State of Rust" yearly survey has consistently found that improved build
times is one of the most frequently requested improvements from the Rust
community. This is consistent with the experiences of teams within Huawei that
use Rust.

Large applications built with debug information have slow linking times, can
experience out-of-memory failures at link time and slow debugger start-up
times. Furthermore, debuginfo in these applications may result in a significant
increase in storage requirements and additional network traffic in distributed
build environments.

## Detailed Explanation
rustc already has support for split debuginfo on Windows (`*.pdb`) and macOS
(`*.dSYM`), but is missing support for split debuginfo on Linux (Split DWARF's
`*.dwp` files).

rustc's existing support (as of rustc stable 1.56.1, released Nov 1st 2021) for
split debuginfo is platform-dependent and exposed through the
`-Csplit-debuginfo` compiler flag:

- `-Csplit-debuginfo=off`
  - Split debuginfo is not desired, debuginfo should be in the final artifact.
  - **Windows:** `-Csplit-debuginfo=off` is not supported. Debuginfo is always
    separate on Windows.
  - **macOS:** `-Csplit-debuginfo=off` is supported, `dsymutil` is not
    executed.
  - **Linux:** `-Csplit-debuginfo=off` is the default. Split DWARF (this
    document) support is not stable.
- `-Csplit-debuginfo=unpacked`
  - Split debuginfo is in many separate files, spread throughout the build
    directory. `unpacked` split debuginfo might be contained within object
    files or in separate files, depending on the platform.
  - **Windows:** `-Csplit-debuginfo=unpacked` is not supported. Debuginfo is
    always packed on Windows.
  - **macOS:** `-Csplit-debuginfo=unpacked` is supported, `dsymutil` is not
    exectued.
  - **Linux:** `-Csplit-debuginfo=unpacked` is not supported. Split DWARF (this
    document) support is not stable.
- `-Csplit-debuginfo=packed`
  - Split debuginfo is desired in a single location separate from the
    executable.
  - **Windows:** `-Csplit-debuginfo=packed` is the default, debuginfo packed
    into a `.pdb` file.
  - **macOS:** `-Csplit-debuginfo=packed` is the  default, debuginfo packed
    into a `.dSYM` file.
  - **Linux:** `-Csplit-debuginfo=packed` is not supported. Split DWARF (this
    document) support is not stable.

Split DWARF is a new addition to the DWARF specification, starting in version 5
(released February 2017). Prior versions of DWARF supported Split DWARF through
extensions to the specification by the GNU project ("Debug Fission" project).

With Split DWARF, debuginfo which does not require link-time relocation is
split and is not processed by the linker, resulting in time/memory link-time
savings and smaller output.

Split DWARF adds support for `-Csplit-debuginfo` on Linux platforms, and adds
the `-Zsplit-dwarf-kind` flag (`-Csplit-dwarf-kind` once stabilized):

- `-Cdebuginfo=0 -Csplit-debuginfo=off`
  - No debug information.
- `-Cdebuginfo=2 -Csplit-debuginfo=off`
  - Debug information in relocatable object files (`.o`), linked into the final
    executable.
- `-Cdebuginfo=2 -Csplit-debuginfo=unpacked -Zsplit-dwarf-kind=single`
  - Debug information in relocatable object files (`.o`), ignored by the
    linker, not in the final executable.
- `-Cdebuginfo=2 -Csplit-debuginfo=packed -Zsplit-dwarf-kind=single`
  - Debug information in relocatable object files (`.o`), ignored by the
    linker, not in the final executable. Packaged from relocatable object files
    (`.o`)  into dwarf package (`.dwp`).
- `-Cdebuginfo=2 -Csplit-debuginfo=unpacked` (uses the default of
  `-Zsplit-dwarf-kind=split`)
  - Debug information in dwarf object files (`.dwo`), not in the final
    executable.
- `-Cdebuginfo=2 -Csplit-debuginfo=packed` (uses the default of
  `-Zsplit-dwarf-kind=split`)
  - Debug information in dwarf object files (`.dwo`), not in the final
    executable.
  - Packaged from dwarf object files (`.dwo`) into dwarf package (`.dwp`).

## Status
Split DWARF support is fully implemented in rustc and available for testing in
nightly. Split DWARF should be particularly beneficial for incremental debug
builds, resulting in compilation time improvements and reduced output artefact size.

Initial benchmarking ([#96199]) suggests a up-to 27% improvement in incremental
debug builds and 30% artefact size reduction are possible when using Split DWARF.

Split DWARF can be used on a nightly compiler by passing the
`-Zunstable-options -Csplit-debuginfo=unpacked` flags (i.e. using the
`RUSTFLAGS` environment variable). If packed debuginfo is required, then
`-Csplit-debuginfo=packed` can be used, this will produce a `.dwp` output file
but will lessen the compilation time improvements.

## Updates
- [x] Initial implementation of Split DWARF ([#77117])
- [x] Add `llvm-dwp` to Rust CI (#[80087])
- [x] Implement [`thorin`], a Split DWARF packaging utility
    - `thorin` was written specifically to integrate with the Rust compiler, it
      is the only Rust implementation of a Split DWARF packaging utility and
      supports both pre-standard GNU-flavour Split DWARF and DWARF 5-flavoured
      Split DWARF. `thorin` supports reading `rlib` files as input, which is
      required for supporting Split DWARF over multiple crates.
- [x] Support Split DWARF for crate dependencies ([#89819])
- [x] Add `split-debuginfo` config option to rustc's bootstrap ([#95612])
- [x] Fix `split-debuginfo` config flag on BSD platforms ([#96758])
- [x] Cache DWARF objects in work products ([#98901])
- [ ] Stabilize Split DWARF ([#98051])

[#77117]: https://github.com/rust-lang/rust/pull/77117
[#80087]: https://github.com/rust-lang/rust/pull/80087
[#89819]: https://github.com/rust-lang/rust/pull/89819
[#96199]: https://github.com/rust-lang/rust/pull/96199
[#95612]: https://github.com/rust-lang/rust/pull/95612
[#96758]: https://github.com/rust-lang/rust/pull/96758
[#98051]: https://github.com/rust-lang/rust/pull/98051
[#98901]: https://github.com/rust-lang/rust/pull/98901
[`thorin`]: https://github.com/rust-lang/thorin

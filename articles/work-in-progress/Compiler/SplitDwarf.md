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

**Goal**: Add split DWARF to rustc's split-debuginfo support

A detailed description of this feature can be found here: https://github.com/rust-lang/rust/issues/34651

**Benefits: How to use split debuginfo (to improve linking time and reduce binary size by up to 30%):**
If your project has multiple crates then you need a build of rustc that includes #89819 (not merged yet, will need to be built manually), if it is only one crate with no dependencies, then nightly can be used. With either of those versions, you can set `RUSTFLAGS="-Csplit-debuginfo=unpacked -Zunstable-options` to enable the split debuginfo. It's still a nightly feature, there might be bugs, if there are any, do let me know. 

The following [comment](https://github.com/rust-lang/rust/pull/89819#issuecomment-941152678) describes the split debuginfo and split dwarf options available in #89819. My work only affects `-Csplit-debuginfo` on Linux, it's already stable for Windows and macOS.

## Update:

- [x] Submitted [rust-lang/rust#89819] in an attempt to support cross-crate Split DWARF, which is complicated by the need to keep (dwarf-)objects around from dependencies for packaging into a DWARF object. 
  - Re-introduces a flag for changing between "single" and "split" variants of Split DWARF, which had been bundled into the `-Csplit-debuginfo={packed,unpacked}` options but make more sense separated. 
  - Also updates the logic for saving temporaries so that we keep the (dwarf-)object files around that we need for cross-crate Split DWARF.
  - Has been reviewed but the approach might need changed as Cargo needs to be able to know which temporaries to delete and this patch makes that more challenging. Alternative approaches include adding relevant temporaries to the rlib, but this is more complicated and contrived as the files would need to be written back to the filesystem where they were originally from the rlib to be packaged.
- [x] Work on a Rust implementation of a DWARF packaging tool is in-progress, nearing completion. Will enable easier integration with rustc as it can load dwarf objects from dependency rlibs.
- [ ] Hopefully a PR for stabilization can be put up in a few weeks once it's been used on nightly for a little bit (I'll probably add a bootstrap option so that this can be used on rustc itself which would be a good test case). 

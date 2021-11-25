---
layout: post
title: Name Mangling
---

# V0 demangling

This feature hasn't been stabilized:

rustc itself is now being built using the v0 mangling scheme (rust-lang/rust#90054).
The compiler flag for changing between symbol mangling schemes is being stabilized (`-Z symbol-mangling-scheme` to `-C symbol-mangling-scheme`) in rust-lang/rust#90128 (ongoing FCP, but likely to land).
After that is stabilized, you still wouldn't be able to use the v0 mangling scheme on stable, that's being discussed in rust-lang/rust#89917.

## Update

- [x] A pull request has been made to make it stable


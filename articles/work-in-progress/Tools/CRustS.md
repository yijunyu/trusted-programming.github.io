---
layout: post
title: CRustS
---

# A transpiler from Unsafe C to Safer Rust

```
Michael Ling, Yijun Yu, Haitao Wu, Yuan Wang
Trustworthiness Software Engineering & Open Source Lab
Huawei Technologies, Inc.
```

[CRustS Tool Demo](http://185.190.206.130)

As a safer alternative to C, Rust is a language for programming system software with a type-safe compiler to check its memory
and concurrency safety. To facilitate a smooth transition from C to Rust in an existing project, and lay a solid foundation for an
initial Rust re-implementation of existing functionalities in C, it would be helpful to have a source-to-source transpiler that can
transform programs from C to Rust using program transformation technologies. However, existing C-to-Rust transformation tool
sets have the drawback that they largely preserve the unsafe semantics of C, while rewriting them in Rust syntax. As such, the
safety of the resulting Rust programs still depends primarily on the programmers, rather than on the Rust compiler. To gain more
safety guarantees, in this demo, we present CRustS a systematic source-to-source transformation approach to increase the ratio of
the code passing the safety checks of Rust compiler by relaxing the semantics-preserving constraints of the transformation. Our
method uses 220 TXL [3] source-to-source transformation rules, of which 198 are strictly semantics-preserving and 22 are semantics
approximating, thus reducing the scope of unsafe expressions and exposing more opportunities for safe refactoring. Our method has
been evaluated on both open-source and commercial projects. Our solution demonstrates significantly higher safe code ratios after the
transformations, with function-level safe code ratios comparable to the average level of idiomatic Rust projects.

## References
- Michael Ling, Yijun Yu, Haitao Wu, Yuan Wang. "In Rust We Trust: A transpiler from Unsafe C to Safer Rust", In: ICSE 2022. paper accepted.

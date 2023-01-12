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

[CRustS Repo](https://github.com/trusted-programming/crusts)

[CRustS Tool Demo](http://185.190.206.130)

As a safer alternative to C, Rust is a language for programming system software
with a type-safe compiler to check its memory and concurrency safety. To
facilitate a smooth transition from C to Rust in an existing project, and lay a
solid foundation for an initial Rust re-implementation of existing
functionalities in C, it would be helpful to have a source-to-source transpiler
that can transform programs from C to Rust using program transformation
technologies. However, existing C-to-Rust transformation tool sets have the
drawback that they largely preserve the unsafe semantics of C, while rewriting
them in Rust syntax. As such, the safety of the resulting Rust programs still
depends primarily on the programmers, rather than on the Rust compiler. To gain
more safety guarantees, in this demo, we present CRustS a systematic
source-to-source transformation approach to increase the ratio of the code
passing the safety checks of Rust compiler by relaxing the semantics-preserving
constraints of the transformation. Our method uses 220 TXL [3] source-to-source
transformation rules, of which 198 are strictly semantics-preserving and 22 are
semantics approximating, thus reducing the scope of unsafe expressions and
exposing more opportunities for safe refactoring. Our method has been evaluated
on both open-source and commercial projects. Our solution demonstrates
significantly higher safe code ratios after the transformations, with
function-level safe code ratios comparable to the average level of idiomatic
Rust projects.

The code repository can be found at https://github.com/yijun/crusts. 

# Evaluation

Compared to the Laertes [OOPSLA'21], with respect to their own benchmarks, the safe ratio
obtained by CRustS is much higher.

##  Laertes

Laertes code and datasets can be downloaded from [here](https://zenodo.org/record/5442253#.YkDbGufMKUk).
It is a docker image which can be imported to extract the underlying code and artefacts.

Before running the tool, one needs to install the nightly 2021-10-15 edition of the Rust compiler, .

```bash
rustup toolchain nightly-2020-10-15
```
Then build the utilities `unsafe-counter`, `resolve-imports`, and `resolve-lifetimes`.

To run the scripts, one needs to have the dynamic libraries available on the load path:
```bash
export LD_LIBRARY_PATH=$HOME/.rustup/toolchains/nightly-2020-10-15-x86_64-unknown-linux-gnu/lib/
./run-all-experiments.sh
```

## Measurements

We wrote a simple `tree-grepper` query to compute the unsafe function ratios from the resulting code.
```bash
./ratio.sh
```

The corresponding queries for unsafe blocks, unsafe functions are respectively:
```
((unsafe_block) @b) 
((function_item (function_modifiers) @m)@f (#match? @m "unsafe"))
```

The corresponding query outputs all the functions.
```
(function_item) @f
```

The unsafe function ratio is thus measured by (1) the number of functions, and (2) the lines of code (LOC) of corresponding functions.

## Results comparison

Initially there are 373 Rust files transpiled from C programs from C2Rust. Amongst them, 98.8% of the functions are marked as `unsafe`, and 99.8% of the lines are enclosed by either an unsafe function or
an unsafe block inside a safe function.

After the translation by the approach of Emre et al.'s approach [OOPSLA21], `laertes` reduces the unsafe function ratio to 81.4% while creating slightly more functions than the original programs. However, most of these converted functions are rather short, resulting in an unsafe LOC ratio as high as 97.9%.

After the application of Ling et al.'s approach [ICSE22], `crusts` reduces the unsafe function ratio to 1.2%, while increasing the unsafe blocks. 
Furthermore, it reduces the length of generate lines from the original C2Rust too. 

|   Method   | # Unsafe Fn |  # Fn | Unsafe Fn Ratio | Unsafe Blk (LOC) | Unsafe Fn (LOC) | Fn (LOC) | Unsafe LOC Ratio | Unsafe Blk LOC Ratio |
| ---------- | ----------: | ----: | --------------: | ---------------: | --------------: | -------: | ---------------: | -------------------: |
| C2Rust.com |       10432 | 10550 |           98.8% |            39407 |          526948 |   527899 |            99.8% |                 7.4% |
| + Laertes  |       10120 | 12432 |           81.4% |            39407 |          524389 |   535221 |            97.9% |                 7.3% |
| + CRustS   |         161 | 12447 |            1.2% |           321004 |            7011 |   391991 |             1.7% |                81.8% |

Alternatively, we may apply CRustS first, then apply Laertes. The following table shows the results.

|   Method   | # Unsafe Fn |  # Fn | Unsafe Fn Ratio | Unsafe Blk (LOC) | Unsafe Fn (LOC) | Fn (LOC) | Unsafe LOC Ratio | Unsafe Blk LOC Ratio |
| ---------- | ----------: | ----: | --------------: | ---------------: | --------------: | -------: | ---------------: | -------------------: |
| C2Rust.com |       10432 | 10550 |           98.8% |            39407 |          526948 |   527899 |            99.8% |                 7.4% |
| + CRustS   |         161 | 10565 |            1.5% |           317253 |            7011 |   381008 |             1.8% |                83.2% |
| + Laertes  |         161 | 11444 |            1.4% |           317253 |            7011 |   383952 |             1.8% |                82.6% |

As one can see, `CRustS` alone could reduce the unsafe functions to the minimal even without applying `laertes`. There is no obvious advantage of applying `laertes` before or after `crusts`.


## References
- Michael Ling, Yijun Yu, Haitao Wu, Yuan Wang, James Cordy, Ahmed Hassan. "In Rust We Trust: A transpiler from Unsafe C to Safer Rust", In: ICSE 2022. paper accepted.
- Mehmet Emre, Ryan Schroeder, Kyle Dewey, and Ben Hardekopf. 2021. Translating C to safer Rust. Proc. ACM Program. Lang. 5, OOPSLA, Article 121 (October 2021), 29 pages.

## Updates
- [x] Compared to Laertes [OOPSLA'21] with respect to their own benchmarks


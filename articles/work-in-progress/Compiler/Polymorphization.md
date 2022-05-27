---
layout: post
title: Polymorphization
---

# Polymorphization
```
David Wood
Edinburgh Research Centre, UK
Huawei Technology, Inc.
```

Polymorphization is a code-size optimisation, aimed at reducing unnecessary
monomorphization, thereby reducing the quantity of LLVM IR generated. By
reducing the quantity of generated LLVM IR, it is expected that time spent in
LLVM during compilation will decrease, resulting in improved overall
compilation times.

## Rationale
Rust's "State of Rust" yearly survey has consistently found that improved build
times is one of the most frequently requested improvements from the Rust
community. This is consistent with the experiences of teams within Huawei that
use Rust.

Rust’s compilation model is different from other programming languages. In C++,
the compilation unit is a single file, whereas Rust’s compilation unit is a
crate (an entire library or application). While compilation times of entire C++
and entire Rust projects are generally comparable, modification of a single C++
file requires far less recompilation than modification of a single Rust file.
In recent years, implementation of incremental compilation into rustc has
improved recompilation times after small modifications to code.

Rust generates machine code using LLVM, a collection of modular and reusable
compiler and toolchain technologies. At LLVM’s core is a language-independent
optimiser, and code-generation support for multiple processors. Languages
including Rust, Swift, Julia and C/C++ have compilers using LLVM as a
“backend”. By de-duplicating the effort of efficient code generation, LLVM
enables compiler engineers to focus on implementing the parts of their compiler
that are specific to the language (in the “frontend” of the compiler).

Compiler frontends are expected to transform their internal representation of
the user’s source code into LLVM IR, an intermediate representation from LLVM
which enables optimisation and code-generation to be written without knowledge
of the source language. While LLVM enables Rust to have world-class runtime
performance, LLVM is a large framework which is not focused on compile-time
performance. This is exacerbated by technical debt in rustc which results in
the generation of low-quality LLVM IR. Recent work on MIR optimisations have
improved the quality of rustc’s generated LLVM IR, and reduced the work
required by LLVM to optimise and produce machine code.

In addition, rustc monomorphises generic functions. Monomorphisation is a
strategy for compiling generic code, which duplicates the definition of generic
functions for every instantiation, producing significantly more generated code
than other translation strategies. As a result, LLVM has to perform significant
work to eliminate or optimise redundant IR.

Within Rayon, a data-parallelism library, a pull request was submitted to
reduce the usage of closures by moving them into nested functions, which do not
inherit generic parameters (and thus would have fewer unnecessary
monomorphisations). Similarly, in rustc, the same author submitted a pull
request to apply the same optimisation manually to the language’s standard
library. Likewise, in Serde, a popular serialisation library, it was observed
that a significant proportion of LLVM IR generated was the result of a tiny
closure within a generic function (which inherited and did not use generic
parameters of the parent function, resulting in unnecessary monomorphisations).
In this particular case, the closure contributed more LLVM IR than all but five
significantly larger functions. These examples suggest that reducing
unnecessary monomorphizations could result in compilation time improvements.

## Detailed Explanation
Polymorphisation is an optimisation which determines when functions, closures
and generators could remain polymorphic during code generation.

Rust supports parameterising functions by constants or types - these are known
as generic functions and this feature is similar to generics in other
languages, like Java’s generics or C++’s templates. Generic functions and types
are a desirable feature for programmers as they enable greater code reuse. When
generating machine code, there are two approaches to dealing with generic
functions - monomorphisation and boxing.

C++ and Rust perform monomorphisation, where multiple copies of a function are
generated for each of the types or constants that the function was instantiated
with. In contrast, Java performs dynamic dispatch, where each object is
heap-allocated and a single copy of a function is generated, which takes an
address.

In addition, Rust compiles to LLVM IR, the intermediate representation of LLVM.
LLVM IR doesn’t have any concept of generics, so Rust must perform either
dynamic dispatch or monomorphisation.

The initial polymorphisation analysis implemented in this project determines
when a type or constant parameter to a function, closure or generator is
unused, and thus when this would result in multiple redundant copies of the
function being generated. By generating fewer redundant monomorphisations of
functions in the LLVM IR, there would be less work for LLVM to do, reducing
compilation times and code size.

Types with unused generic parameters are disallowed by rustc, but there are no
checks for unused generic parameters in functions. Despite this, it is assumed
that it is rare for programmers to write functions which have unused generic
parameters. However, closures inherit the generic parameters of their parent
functions and often don’t make use of these parameters.

Consider the following example from Serde, introduced earlier:

```rust
fn parse_value<V>(
  &mut self,
  visitor: V
) -> Result<V::Value>
where
  V: de::Visitor<'de>,
{
  let peek = match /* ... */ {
    // ...
  };
  let value = match peek {
    // ...
  };
  match value {
    Ok(value) => Ok(value),
    Err(err) => Err(err.fix_position(
      |code| self.error(code))),
  }
}
```

`parse_value` is a heavily used function which takes a single type parameter,
`V`, and is instantiated many times with different types (a second type
parameter from the surrounding block, `R`, is in scope too, which will also
vary). This function contains one tiny closure on line 16 which would be
monomorphised for each instantiation of `parse_value`. In Serde, instantiations
of this closure contributed more LLVM IR than all but five larger functions in
the library.

In order to determine which items will be included in the generated LLVM IR for
a crate, rustc performs monomorphisation collection. Non-generic, non-const
functions map to one LLVM artefact, whereas generic functions can contribute
zero to *N* artefacts depending on the number of instantiations of the
function. Monomorphisations can be produced from instantiations of functions
defined in other crates.

*Mono items* are anything that results in a function or global in the LLVM IR
of a codegen unit. Mono items can reference other mono items, for example, if a
function `baz` references a function `quux` then the mono item for `baz` will
reference the mono item for `quux` (typically this results in the generated
LLVM IR for `baz` referencing the generated LLVM IR for `quux` too). Therefore,
mono items form a directed graph, known as the *mono item graph*, which
contains all items necessary for codegen of the entire program. In order to
compute the mono item graph, the collector starts with the roots - non-generic
syntactic items in the source code. Roots are found by walking the HIR (an
intermediate representation in rustc) of the crate, and whenever a non-generic
function, method or static item is found, a mono item is created and added to
the set of mono items.

Polymorphization's analysis is performed before a mono item is added to the
mono item set. Polymorphization modifies the mono item depending on the result
of its analysis, preventing mono items from varying on the basis of the
instantiation of their unused generic parameters. Due to this intervention,
fewer distinct mono items will be in the mono item set, resulting in less LLVM
IR being generated.

## Updates
- [x] Implement initial version of polymorphization ([#69749])
- [x] Add helper function for checking whether only used generic parameters
      need substitution ([#74717])
- [x] Use `FiniteBitSet<u32>` in polymorphization; avoid encoding results for
      functions where every parammeter is used; and add debug assertions ([#75155])
- [x] Polymorphize closures/generators captured as upvars by polymorphized
      closures/generators ([#75255])
- [x] Visit promoted MIR of unevaluated constants during polymorphization
      analysis ([#75260])
- [x] Apply substitutions to MIR shims during construction rather than codegen
      ([#75346])
- [x] Support unevaluated constants by skipping associated constants and
      prompted constants containing `Self` ([#75333])
- [x] Only polymorphize tupled upvar substitutions ([#75337])
- [x] Consider `I` used if `T` is used with `I: Foo<T>` predicate ([#75518])
- [x] Consider all parameters in a predicate used if any of them are ([#75595])
- [x] Enable polymorphization of shims; remove now-unnecessary predicate
      restrictions on polymorphization's analysis; and skip foreign items
      ([#89514])
- [ ] Fix remaining blocker - [#75325]
  - lcnr is working on a fix which should also enable greater polymorphization
    in the long run.
- [ ] Re-enable polymorphization

[#69749]: https://github.com/rust-lang/rust/pull/69749
[#74717]: https://github.com/rust-lang/rust/pull/74717
[#75155]: https://github.com/rust-lang/rust/pull/75155
[#75255]: https://github.com/rust-lang/rust/pull/75255
[#75260]: https://github.com/rust-lang/rust/pull/75260
[#75346]: https://github.com/rust-lang/rust/pull/75346
[#75333]: https://github.com/rust-lang/rust/pull/75333
[#75337]: https://github.com/rust-lang/rust/pull/75337
[#75518]: https://github.com/rust-lang/rust/pull/75518
[#75595]: https://github.com/rust-lang/rust/pull/75595
[#89514]: https://github.com/rust-lang/rust/pull/89514
[#75325]: https://github.com/rust-lang/rust/pull/75325

---
layout: post
title: Trait System Rewrite
toc: true
---

# Trait System Rewrite 

```
Bastian Kauschke (lcnr)
Trusted Programming
Huawei Technologies, Inc. & LCNR
```

Tracked by https://github.com/rust-lang/types-team/issues/58

## Proposal
Start an initiative with the goal of replacing the current trait system implementation of rustc. This new implementation should fully replace both fulfill and evaluate and offer an API a lot closer to the ideal of `chalk`/`a-mir-formality`.

## Goals of this initiative

- greatly simplify future changes to the trait system, unblocking features like marker traits and fixes for existing soundness bugs
  - A type system unsoundness which is still not fixed would be https://github.com/rust-lang/rust/issues/100051 while a similar issue I've recently fixed is https://github.com/rust-lang/rust/issues/98543.
Note the required explicit (and without this bug useless) `for<'what, 'ever> &'what &'ever (): Trait,` clause on the impl in the example. Without it, this unsoundness cannot be triggered.
- better learnability, the current system is difficult to learn and understand
- far better[^1] caching with an estimated impact of
  - reducing compilation-time of some real world crates to less than half for less type-heavy crates 0% and 15% improvements
  - in rare cases, may initially slightly worsen performance
- reduces the chance of trait system bugs in the future

## Explicit non-goals of this initiative
This initiative does not intend to implement any major changes to the trait system as part of the replacement. The new replacement should closely mirror the old system at the time of replacement to minimize the risk of backwards compatibility issues.

We also do not intend to extract any shared code with rust-analyzer as part of this initiative. While that will be easier after this work has been completed, the sole focus of this initiative is to replace the existing solvers with a solver which results in the advantages noted above.

## Outline of the planned work

Start by clearly laying out how the compiler uses the existing trait solvers and what API has to be provided by the new solver.

Write a new solver which is directly integrated in the compiler with the goal of replacing the old implementation and builds on the experience of the Types Team over the last years from working on rustc, chalk, and a-mir-formality. This new solver will directly include the core architectural changes necessary in the future.

While this is happening any parts strongly tied to the architecture of the current solvers have to be rewritten where possible. The biggest challenge will be trait diagnostics, which should be rewritten to be as solver agnostic as possible. Instead of relying on solver internals, diagnostics should lazily recompute necessary information where possible. This may require a reimplementation of our trait diagnostics to replace the existing one.

## Rationale

The benefits described as part of the goals of this initiative and the fact that this unblocks work on other areas I am working on. An example of a dependency between Const Generics and my type system work is that default for arrays of all sizes requires us to first stabilize the marker traits feature (https://github.com/rust-lang/rust/issues/29864).
This feature requires this type system work.


## Roadmap

While I previously intended to rewrite the existing solver in place I ended up finding a bunch of cyclic dependencies between the major changes, making an incremental rewrite nearly impossible. At the Types Team Meetup from the 30.11.2022 to the 02.12.2022 we decided on writing a new solver to slowly replace the old one instead.

The major direct behavior improvement of the new solver will be **non-fatal overflow** and an approach far better suited to caching and coinduction. Our first milestone will be to get the new solver to a point where it can be used expermentally as the solver for rustc. The next steps will be to continously improve the (unstable) integration of our new solver. We can then start to use it by default for some parts of the compiler. The final milestone will be to enable by default. 

For the (stable) integration of the solver there are still many unknown unknowns, especially "refined API surface of the trait solver" requires research to figure out the necessary steps. It is known that diagnostics heavily rely on trait system internals, but the amount of effort required to refactor that is still not clear. The desired API surface of the trait solver will also continue to evolve as we are implementing the new solver.

The rewrite initiative will only work on steps directly required for "GOAL: replace current trait solver impl". Once this is done, the initiative will be closed again and the blockers for keyword generics and const generics can be tackled next. At this point we should get the compile-time improvements described in https://github.com/rust-lang/types-team/issues/58.

## Updates

- [x] implement the skeleton of the new solver https://github.com/rust-lang/rust/pull/105661
- [ ] add the integration of the new solver in rustc
- [ ] implement all predicates in the new solver
- [ ] verify that the approach to non-fatal overflow works correctly

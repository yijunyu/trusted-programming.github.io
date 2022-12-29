---
layout: post
title: Work in Progress to the Open Source Communities by Huawei Trusted Programming
toc: true
list_in_items: false
---

Rust community has come up several important roadmaps, where Huawei is making substantial contributions:

- [Language Roadmap](https://blog.rust-lang.org/inside-rust/2022/04/04/lang-roadmap-2024.html)
- [Compiler Team Roadmap](https://blog.rust-lang.org/inside-rust/2022/02/22/compiler-team-ambitions-2022.html)
- [Library Roadmap](https://icecube.m-ou.se/pub/rust-blog-draft/inside-rust/2022/04/20/libs-aspirations.html)

The Library team is also working on setting up a team for official crates like `log`, `libc`, `cc`, and 10+ more of those, to make sure they are maintained.

Here we highlight some of opensource work in progress by Huawei employees. If you want to look at our existing open-source contributions, 
take a look [here]({{ site.baseurl }}/articles/opensource-contributions.html).

{% assign articles = site.pages | sort: "dir" %}
{% assign prev_dir = nil %}
{% for article in articles %}
    {% assign dir = article.dir | replace: '\\', '/' %}
    {% if dir == '/articles/work-in-progress/' %}
        {% continue %}
    {% elsif article.layout == 'post' and dir contains 'articles/work-in-progress/' %}
        {% assign tmp = dir | split: '/' | slice: 3 %}
        {% if prev_dir == nil or tmp != '' and prev_dir != tmp %}
            {% assign prev_dir = tmp %}
### {{ tmp }}
        {% endif %}
More information on <b>{{ article.title }}</b> [here]({{ article.url }}).


### Rust roadmap features contributed by us:

25 -- 10

| Classification     |       Objectives        |  Features   |                  Program                   |             Leaders             |        Huawei Contributors        |
| ------------------ | ----------------------- | ----------- | ------------------------------------------ | ------------------------------- | --------------------------------- |
| Compiler 2022      | I-unsound               | Initiatives | 69 open issues,                            | oli-obk, pnkfelix               | lcnr (type system)                |
| Compiler 2022      | Async Rust              | Initiatives | async fn traits                            | nikomatsakis, tmandry           | lcnr (keyword generics)           |
| Compiler 2022      | Async Rust              | Initiatives | async crashdump initiative                 | michaelwoerister                |                                   |
| Compiler 2022      | Debugging               | Initiatives | wg-debugging, improve debuginfo            | wesleywiser, pnkfelix           |                                   |
| Compiler 2022      | Debugging               | Initiatives | wg-debugging, split debuginfo              | davidwco                        | davidwco                          |
| Compiler 2022      | Debugging               | Initiatives | wg-debugging, trace-based debugger         | pnkfelix                        |                                   |
| Compiler 2022      | Faster Builds           | Initiatives | performance workgroup                      | lqd, nnethercote                | lcnr                              |
| Compiler 2022      | Faster Builds           | Aspirations | parallel compilation                       | sparrowlii                      | sparrowlii                        |
| Compiler 2022      | Faster Builds           | Aspirations | incremental compilation                    | cjgillot, Aaron Hill            |                                   |
| Compiler 2022      | Faster Builds           | Aspirations | inter-crate sharing                        | nnethercote, lqd                |                                   |
| Compiler 2022      | Expressiveness          | Initiatives | GAT                                        | jackh726                        | lcnr                              |
| Compiler 2022      | Expressiveness          | Initiatives | async fn traits                            | tmandry                         |                                   |
| Compiler 2022      | Expressiveness          | Initiatives | safe transmute - zero cost type conversion | jswrenn                         |                                   |
| Compiler 2022      | Expressiveness          | Aspirations | const generics and const evaluation        | lcnr, oli-obk                   | lcnr                              |
| Compiler 2022      | Librarification         | Initiatives | rustc to rust-analyzer                     |                                 |                                   |
| Compiler 2022      | Librarification         | Initiatives | chalk                                      | jackh726, nikomatsakis          |                                   |
| Compiler 2022      | Librarification         | Aspirations | MIR tooling: Kani, Prusti, Creusot         | xldenis, pnkfelix               |                                   |
| Compiler 2022      | P-high backlog          | Aspirations |                                            | pnkfelix, wesleywiser, apiraino | lcnr, davidwco                    |
| Compiler 2022      | Team operations         | Aspirations | MCVE reduction tooling                     | pnkfelix                        |                                   |
| Compiler 2022      | Team operations         | Aspirations | Performance dashboard                      | rylev, Mark-Simulacrum          |                                   |
| Compiler 2022      | Backend                 | Aspirations | Fallback MIR implementation                | scottmcm                        |                                   |
| Compiler 2022      | Backend                 | Aspirations | Cranelift                                  | bjorn3                          |                                   |
| Compiler 2022      | Backend                 | Aspirations | GCC                                        | antoyo, bjorn3                  | antoyo                            |
| Compiler 2022      | Diagnostics             | Aspirations | full employment theorem                    | estebank                        | davidwco (diagnostic translation) |
| Compiler 2023      | Type system refactoring | Aspirations |                                            | lncr                            |                                   |

40 -- 16

| Classification     |                                  Objectives                                  |                                 Features                                  | Huawei Contributors  |
| ------------------ | ---------------------------------------------------------------------------- | ------------------------------------------------------------------------- | -------------------- |
| Language           | Flattening the curve - Make precise analysis, less rigmarole                 | polonius                                                                  |                      |
| Language           | Flattening the curve - Make precise analysis, less rigmarole                 | implied bounds                                                            | lcnr                 |
| Language           | Flattening the curve - Make precise analysis, less rigmarole                 | Deref patterns                                                            |                      |
| Language           | Flattening the curve - Make precise analysis, less rigmarole                 | perfect derive                                                            | lcnr                 |
| Language           | Flattening the curve - Make precise analysis, less rigmarole                 | autoref operators and clones                                              |                      |
| Language           | Flattening the curve - Express yourself more easily                          | let-else                                                                  |                      |
| Language           | Flattening the curve - Express yourself more easily                          | let-chains                                                                |                      |
| Language           | Flattening the curve - Express yourself more easily                          | "Type alias" impl Trait                                                   | guillaumegomez, lcnr |
| Language           | Flattening the curve - Express yourself more easily                          | expand impl Trait                                                         | lcnr                 |
| Language           | Flattening the curve - Express yourself more easily                          | generic associated types                                                  | lcnr                 |
| Language           | Flattening the curve - Express yourself more easily                          | generators                                                                |                      |
| Language           | Flattening the curve - Improve async support                                 | async fns in traits                                                       | lcnr                 |
| Language           | Flattening the curve - Improve async support                                 | async drop, async closures                                                |                      |
| Language           | Flattening the curve - Make dyn Trait more usable                            | dyn upcasting coercion initiative                                         |                      |
| Language           | Flattening the curve - Make dyn Trait more usable                            | dyn Trait object safe                                                     | joshtriplet, m-ou-se |
| Language           | Help Rust's users to help each other - Feature lifecycle                     | RFC 3240 edition-based method disambiguation                              |                      |
| Language           | Help Rust's users to help each other - Feature lifecycle                     | release trains for all ecosystem crates                                   |                      |
| Language           | Help Rust's users to help each other - Richer representations                | Async fn in traits                                                        | lcnr                 |
| Language           | Help Rust's users to help each other - Richer representations                | Const generics and constant evaluation                                    | lcnr                 |
| Language           | Help Rust's users to help each other - Richer representations                | Type alias impl trait                                                     | guillaumegomez, lcnr |
| Language           | Help Rust's users to help each other - Richer representations                | Generic associated types                                                  | lcnr                 |
| Language           | Help Rust's users to help each other - Richer representations                | allow libraries to implement the Fn traits                                |                      |
| Language           | Help Rust's users to help each other - Richer representations                | variadic tuples and generics                                              |                      |
| Language           | Help Rust's users to help each other - Custom developer experience           | allow libraries to provide custom lints for their users                   |                      |
| Language           | Help Rust's users to help each other - Custom developer experience           | allow libraries to control Rust diagnostics for trait resolution errors   | lcnr                 |
| Language           | Help Rust's users to help each other - Interoperability                      | RFC 2492, scoped contexts and capabilities                                |                      |
| Language           | Help Rust's users to help each other - Interoperability                      | Negative impls in coherence                                               |                      |
| Language           | Help Rust's users to help each other - Interoperability                      | async working group's portability initiative                              |                      |
| Language           | Help Rust's users to help each other - Interoperability                      | standard way to write performance benchmarks such as criterion            | nnethercote          |
| Language           | Help Rust's users to help each other - Interoperability                      | better support dynamic linking with richer and safer types than the C ABI | m-ou-se, joshtriplet |
| Language           | Help the Rust project scale - Set the status at a glance                     | initiative project board                                                  |                      |
| Language           | Help the Rust project scale - Set the status at a glance                     | backlog bonanza                                                           |                      |
| Language           | Help the Rust project scale - Set the status at a glance                     | reduce in-flight features                                                 | lcnr                 |
| Language           | Help the Rust project scale - Set the status at a glance                     | tracking issues                                                           |                      |
| Language           | Help the Rust project scale - Set the status at a glance                     | improving visualization                                                   |                      |
| Language           | Help the Rust project scale - Clear owners and communication                 | initiative system                                                         |                      |
| Language           | Help the Rust project scale - Clear owners and communication                 | formality team                                                            |                      |
| Language           | Help the Rust project scale - Clear owners and communication                 | beyond type system                                                        | lcnr                 |
| Language           | Help the Rust project scale - Efficient, open processes with tooling support | consensus decision process                                                |                      |
| Language           | Help the Rust project scale - Efficient, open processes with tooling support | improve rustbots                                                          |                      |

34 -- 25

| Classification |                                    Objectives                                    |                                    Features                                     |     Leaders      |  Huawei Contributors  |
| -------------- | -------------------------------------------------------------------------------- | ------------------------------------------------------------------------------- | ---------------- | --------------------- |
| Library        | Scalability - Evolvability of standard library and fixing mistakes               | Edition-based method disambiguation                                             |                  |                       |
| Library        | Scalability - Evolvability of standard library and fixing mistakes               | Range as Copy                                                                   | m-ou-se          |                       |
| Library        | Scalability - Evolvability of standard library and fixing mistakes               | lock-poisoning                                                                  | m-ou-se          | m-ou-se               |
| Library        | Scalability - Evolvability of standard library and fixing mistakes               | general mechanisms                                                              | m-ou-se          | m-ou-se               |
| Library        | Scalability - People and collaboration                                           | more complete guidelines                                                        | m-ou-se          | m-ou-se               |
| Library        | Scalability - People and collaboration                                           | more interaction with the rest of ecosystem                                     |                  | m-ou-se               |
| Library        | Scalability - Making std less special / Empowering other crates in the ecosystem | reduce dependencies on unsable features                                         | m-ou-se          | m-ou-se               |
| Library        | Scalability - Making std less special / Empowering other crates in the ecosystem | adapting to different platforms, std portability                                | amanieu          | m-ou-se               |
| Library        | Scalability - Making std less special / Empowering other crates in the ecosystem | adapting to different platforms, portability lint                               |                  |                       |
| Library        | Scalability - Making std less special / Empowering other crates in the ecosystem | adapting to different platforms, enable non-portable functionality              |                  |                       |
| Library        | Scalability - Making std less special / Empowering other crates in the ecosystem | adapting to different platforms, modularize std library                         |                  |                       |
| Library        | Improving and adding new APIs                                                    | Ergonomics: abs_diff, Path::is_symlink, iter::from_fn, NonZero*::saturating_add | m-ou-se          | m-ou-se               |
| Library        | Improving and adding new APIs                                                    | Standardizing some bigger features the ecosystems needs: async                  | joshtriplet      | m-ou-se               |
| Library        | Improving and adding new APIs                                                    | Standardizing some bigger features the ecosystems needs: alloc                  |                  |                       |
| Library        | Improving and adding new APIs                                                    | Standardizing some bigger features the ecosystems needs: error/panic            | janelusby        | m-ou-se               |
| Library        | Improving and adding new APIs                                                    | Standardizing some bigger features the ecosystems needs: portable SIMD          |                  |                       |
| Library        | Improving and adding new APIs                                                    | Standardizing some bigger features the ecosystems needs: benchmarking           | nnethercote      | m-ou-se               |
| Library        | Reducing and improving unsafe code                                               | std::arch                                                                       | amanieu          |                       |
| Library        | Reducing and improving unsafe code                                               | std::simd                                                                       | sparrowlii       |                       |
| Library        | Reducing and improving unsafe code                                               | scoped threads                                                                  | m-ou-se          | m-ou-se               |
| Library        | Reducing and improving unsafe code                                               | atomic primitives                                                               | m-ou-se          | m-ou-se               |
| Library        | Reducing and improving unsafe code                                               | iterator with static lengths for arrays                                         |                  |                       |
| Library        | Reducing and improving unsafe code                                               | MaybeUninit methods                                                             |                  | m-ou-se               |
| Library        | Reducing and improving unsafe code                                               | NonNull and pointer methods                                                     |                  | m-ou-se               |
| Library        | Reducing and improving unsafe code                                               | more complete interface to OsString, Path, CString                              |                  | m-ou-se               |
| Library        | Reducing and improving unsafe code                                               | documentation for Pin and other unsafe types                                    |                  | m-ou-se               |
| Library        | Reducing and improving unsafe code                                               | File descriptors (OwnedFd, AsFd) and handles (OwnedHandle, AsHandle)            |                  | joshtriplett, m-ou-se |
| Library        | Improving implementations within std library                                     | core::fmt, format_args!(), fmt::Arguments                                       | m-ou-se          | m-ou-se               |
| Library        | Improving implementations within std library                                     | synchronization primitives such as Mutex, RwLock, Condvar                       | m-ou-se          | m-ou-se, amanieu      |
| Library        | Improving implementations within std library                                     | cleanup platform-specific code in std::sys                                      |                  | m-ou-se               |
| Library        | Improving implementations within std library                                     | avoiding allocations when possible in std::fs                                   |                  |                       |
| Library        | Improving implementations within std library                                     | making widely used types more light-weight, std::io::Error                      |                  |                       |
| Library        | Improving implementations within std library                                     | cleanup unnecessary SeqCst memory ordering                                      | m-ou-se, amanieu |                       |
| Library        | Improving implementations within std library                                     | optimizing thread local variables                                               | m-ou-se          | m-ou-se               |


    {% endif %}
{% endfor %}

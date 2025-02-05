---
layout: post
title: Contributions to the tree-sitter crate by Huawei Trusted Programming 
toc: true
---

Here is the list of the opensource contributions made by huawei employees on the [tree-sitter crate](https://github.com/tree-sitter/tree-sitter).

### Generate XML output of the abstract syntax trees, which has similar format to the SrcML schema, e.g., embedding the tokens with XML tags according to the ASTs

When you run tree-sitter, it will output the ASTs as a plain text file with some indention, while the concrete tokens are only shown by their offsets in the original source file. We created [this pull request](https://github.com/tree-sitter/tree-sitter/pull/863) to generate XML output of the ASTs, which has similar format to the SrcML schema, e.g., embedding the tokens with XML tags according to the ASTs. 

### Precompiled parser library for tree-sitter grammars:

Building tree-sitter parsers takes extra time. Here is a list of precompiled tree-sitter parsers built for the 21 officially supported programming languages. 
We created a new [crate](https://crates.io/crates/tree-sitter-parsers) for Rust developers (currently tested on X86_64, Raspberry Pi, and Windows), see
[Rust source code](https://github.com/yijunyu/tree-sitter-parsers/tree/rust). 

If you are using Python, the precompiled parsers can be imported through `pip install tree-sitter-parsers` as well, and the precompiled shared libraries can be found for [Linux](https://github.com/yijunyu/tree-sitter-parsers/tree/Linux) and [Windows](https://github.com/yijunyu/tree-sitter-parsers/tree/Windows), see [Python source code](https://github.com/yijunyu/tree-sitter-parsers). 

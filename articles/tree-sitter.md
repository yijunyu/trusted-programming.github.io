---
layout: post
title: Contributions to the tree-sitter crate by Huawei Trusted Programming 
toc: true
---

Here is the list of the opensource contributions made by huawei employees on the [tree-sitter crate](https://github.com/tree-sitter/tree-sitter).

### (tree-sitter) Generate XML output of the abstract syntax trees, which has similar format to the SrcML schema, e.g., embedding the tokens with XML tags according to the ASTs

When you run tree-sitter, it will output the ASTs as a plain text file with some indention, while the concrete tokens are only shown by their offsets in the original source file. We created [this pull request](https://github.com/tree-sitter/tree-sitter/pull/863) to generate XML output of the ASTs, which has similar format to the SrcML schema, e.g., embedding the tokens with XML tags according to the ASTs. 

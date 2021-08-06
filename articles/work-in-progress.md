---
layout: post
title: Work in Progress to the Open Source Communities by Huawei Trusted Programming 
toc: true
---

Here is the list of opensource work in progress by huawei employees. If you want to look at the opensource contributions, take a look [here]({{ site.baseurl }}/articles/opensource-contributions.html).

### (rustup) Add freebsd CI check

rustup recently got some issues on freebsd, adding this [CI check](https://github.com/rust-lang/rustup/pull/2783) will allow to prevent issues to be released unnoticed.

### (rustdoc) Add "copy to clipboard" and "show hidden lines" for codeblocks

This [pull request](https://github.com/rust-lang/rust/pull/86892) adds both features in the title. It's common to copy code from the code block examples and also common to want to see the "full" code (including the eventual wrappers and so on).

### (rustdoc) Fix union keyword highlighting in rustdoc HTML sources

The `union` keyword has a different meaning depending where it's used. Rustdoc simply didn't take this situation into account, prevent the `union` keyword to have the correct highlighting. This [pull request](https://github.com/rust-lang/rust/pull/87428) fixes this issue.

### (docs.rs) Unify keyboard events on docs.rs results

On <docs.rs>, you can navigate some pages using the keyboard. However, each page had its own handling for this behaviour. This [pull request](https://github.com/rust-lang/docs.rs/pull/1452) unifies the behaviour and the DOM.

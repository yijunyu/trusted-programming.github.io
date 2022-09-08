---
layout: post
title: Contributions to the askama project by Huawei Trusted Programming 
toc: true
---

Here is the list of the opensource contributions made by huawei employees on [askama](https://github.com/djc/askama).

### Add automatic whitespace removal config

This [pull request](https://github.com/djc/askama/pull/664) added a new configuration parameter: `suppress_whitespace`. Once enabled, it automatically trims whitespaces around jinja blocks.

### Rename `suppress_whitespace` config parameter `whitespace`

With this change, it allows to have multiple values given to this parameter. It was done in [#672](https://github.com/djc/askama/pull/672).

### Add `minimize` config for `whitespace` and add support for `~`

It allows to trim all but one whitespace around jinja blocks. `~` is the syntax equivalent. It was done in [#673](https://github.com/djc/askama/pull/673).

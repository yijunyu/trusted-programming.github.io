---
layout: post
title: Work in Progress to the Open Source Communities by Huawei Trusted Programming
toc: true
list_in_items: false
---

Here is the list of opensource work in progress by Huawei employees. If you want to look at our existing open-source contributions, take a look [here]({{ site.baseurl }}/articles/opensource-contributions.html).

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

    {% endif %}
{% endfor %}

### (rustc) implement RFC 2574

https://github.com/rust-lang/rust/pull/86546

### (rustc) Recover invalid assoc type bounds using ==

<https://github.com/rust-lang/rust/pull/87566>

### (rustc) Emit clearer diagnostics for parens around for loop heads

<https://github.com/rust-lang/rust/pull/86422>

# Language

# Library

### (ndarray) Implement construction from negative strides

<https://github.com/rust-ndarray/ndarray/pull/901>

### 

# Development Toolchain

### (rustup) Add freebsd CI check

rustup recently got some issues on freebsd, adding this [CI check](https://github.com/rust-lang/rustup/pull/2783) will allow to prevent issues to be released unnoticed.

### (rustdoc) Add "copy to clipboard" and "show hidden lines" for codeblocks

This [pull request](https://github.com/rust-lang/rust/pull/86892) adds both features in the title. It's common to copy code from the code block examples and also common to want to see the "full" code (including the eventual wrappers and so on).

### (docs.rs) Unify keyboard events on docs.rs results

On <docs.rs>, you can navigate some pages using the keyboard. However, each page had its own handling for this behaviour. This [pull request](https://github.com/rust-lang/docs.rs/pull/1452) unifies the behaviour and the DOM.


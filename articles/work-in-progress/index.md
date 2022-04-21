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

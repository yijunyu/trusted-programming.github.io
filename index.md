---
layout: default
title: Trusted Programming
---

# Trusted Programming

We are leading the smooth transition towards more trustworthy software engineering
through innovative R&D in **programming theory**, e.g., lambda calculus-based functional
programming, deep code learning-based intelligent software engineering; **programming
technology and methods**, e.g., model-driven software development (MDSD), domain-specific
languages (DSL), and **programming tools**, e.g., code transpiler, deep code learner, bug
localizer, etc.

<ul>
{% for post in site.posts %}
 {% unless post.url contains "_cn" %}
   <li><a href="{{ post.url | prepend: site.baseurl }}">{{ post.title }}</a></li>
 {% endunless %}
{% endfor %}
 <li><a href="{{ site.baseurl }}/articles/opensource-contributions.html">Huawei's opensource contributions</a></li>
 <li><a href="https://foundation.rust-lang.org">Huawei is one of the main contributors to the Rust Foundation</a></li>
 <li><a href="https://2020conf.rustcc.cn">The 1st Rust China Conf 2020, Shenzhen, China</a></li>
 <li><a href="https://apply.workable.com/huawei-ireland/j/823CFEB55B/">Join Huawei R&D for Trusted Programming -- Job Opportunities</a></li>
</ul>

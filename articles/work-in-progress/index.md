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

---
layout: post
title: Contributions to the Open Source Communities by Huawei Trusted Programming
toc: true
list_in_items: false
---

Here is the list of opensource projects where employees huawei contributed (if you want to see the work in progress, take a look [here]({{ site.baseurl }}/articles/work-in-progress/index.html)). Considering there are a lot of contributions overall, they are split by projects:

{% for article in site.pages %}
    {% assign dir = article.dir | replace: '/', '' | replace: '\\', '' %}
    {% if article.layout == 'post' and dir == 'articles' and article.list_in_items != false %}

### {{ article.name | split: ".md" | slice: 0, 1 }}

See the list of contributions [here]({{ site.baseurl }}{{ article.url }}).
    {% endif %}
{% endfor %}

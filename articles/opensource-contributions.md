---
layout: post
title: Contributions to the Open Source Communities by Huawei Trusted Programming
list_in_items: false
---

Here is the list of opensource projects where employees huawei contributed (if you want to see the work in progress, take a look [here]({{ site.baseurl }}/articles/work-in-progress/index.html)). Considering there are a lot of contributions overall, they are split by projects:

{%- assign total = '' -%}

{%- for article in site.pages -%}
    {%- assign dir = article.dir | replace: '\\', '/' -%}
    {%- assign check = article.dir | split:'/' -%}

    {%- if check.size > 2 and check[1] == 'articles' and check[2] != 'work-in-progress' -%}
        {% assign total = total | append: dir | append: ";" | append: article.name | append: ";" | append: article.url | append: "|" %}
    {%- endif -%}
{%- endfor -%}

{%- assign total = total | split: "|" | sort -%}
{%- assign previous = "" -%}

{%- for article in total -%}
    {%- if article == "" -%}
        {%- continue -%}
    {%- endif -%}

    {%- assign parts = article | split: ";" -%}

    {%- if previous != parts[0] -%}

{% assign part_name = parts[0] | split: "/" %}
{% assign previous = parts[0] %}

## {{ part_name[-1] }}

    {% endif %}
 * [{{ parts[1] | split: ".md" | slice: 0, 1 }}]({{ site.baseurl }}{{ parts[2] }})
{% endfor -%}

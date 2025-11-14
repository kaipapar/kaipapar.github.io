---
layout: page
title: Posts
---

<!-- {% for tag in site.tags %}
  <h3>{{ tag[0] }}</h3>
  <ul>
    {% for post in tag[1] %}
      <li><a href="{{ post.url }}">{{ post.date | date: "%B %Y" }} - {{ post.title }}</a></li>
    {% endfor %}
  </ul>
{% endfor %} -->

{% assign top_categories = "" | split: "" %}

{%- comment -%}
Collect unique top-level categories (e.g., "software")
{%- endcomment -%}
{% for post in site.posts %}
  {% assign parts = post.url | split: "/" %}
  {% assign top = parts[1] %}
  {% if top and top != "" %}
    {% unless top_categories contains top %}
      {% assign top_categories = top_categories | push: top %}
    {% endunless %}
  {% endif %}
{% endfor %}

{%- comment -%}
Iterate through top-level categories
{%- endcomment -%}
{% for top in top_categories %}
  <section class="category-block">
    <h2>{{ top | capitalize }}</h2>

    {% assign sub_categories = "" | split: "" %}

    {%- comment -%}
    Collect unique subcategories under this top-level
    {%- endcomment -%}
    {% for post in site.posts %}
      {% assign parts = post.url | split: "/" %}
      {% if parts[1] == top and parts[2] %}
        {% assign sub = parts[2] %}
        {% unless sub_categories contains sub %}
          {% assign sub_categories = sub_categories | push: sub %}
        {% endunless %}
      {% endif %}
    {% endfor %}

    {%- comment -%}
    List posts under each subcategory
    {%- endcomment -%}
    {% for sub in sub_categories %}
      <div class="subcategory-block">
        <h4>{{ sub | capitalize }}</h4>
        <ul>
          {% for post in site.posts %}
            {% assign parts = post.url | split: "/" %}
            {% if parts[1] == top and parts[2] == sub %}
              <li>
                <a href="{{ post.url }}">{{ post.title }}</a>
                <span class="post-date">{{ post.date | date: "%B %Y" }}</span>
              </li>
            {% endif %}
          {% endfor %}
        </ul>
      </div>
    {% endfor %}
  </section>
{% endfor %}
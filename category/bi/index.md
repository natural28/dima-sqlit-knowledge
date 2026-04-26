---
layout: default
title: "Все статьи по BI и аналитике"
description: "Все материалы по BI и аналитике: продуктовые метрики, data-driven подход, мышление аналитика, карьера и работа с бизнес-контекстом."
permalink: /category/bi/
category: bi
category_key: bi
---
{% assign category_key = page.category_key | downcase %}
{% assign sorted_pages = site.pages | sort: "date" | reverse %}
{% assign category_count = 0 %}

{% for post in sorted_pages %}
  {% if post.path contains 'posts/' and post.path contains '.md' %}
    {% assign post_categories = post.categories %}
    {% if post_categories == nil or post_categories == empty %}
      {% if post.category %}
        {% assign post_categories = post.category | split: "|" %}
      {% else %}
        {% assign post_categories = "" | split: "|" %}
      {% endif %}
    {% endif %}
    {% assign has_category = false %}
    {% for post_category in post_categories %}
      {% assign normalized_post_category = post_category | downcase | strip %}
      {% if normalized_post_category == category_key %}
        {% assign has_category = true %}
        {% break %}
      {% endif %}
    {% endfor %}
    {% if has_category %}
      {% assign category_count = category_count | plus: 1 %}
    {% endif %}
  {% endif %}
{% endfor %}

Раздел для материалов по аналитике и BI: продуктовые метрики, data-driven подход, мышление аналитика, карьера и всё, что помогает смотреть на данные не только технически, но и бизнесово. Сейчас здесь `{{ category_count }}` статей.

## Что есть в разделе

- продуктовые метрики и интерпретация цифр
- data-driven подход и аналитическое мышление
- карьера аналитика и рынок
- бизнес-контекст вокруг данных

## Все статьи

{% for post in sorted_pages %}
  {% if post.path contains 'posts/' and post.path contains '.md' %}
    {% assign post_categories = post.categories %}
    {% if post_categories == nil or post_categories == empty %}
      {% if post.category %}
        {% assign post_categories = post.category | split: "|" %}
      {% else %}
        {% assign post_categories = "" | split: "|" %}
      {% endif %}
    {% endif %}
    {% assign has_category = false %}
    {% for post_category in post_categories %}
      {% assign normalized_post_category = post_category | downcase | strip %}
      {% if normalized_post_category == category_key %}
        {% assign has_category = true %}
        {% break %}
      {% endif %}
    {% endfor %}
    {% if has_category %}
- [{{ post.title }}]({{ post.url | relative_url }}){% if post.date %} — {{ post.date | date: "%d.%m.%Y" }}{% endif %}
    {% endif %}
  {% endif %}
{% endfor %}

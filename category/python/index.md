---
layout: default
title: "Все статьи по Python"
description: "Подборка статей по Python для аналитика: pandas, автоматизация, Jupyter, полезные практики, ошибки и разборы рабочих задач."
permalink: /category/python/
category: python
category_key: python
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

Здесь собраны все материалы по Python для аналитика: `pandas`, автоматизация, работа с файлами, Jupyter Notebook, обработка ошибок и практические приемы для повседневной работы. Сейчас в разделе `{{ category_count }}` статей.

## Что есть в разделе

- `pandas` и работа с таблицами
- автоматизация рутины и полезные скрипты
- работа в Jupyter Notebook
- типичные ошибки и хорошие практики в Python

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

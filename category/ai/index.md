---
layout: default
title: "Все статьи по AI для аналитика"
description: "Подборка статей по AI для аналитика: как использовать нейросети в работе, как проверять ответы, выбирать инструменты и не терять качество."
permalink: /category/ai/
category: ai
category_key: ai
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

Здесь собраны материалы по AI для аналитика: где нейросети реально помогают в работе, как выбирать между инструментами, как проверять ответы и как использовать AI без самообмана. Сейчас в разделе `{{ category_count }}` статей.

## Что есть в разделе

- практическое применение AI в аналитике
- сравнение инструментов и моделей
- проверка ответов нейросетей
- ошибки и ограничения AI в реальной работе

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

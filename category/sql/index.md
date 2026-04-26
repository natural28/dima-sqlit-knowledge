---
layout: default
title: "Все статьи по SQL"
description: "Подборка всех статей по SQL: запросы, собеседования, оконные функции, метрики, ловушки и практические разборы для аналитиков."
permalink: /category/sql/
category: sql
category_key: sql
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

На этой странице собраны все материалы по SQL из базы знаний: от базовых конструкций и ловушек до оконных функций, метрик и задач с собеседований. Сейчас здесь `{{ category_count }}` статей.

## Что есть в разделе

- основы SQL и порядок выполнения запроса
- `JOIN`, `GROUP BY`, `HAVING`, `UNION`, `NULL`
- оконные функции и аналитические задачи
- собеседовательные разборы и практические SQL-хитрости

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

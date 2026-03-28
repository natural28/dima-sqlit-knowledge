# Workflow

## Как добавить новую статью

1. Создай новый Markdown-файл в `posts/`.
2. Используй slug как имя файла. Пример:
   `posts/moy-novyy-post.md`
3. Добавь front matter в начало файла.
4. Ниже напиши текст статьи.
5. Сохрани файл и проверь его локально.

Пример:

```md
---
layout: default
title: "Мой новый пост"
date: 2026-03-28
category: sql
slug: moy-novyy-post
excerpt: "Короткий анонс для карточки на главной."
description: "Короткое SEO-описание статьи."
sources:
  - label: "Telegram"
    url: "https://t.me/..."
  - label: "Статья"
    url: "https://example.com/..."
---

## О чем статья

Текст статьи...
```

## Почему Live Server не подходит

`Live Server` просто отдает файлы как есть. Этому проекту нужен именно `Jekyll`, потому что:

- должны отрендериться `{{ site.baseurl }}` и другие Liquid-переменные
- должны собраться страницы из `posts/`
- должен примениться layout из `_layouts/`

## Как посмотреть сайт локально

Выполни:

```powershell
gem install bundler
bundle install
bundle exec jekyll serve --livereload
```

Потом открой:

```text
http://127.0.0.1:4000/dima-sqlit-knowledge/
```

## Как остановить сервер

В том же окне PowerShell нажми:

```text
Ctrl + C
```

Если PowerShell спросит подтверждение, нажми:

```text
Y
```

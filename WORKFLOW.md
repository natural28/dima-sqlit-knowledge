# Workflow

## Add a new article

1. Create a new Markdown file in `posts/`.
2. Use the slug as the file name. Example:
   `posts/moy-novyy-post.md`
3. Add front matter at the top of the file.
4. Write the article body below it.
5. Save the file and check it locally.

Example file:

```md
---
layout: default
title: "Мой новый пост"
date: 2026-03-28
category: sql
slug: moy-novyy-post
excerpt: "Короткий анонс для карточки на главной."
description: "Короткое SEO-описание статьи."
telegram_link: "https://t.me/..."
---

## О чем статья

Текст статьи...
```

## Why Live Server does not work

`Live Server` serves files as-is. This project needs `Jekyll` because:

- `{{ site.baseurl }}` and other Liquid tags must be rendered
- collection pages from `posts/` must be built
- layouts from `_layouts/` must be applied

Because of that, plain static hosting is not enough for local preview.

## Local preview

1. Install Ruby with DevKit for Windows.
2. In the project root run:

```powershell
gem install bundler
bundle install
bundle exec jekyll serve --livereload
```

3. Open:

```text
http://127.0.0.1:4000/dima-sqlit-knowledge/
```

4. Open a post page and verify:

- content is visible
- links work
- the article opens from the home page

## Recommended publish flow

1. Create or edit the article in `posts/*.md`.
2. Run local preview with `bundle exec jekyll serve --livereload`.
3. Check the home page and the article page.
4. Commit changes to a feature branch.
5. Push the branch and open a pull request.

## Current architecture

The site now uses Markdown as the source of truth:

- the article page is rendered from `posts/*.md`
- the home page list is generated from the same Markdown files
- SEO fields also come from front matter in the Markdown file

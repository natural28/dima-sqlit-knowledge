# База знаний — Дима SQL-it

Статический сайт на Jekyll для GitHub Pages.

Сейчас проект устроен так:

- статьи лежат в `posts/*.md`
- каждая статья рендерится через `_layouts/default.html`
- главная страница собирает список статей из тех же markdown-файлов
- для уже существующих постов поддерживается `telegram_link`
- для новых постов можно использовать `sources:` с одной или несколькими ссылками

## Что уже сделано

- восстановлен рендер постов на GitHub Pages
- возвращена кнопка `Назад к списку постов` из layout
- удалены хардкодные ссылки назад из самих markdown-файлов
- добавлен локальный запуск через Jekyll
- убран `wdm`, который ломался на Ruby 3.4

## Структура

```text
.
├── _config.yml
├── _layouts/
│   └── default.html
├── posts/
│   └── *.md
├── index.html
├── Gemfile
├── POST_TEMPLATE.md
└── WORKFLOW.md
```

## Как запустить локально

1. Установи Ruby with DevKit для Windows.
2. Открой новый PowerShell.
3. Перейди в папку проекта:

```powershell
cd C:\Users\natural\Downloads\si\dima-sqlit-knowledge
```

4. Установи зависимости:

```powershell
gem install bundler
bundle install
```

5. Запусти сайт:

```powershell
bundle exec jekyll serve --livereload
```

6. Открой в браузере:

```text
http://127.0.0.1:4000/dima-sqlit-knowledge/
```

## Как остановить сервер

В том же окне PowerShell нажми:

```text
Ctrl + C
```

Если PowerShell спросит подтверждение остановки, нажми:

```text
Y
```

## Как добавить новую статью

1. Скопируй шаблон из `POST_TEMPLATE.md`
2. Создай новый файл в `posts/`, например:

```text
posts/moy-novyy-post.md
```

3. Заполни front matter и текст статьи
4. Запусти локальный сервер
5. Проверь главную страницу и сам пост
6. Закоммить изменения и запушь ветку

## Формат источников

Для старых постов можно оставлять:

```yaml
telegram_link: "https://t.me/..."
```

Для новых постов лучше использовать:

```yaml
sources:
  - label: "Telegram"
    url: "https://t.me/..."
  - label: "Habr"
    url: "https://habr.com/..."
  - label: "Сайт"
    url: "https://example.com/..."
```

## Если что-то снова ломается

Проверь по порядку:

1. Есть ли нормальный `title`, `date`, `category`, `slug` в посте
2. Запускается ли `bundle exec jekyll serve --livereload`
3. Открываешь ли именно адрес с `dima-sqlit-knowledge`
4. Нет ли в markdown старых ручных ссылок назад

## Полезные файлы

- `POST_TEMPLATE.md` — шаблон новой статьи
- `WORKFLOW.md` — короткий рабочий процесс
- `_layouts/default.html` — шаблон страницы поста
- `index.html` — главная страница

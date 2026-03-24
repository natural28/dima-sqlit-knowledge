# База знаний — Дима SQL-ит

Статический сайт с базой знаний по Data Analyst, созданный на основе постов из Telegram канала.

## 🚀 Быстрый старт

### 1. Создать репозиторий на GitHub

1. Зайти на https://github.com
2. Нажать "New repository"
3. Назвать репозиторий: `dima-sqlit-knowledge`
4. Выбрать "Public"
5. Нажать "Create repository"

### 2. Загрузить файлы

```bash
# Клонировать репозиторий
git clone https://github.com/YOUR_USERNAME/dima-sqlit-knowledge.git

# Скопировать файлы в репозиторий
cp -r knowledge-base/* dima-sqlit-knowledge/

# Перейти в папку репозитория
cd dima-sqlit-knowledge

# Добавить файлы в git
git add .

# Сделать коммит
git commit -m "Initial commit: база знаний"

# Отправить на GitHub
git push origin main
```

### 3. Настроить GitHub Pages

1. Зайти в настройки репозитория (Settings)
2. Прокрутить вниз до секции "Pages"
3. В "Source" выбрать "Deploy from a branch"
4. В "Branch" выбрать `main` и `/ (root)`
5. Нажать "Save"

### 4. Настроить домен

#### Вариант A: Через DNS (рекомендуется)

Добавить A записи в DNS настройках домена:

```
@  A  185.199.108.153
@  A  185.199.109.153
@  A  185.199.110.153
@  A  185.199.111.153
```

Или CNAME запись:

```
www  CNAME  YOUR_USERNAME.github.io
```

#### Вариант B: Через CNAME файл

Файл `CNAME` уже создан с содержимым `dima-sqlit.ru`.

### 5. Включить HTTPS

1. В настройках GitHub Pages (Settings → Pages)
2. Поставить галочку "Enforce HTTPS"
3. Подождать 5-10 минут для создания сертификата

## 📁 Структура проекта

```
knowledge-base/
├── index.html              # Главная страница
├── _config.yml             # Конфигурация Jekyll
├── CNAME                   # Настройка домена
├── README.md               # Этот файл
├── posts/                  # Статьи в формате Markdown
│   ├── sql-window-functions.md
│   ├── python-airflow-reports.md
│   └── ...
└── categories/             # Страницы категорий
    ├── sql.md
    ├── python.md
    └── ...
```

## ✍️ Как добавлять статьи

### 1. Создать файл

Создать новый `.md` файл в папке `posts/`:

```bash
touch posts/my-new-article.md
```

### 2. Написать содержимое

```markdown
# Название статьи

**Дата:** 2024-01-20  
**Категория:** SQL  
**Теги:** SQL, оптимизация

---

## Введение

Текст статьи...

## Основная часть

Код и примеры...

## Заключение

Выводы...

---

[← Назад к списку статей](/posts/)
```

### 3. Обновить главную страницу

Добавить статью в список на `index.html`:

```html
<article class="post-item">
  <h3 class="post-title">Название статьи</h3>
  <p class="post-meta">📅 2024-01-20 • 🏷️ SQL</p>
  <p class="post-excerpt">Краткое описание...</p>
  <a href="/posts/my-new-article/" class="post-link">Читать далее →</a>
</article>
```

### 4. Обновить категорию

Если статья относится к категории, добавить в соответствующий файл в `categories/`.

## 🎨 Кастомизация

### Изменить цвета

В `_config.yml` или в CSS файлах изменить переменные:

```css
:root {
  --accent-color: #a45eff;  /* Основной цвет */
  --accent-green: #10b981;  /* Зеленый акцент */
}
```

### Добавить аналитику

В `_config.yml` добавить:

```yaml
google_analytics: UA-XXXXXXXX-X
```

Или в `index.html` перед `</head>`:

```html
<!-- Google Analytics -->
<script async src="https://www.googletagmanager.com/gtag/js?id=UA-XXXXXXXX-X"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());
  gtag('config', 'UA-XXXXXXXX-X');
</script>
```

## 🔍 SEO оптимизация

### Мета-теги

Каждая страница должна иметь:

```html
<title>Название — База знаний Дима SQL-ит</title>
<meta name="description" content="Описание страницы...">
<meta name="keywords" content="ключевые, слова">
```

### Open Graph

Для соцсетей:

```html
<meta property="og:title" content="Название">
<meta property="og:description" content="Описание">
<meta property="og:image" content="URL картинки">
<meta property="og:url" content="URL страницы">
```

### Sitemap

Jekyll автоматически генерирует `sitemap.xml`.

## 📱 Мобильная версия

Сайт адаптивен и хорошо отображается на мобильных устройствах.

## 🛠 Технологии

- **Jekyll** — генератор статических сайтов
- **GitHub Pages** — хостинг
- **HTML/CSS** — верстка
- **Markdown** — контент

## 📞 Контакты

- **Telegram канал:** https://t.me/dima_sqlit
- **Менторство:** https://mentor.dima-sqlit.ru
- **Связь:** https://t.me/catdem

## 📄 Лицензия

MIT License

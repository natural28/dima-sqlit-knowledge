---
title: "Cookies"
permalink: /cookies/
---
<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>Cookies — Дима SQL-it</title>
  <style>
    body {
      margin: 0;
      background: #f4f8fb;
      color: #14202b;
      font-family: "Segoe UI", Arial, sans-serif;
      line-height: 1.7;
    }

    main {
      width: min(760px, calc(100% - 32px));
      margin: 0 auto;
      padding: 48px 0 64px;
    }

    h1 {
      margin: 0 0 18px;
      font-size: clamp(34px, 6vw, 52px);
      line-height: 1;
      letter-spacing: -0.04em;
    }

    h2 {
      margin: 34px 0 12px;
      font-size: 26px;
      line-height: 1.15;
      letter-spacing: -0.03em;
    }

    p,
    li {
      font-size: 18px;
    }

    a {
      color: #0284c7;
      font-weight: 700;
    }

    .back-link {
      display: inline-flex;
      margin-top: 28px;
    }
  </style>
</head>
<body>
  <main>
    <h1>Cookies</h1>
    <p>Сайт использует cookies и localStorage для базовой работы интерфейса и, если посетитель разрешил аналитику, для оценки посещаемости через Яндекс Метрику.</p>

    <h2>Обязательные данные</h2>
    <p>Они нужны для нормальной работы сайта: например, чтобы запомнить выбранную тему оформления и выбор в баннере cookies.</p>

    <h2>Аналитика</h2>
    <p>Если посетитель нажимает “Разрешить аналитику”, сайт включает Яндекс Метрику. Она помогает понять, какие страницы читают, откуда приходят посетители, сколько времени проводят на сайте и как взаимодействуют с материалами.</p>

    <h2>Как изменить выбор</h2>
    <p>Выбор хранится в localStorage браузера. Чтобы сбросить его, можно очистить данные сайта в настройках браузера.</p>

    <a class="back-link" href="{{ '/' | relative_url }}">← На главную</a>
  </main>
</body>
</html>

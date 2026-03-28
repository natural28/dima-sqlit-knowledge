---
layout: default
title: "SQL Ловушка: почему оператор NOT IN ломается, а EXISTS работает"
date: 2025-08-06
category: sql
slug: sql-lovushka-pochemu-operator-not-in-lomaetsya-a-e
excerpt: "⚠️ **SQL Ловушка: почему оператор NOT IN ломается, а EXISTS работает**:  Рассмотрим классическую проблему с которой встречались многие.  📊 Пример данн..."
description: "⚠️ **SQL Ловушка: почему оператор NOT IN ломается, а EXISTS работает**:  Рассмотрим классическую проблему с которой встречались многие.  📊 Пример данн..."
telegram_link: "https://t.me/c/2216284248/35"
---

Рассмотрим классическую проблему с которой встречались многие.

📊 Пример данных:
Таблица orders:
```
order_id
--------
1
2
3
4
```

И таблица delivered_orders:
```
order_id
--------
1
2
NULL  ← вот эта засада!
```

<u>⭐️</u><u> Задача: Найти не доставленные заказы</u>.

❌ <u>Почему оператор NOT IN в данном случае выдаст не верный результат:</u>

Пишем запрос:
```
SELECT *
FROM   orders
WHERE  order_id NOT IN (SELECT order_id FROM delivered_orders);
```
Подзапрос вернет: (1, 2, NULL)

Итоговый результат - ПУСТАЯ ВЫБОРКА!

Почему сломалось? Давайте посмотрим на логику работы оператора not in для строки 3 в таблице orders:
1️⃣ 3 ≠ 1 AND 3 ≠ 2 AND 3 ≠ NULL
Переведем эти условия на булевую логику:
2️⃣3 ≠ 1 (True) AND 3 ≠ 2 (True) AND 3 ≠ NULL (UNKNOWN) →  UNKNOWN (False)
То есть для любой строки условие не будет выполнено из-за NULL

✔️ <u>Что делать, чтобы не допустить такой проблемы?</u>

1️⃣Ответ - в подзапросе в условии where добавить is not null:
```
SELECT *
FROM   orders
WHERE  order_id NOT IN (SELECT order_id FROM delivered_orders where order_id is not null);
```
2️⃣Ответ - использовать оператор NOT EXISTS:
Пишем запрос:
```
SELECT *
FROM   orders o
WHERE  NOT EXISTS (
        SELECT 1
        FROM   delivered_orders d
        WHERE  d.order_id = o.order_id
);
```
Сравнение выполняется построчно; запись с NULL не совпадает ни с одним order_id, поэтому итог снова 3 и 4 — без риска забыть фильтр IS NOT NULL.

<u>Итог</u>:
😎 Если эта инструкция вам помогла, то кидайте 🔥 или ❤️! 
Встречались с такой проблемой и поняли как ее решить?

---

## Ссылки

- 📱 [Telegram канал](https://t.me/dima_sqlit)
- 🎯 [Менторство](https://mentor.dima-sqlit.ru)
- 💬 [Связаться](https://t.me/catdem)

---

[← Назад к списку постов](/posts/)

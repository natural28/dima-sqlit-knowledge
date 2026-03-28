---
layout: default
title: "Как работать с оконными функциями в SQL"
date: 2024-01-15
category: sql
slug: sql-window-functions
---
## Что такое оконные функции?

Оконные функции — это мощный инструмент SQL, который позволяет выполнять вычисления над набором строк, связанных с текущей строкой. В отличие от агрегатных функций, оконные функции не схлопывают строки, а возвращают результат для каждой строки.

## Зачем они нужны?

- **Ранжирование данных** — присвоить порядковые номера строкам
- **Сравнение с предыдущими/следующими значениями** — анализ трендов
- **Вычисление накопительных итогов** — суммы, средние нарастающим итогом
- **Процентили и квантили** — статистический анализ

## Основной синтаксис

```sql
функция() OVER (
    [PARTITION BY столбец]
    [ORDER BY столбец]
    [ROWS/RANGE BETWEEN ... AND ...]
)
```

## Практические примеры

### 1. ROW_NUMBER() — нумерация строк

```sql
SELECT 
    employee_name,
    department,
    salary,
    ROW_NUMBER() OVER (PARTITION BY department ORDER BY salary DESC) as rank
FROM employees
```

**Результат:** Каждый сотрудник получает номер в своем отделе по зарплате.

### 2. RANK() и DENSE_RANK() — ранжирование с учетом одинаковых значений

```sql
SELECT 
    product_name,
    category,
    price,
    RANK() OVER (PARTITION BY category ORDER BY price DESC) as price_rank,
    DENSE_RANK() OVER (PARTITION BY category ORDER BY price DESC) as dense_rank
FROM products
```

**Разница:**
- `RANK()` — пропускает номера при одинаковых значениях (1, 2, 2, 4)
- `DENSE_RANK()` — не пропускает номера (1, 2, 2, 3)

### 3. LAG() и LEAD() — доступ к предыдущей/следующей строке

```sql
SELECT 
    date,
    revenue,
    LAG(revenue, 1) OVER (ORDER BY date) as prev_day_revenue,
    revenue - LAG(revenue, 1) OVER (ORDER BY date) as revenue_change
FROM daily_sales
```

**Использование:** Анализ изменений показателей во времени.

### 4. SUM() с окном — накопительные итоги

```sql
SELECT 
    month,
    revenue,
    SUM(revenue) OVER (ORDER BY month) as cumulative_revenue
FROM monthly_sales
```

**Результат:** Накопительная сумма дохода по месяцам.

### 5. AVG() с окном — скользящее среднее

```sql
SELECT 
    date,
    price,
    AVG(price) OVER (
        ORDER BY date 
        ROWS BETWEEN 6 PRECEDING AND CURRENT ROW
    ) as moving_avg_7_days
FROM stock_prices
```

**Результат:** Скользящее среднее за 7 дней.

## Частые ошибки

### Ошибка 1: Забыть PARTITION BY

```sql
-- Неправильно: нумерация по всему набору данных
SELECT *, ROW_NUMBER() OVER (ORDER BY date) as rn FROM sales

-- Правильно: нумерация по категориям
SELECT *, ROW_NUMBER() OVER (PARTITION BY category ORDER BY date) as rn FROM sales
```

### Ошибка 2: Неправильный ORDER BY

```sql
-- Неправильно: порядок не определен
SELECT *, SUM(amount) OVER () as total FROM transactions

-- Правильно: явный порядок для накопительной суммы
SELECT *, SUM(amount) OVER (ORDER BY date) as running_total FROM transactions
```

## Когда использовать оконные функции?

✅ **Используйте, когда нужно:**
- Ранжировать данные внутри групп
- Сравнивать строку с предыдущими/следующими
- Вычислять накопительные итоги
- Работать с процентилями

❌ **Не используйте, когда:**
- Нужны простые агрегаты (SUM, AVG, COUNT)
- Работаете с небольшими наборами данных
- Нужна максимальная производительность

## Производительность

Оконные функции могут быть медленными на больших данных. Советы:

1. **Используйте индексы** на столбцы в PARTITION BY и ORDER BY
2. **Ограничивайте данные** перед применением оконных функций
3. **Тестируйте** на реальных данных перед продакшеном

## Заключение

Оконные функции — это must-have навык для аналитика данных. Они позволяют решать сложные задачи простым и элегантным способом.

**Практическое задание:** Попробуйте написать запрос, который для каждого сотрудника покажет:
- Его зарплату
- Среднюю зарплату в отделе
- Разницу между его зарплатой и средней
- Его ранг в отделе по зарплате

---

## Полезные ссылки

- [Документация PostgreSQL](https://www.postgresql.org/docs/current/tutorial-window.html)
- [Оконные функции в MySQL](https://dev.mysql.com/doc/refman/8.0/en/window-functions.html)
- [Практика на LeetCode](https://leetcode.com/problemset/database/)

---

[← Назад к списку статей](/posts/)

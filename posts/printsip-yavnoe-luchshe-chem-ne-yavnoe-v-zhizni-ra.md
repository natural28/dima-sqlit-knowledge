---
layout: default
title: "Принцип \"явное лучше чем не явное\" в жизни, работе, sql, python:"
date: 2025-11-05
category: sql
slug: printsip-yavnoe-luchshe-chem-ne-yavnoe-v-zhizni-ra
telegram_link: "https://t.me/c/2216284248/93"
---
🤔 **Принцип "явное лучше чем не явное" в жизни, работе, sql, python:**

Выражение "явное лучше чем не явное" ("Explicit is better than implicit")  — одна из основных заповедей Zen of Python, которая применима не только к коду.
Давайте разберем этот принцип на простых примерах:

**Примеры в SQL:** 🛑

Неявное (плохо): непонятно, откуда поле
```
SELECT 
    employee_id,
    employee_name,
    department_name,
    salary
FROM employees
INNER JOIN departments ON employees.department_id = departments.department_id;
```
Проблема: В SELECT не указано, из какой таблицы берутся столбцы employee_id, employee_name, department_name и salary — из employees или из departments? Читающему код приходится тратить время на изучение схемы БД, чтобы понять источник каждого поля и избежать ошибок в интерпретации.

Явное (хорошо): понятно с первого взгляда
```
SELECT 
    e.employee_id,
    e.employee_name,
    d.department_name,
    e.salary
FROM employees AS e
INNER JOIN departments AS d ON e.department_id = d.department_id;
```
Почему лучше:
• Сразу видно: employee_id и salary из таблицы employees (алиас e), а department_name из departments (алиас d)
• Через полгода коллега (или ты сам) откроешь этот запрос и не потеряешь время на разбор
• и т.д.

**Примеры в Python:** 🛑

Неявное (плохо): непонятно, что на входе и выходе
```
def calculate_conversion(users, converted):
    return converted / users
```
<u>Проблемы:</u>
• Что такое users и converted? Int, float, или может быть список?
• Что возвращает функция? Float или int?
• Что делать, если users = 0? Будет деление на ноль.
• Нет документации — коллега не поймет, как использовать.

Явное (хорошо): типы и документация
```
def calculate_conversion(users: int, converted: int) -> float:
    """
    Рассчитывает конверсию пользователей.
    
    Args:
        users (int): Общее количество пользователей (должно быть > 0).
        converted (int): Количество конвертированных пользователей.
    
    Returns:
        float: Конверсия в долях (например, 0.05 для 5%).
    
    Raises:
        ValueError: Если users <= 0.
    
    Example:
        >>> calculate_conversion(1000, 50)
        0.05
    """
    if users <= 0:
        raise ValueError("Количество пользователей должно быть больше 0")
    
    return converted / users
```
<u>Почему лучше:</u>
• Type hints (users: int, -> float): Сразу видно, какие типы ожидаются и что вернется. IDE подсветит ошибки, если передашь строку вместо int
• Docstring: Полное описание — что функция делает, какие аргументы, что возвращает, какие исключения. Тот, кто использует твою функцию, не имеет вопросов по ее использованию.
• Валидация входных данных: Явно проверяем users > 0, чтобы не словить деление на ноль.
• Пример использования: Коллега может скопировать и сразу запустить.

<u>Итог:</u>
Явный подход в коде, SQL-запросах и целом в жизни — это основа.
Явное лучше неявного, потому что это экономит время, устраняет недопонимания и делает все проще.

🍸 Если вы нашли пост для себя полезным, то накидывайте реакций, чтобы я понимал, что вам эта тема интересна!
❤️Поддержать канал бустами, чтобы у автора появился дополнительный функционал можно - [здесь](https://t.me/boost/dima_sqlit) (это бесплатно и доступно с подпиской telegram premium)

❓  Что думаете об этом подходе (знали о нем или нет) ? Делитесь опытом в комментариях!
✔️ **Подпишитесь на канал**, чтобы не пропустить следующие посты.

Сделал сайт - оцените:
🚬 [Вопросы, обучение, консультации](http://mentor.dima-sqlit.ru/)

[@@dima_sqlit](https://t.me/dima_sqlit)

---

## Ссылки

- 📱 [Telegram канал](https://t.me/dima_sqlit)
- 🎯 [Менторство](https://mentor.dima-sqlit.ru)
- 💬 [Связаться](https://t.me/catdem)

---

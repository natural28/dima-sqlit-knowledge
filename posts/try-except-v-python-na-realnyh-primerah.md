---
layout: default
title: "try/except в Python на реальных примерах"
date: 2026-04-15
categories:
  - python
slug: try-except-v-python-na-realnyh-primerah
excerpt: "Разбираем try/except в Python на реальных примерах: чтение файлов, работа с API, преобразование типов и безопасные скрипты."
description: "Понятное объяснение try/except в Python на реальных примерах: как обрабатывать ошибки в скриптах аналитика и не ломать весь процесс."
---

`try/except` — одна из самых полезных конструкций в Python, особенно для аналитика. Скрипты часто ломаются не потому, что логика плохая, а потому что реальный мир грязный:

- файл не найден
- колонка отсутствует
- API не ответил
- число оказалось строкой
- в данных пришел `None`

Именно для этого нужен `try/except`.

## Базовая идея

```python
try:
    # код, который может упасть
except:
    # что делать, если ошибка произошла
```

Но на практике лучше ловить не все подряд, а конкретные ошибки.

## Пример 1. Преобразование строки в число

```python
value = "123"

try:
    number = int(value)
except ValueError:
    number = None
```

Если в `value` окажется `"abc"`, код не упадет, а обработает ситуацию.

## Пример 2. Чтение файла

```python
import pandas as pd

try:
    df = pd.read_csv("sales.csv")
except FileNotFoundError:
    print("Файл sales.csv не найден")
```

Это базовый, но очень жизненный кейс.

## Пример 3. Работа с колонкой

```python
try:
    avg_price = df["price"].mean()
except KeyError:
    print("В таблице нет колонки price")
```

Если структура файла поменялась, скрипт хотя бы объяснит, что именно случилось.

## Пример 4. Работа с API

```python
import requests

try:
    response = requests.get("https://api.example.com/data", timeout=10)
    response.raise_for_status()
    data = response.json()
except requests.exceptions.RequestException as e:
    print(f"Ошибка запроса: {e}")
```

Для аналитика это очень полезно, если ты забираешь данные из внешних сервисов.

## Почему не стоит писать просто except

Вот так:

```python
try:
    ...
except:
    print("Ошибка")
```

технически можно, но это плохая привычка.

Проблема в том, что ты ловишь вообще все:

- ошибки в данных
- ошибки сети
- ошибки логики
- даже неожиданные баги в коде

Из-за этого код становится труднее отлаживать.

Лучше так:

```python
except ValueError:
except FileNotFoundError:
except KeyError:
```

## try/except/else/finally

Есть еще полезные части конструкции:

```python
try:
    number = int(value)
except ValueError:
    print("Не удалось преобразовать")
else:
    print("Преобразование успешно")
finally:
    print("Этот блок выполнится в любом случае")
```

### Когда что использовать

- `except` — обработка ошибки
- `else` — код, если ошибки не было
- `finally` — код, который должен выполниться всегда

## Реальный кейс аналитика: пройти по многим файлам

```python
import pandas as pd
from pathlib import Path

for path in Path("data").glob("*.csv"):
    try:
        df = pd.read_csv(path)
        print(f"{path.name}: ok, строк = {len(df)}")
    except Exception as e:
        print(f"{path.name}: ошибка -> {e}")
```

Тут важно одно: если один файл битый, весь процесс не падает.

## Частая ошибка №1: скрывать ошибку и ничего не логировать

Плохо:

```python
try:
    ...
except:
    pass
```

Это очень опасно. Код молча проглатывает ошибку, и ты потом тратишь время на поиск странного поведения.

Лучше хотя бы так:

```python
except Exception as e:
    print(e)
```

## Частая ошибка №2: оборачивать слишком большой блок

Плохо:

```python
try:
    df = pd.read_csv(path)
    df["price"] = df["price"].astype(float)
    result = df.groupby("category")["price"].mean()
    save_result(result)
except Exception:
    print("Что-то пошло не так")
```

Здесь непонятно, где именно возникла проблема.

Лучше ловить ошибки ближе к конкретным рисковым местам.

## Итог

`try/except` нужен не для того, чтобы “прятать ошибки”, а чтобы управлять ими осознанно.

Для аналитика это особенно важно в задачах:

- чтения файлов
- обработки данных
- работы с API
- автоматизации отчетов

Главное правило:

- лови конкретные исключения
- не проглатывай ошибки молча
- делай обработку понятной для себя и для будущего дебага

---
layout: default
title: "Как загружать данные из CSV, Excel или Pandas DataFrame во временные таблицы ClickHouse:"
date: 2025-09-30
category: sql
slug: kak-zagruzhat-dannye-iz-csv-excel-ili-pandas-dataf
telegram_link: "https://t.me/c/2216284248/75"
---
😭 **Как загружать данные из CSV, Excel или Pandas DataFrame во временные таблицы ClickHouse:**

Работая с ClickHouse, часто сталкиваешься с ситуацией: тебе дали список из десятков тысяч user_id или сотен городов, и нужно отфильтровать данные по ним. Но часто возникают проблемы следующего характера:
❗️ Нет прав на создание таблиц (даже временных)
❗️ Подставлять всё через IN (...) в запрос через f строку — не вариант: СУБД ругается на длину запроса
✔️ Выход есть — внешние временные таблицы через ExternalData!

1️⃣**Что понадобится?

**• Устанавливаем библиотеку (если ещё не стоит):
```
pip install clickhouse-connect pandas
```

• Импортируем нужное:
```
import clickhouse_connect
import pandas as pd
from clickhouse_connect.driver.external import ExternalData
```

• Подключаемся к ClickHouse (настройки у всех разные, но вот пример подключения):
```
def get_click_dl_client():
    client = clickhouse_connect.get_client(
        host='host',
        port=8443,
        username='your_login',
        password='your_password',
        secure=True,
        verify=False,
        send_receive_timeout=6000000
    )
    return client

client = get_click_dl_client()
```

2️⃣ **Сценарий (у нас два файла):**

1) users.csv — содержит user_id (int) и флаг actual (String: «да»/«нет»)
2) city.xlsx — список городов в колонке city (String)
Нам нужно отобрать user_id только с actual = 'да' и только из указанных городов.

• Загружаем данные через ExternalData
Создаём объект — он будет "контейнером" для наших временных таблиц:
```
ext_data = ExternalData()
```

• Вариант 1: Прямая загрузка из CSV-файла
```
ext_data.add_file(
    file_name='user_table_tmp',          # имя таблицы в SQL-запросе
    fmt='CSVWithNames',                  # Формат с именами столбцов в первой строке (если без имён — используйте 'CSV')
    structure=['user_id Int32', 'actual String'],  # Структура - типы полей
    data=open('users.csv', 'rb').read()                     # путь к файлу (строка!)
)
```

• Вариант 2: Загрузка из Pandas DataFrame (из Excel):
```
city_df = pd.read_excel('city.xlsx')  # Читаем Excel в DataFrame

ext_data.add_file(
    file_name='city_table_tmp',  # имя таблицы в SQL-запросе
    fmt='CSVWithNames',  # С именами столбцов
    structure=['city String'],  # Структура - типы полей
    data=city_df.to_csv(index=False).encode('utf-8')  # Конвертируем DF в CSV-строку и в байты для передачи
)
```
Здесь .to_csv() превращает DataFrame в CSV-строку, а .encode('utf-8') — в байты для ExternalData.

• Теперь используем в запросе — без прав на создание таблиц в БД!
```
q = '''
SELECT
    user_id,
    SUM(money_spend) AS total_spend
FROM events
WHERE
    1=1
    AND user_id IN (SELECT user_id FROM user_table_tmp WHERE actual='да')
    AND city IN (SELECT city FROM city_table_tmp)
GROUP BY 1
'''

df_total_spend = client.query_df(q, external_data=ext_data)  # Выполняем с внешними данными
```

<u>Итог:</u>
ExternalData — супер-способ обойти отсутствие прав на temp tables в ClickHouse. Загружайте из файлов или DataFrame и джойньте/фильтруйте на здоровье!

🍸 Если вы нашли пост для себя полезным, то накидывайте реакций, чтобы я понимал, что вам эта тема интересна!
❤️Поддержать канал бустами, чтобы у автора появился дополнительный функционал можно - [здесь](https://t.me/boost/dima_sqlit) (это бесплатно и доступно с подпиской telegram premium)

❓  А вы сталкивались с ограничениями на IN или отсутствием прав в ClickHouse? Как решали? Делитесь в комментариях!
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

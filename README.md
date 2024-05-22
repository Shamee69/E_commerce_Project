# E-commerce First_Project, описание задач и таблиц:

### Стек: Python (Jupyter Notebook)
### Задачи по проекту:
1. Посчитать сколько пользователей, которые совершили покупку только один раз;
2. Сколько заказов в месяц в среднем не доставляется по разным причинам;
3. По каждому товару определить, в какой день недели товар чаще всего покупается;
4. Сколько у каждого из пользователей в среднем покупок в неделю (по месяцам);
5.1  Когортный анализ пользователей;
5.2 В период с января по декабрь выявить когорту с самым высоким retention на 3-й месяц.
6. RFM-анализ пользователей.

## Структура таблиц

### Таблица №1: olist_customers_datase.csv

| Столбец                  | Описание                              |
|--------------------------|---------------------------------------|
| customer_id              | Позаказный идентификатор пользователя |
| customer_unique_id       | Уникальный идентификатор пользователя (аналог номера паспорта) |
| customer_zip_code_prefix | Почтовый индекс пользователя          |
| customer_city            | Город доставки пользователя            |
| customer_state           | Штат доставки пользователя            |

### Таблица №2: olist_orders_dataset.csv

| Столбец                      | Описание                                      |
|------------------------------|-----------------------------------------------|
| order_id                     | Уникальный идентификатор заказа (номер чека) |
| customer_id                  | Позаказный идентификатор пользователя        |
| order_status                 | Статус заказа                                 |
| order_purchase_timestamp     | Время создания заказа                         |
| order_approved_at            | Время подтверждения оплаты заказа             |
| order_delivered_carrier_date | Время передачи заказа в логистическую службу |
| order_delivered_customer_date| Время доставки заказа                         |
| order_estimated_delivery_date| Обещанная дата доставки                      |

### Таблица №3: olist_order_items_dataset.csv

| Столбец               | Описание                                                |
|-----------------------|---------------------------------------------------------|
| order_id              | Уникальный идентификатор заказа (номер чека)           |
| order_item_id         | Идентификатор товара внутри одного заказа              |
| product_id            | Идентификатор товара (аналог штрихкода)                |
| seller_id             | Идентификатор производителя товара                     |
| shipping_limit_date   | Максимальная дата доставки продавцом                  |
| price                 | Цена за единицу товара                                 |
| freight_value         | Вес товара                                              |

# Решение

## Задача 1: Подсчет пользователей, совершивших покупку только один раз.

### Методика подсчета
Для подсчета количества пользователей, совершивших покупку только один раз, использовался следующий подход:
1. Сначала были объединены данные о клиентах с данными о заказах, чтобы учесть только тех пользователей, у которых есть заказы.
2. Затем были посчитаны количество заказов на каждого пользователя.
3. Пользователи, у которых был только один заказ, считались совершившими покупку только один раз.

### Результаты
В результате анализа было выявлено, что:
- По дате закрытия заказа: количество пользователей, совершивших покупку только один раз, составляет 90 555.

## Задача 2: Среднее количество не доставленных заказов в месяц.

### Определение не доставленного заказа
Не доставленный заказ - это заказ, который не имеет статуса "доставлен". Все другие статусы рассматриваются как причины недоставки.

### Методика подсчета
Для подсчета среднего количества не доставленных заказов в месяц был использован следующий подход:
1. Все заказы без даты доставки до клиента считаются недоставленными.
2. Для каждого месяца было посчитано количество недоставленных заказов по каждой причине.
3. Затем было посчитано среднее количество недоставленных заказов за весь период.

### Результаты
В результате анализа было определено, что в среднем в месяц не доставляется:
- Отмененных заказов:  26.04
- Недоступных заказов: 25.38
******************************************************************************************************************

## Задача 3: Определение дня недели, в который товар чаще всего покупается

### Методика решения
Для выполнения задачи были выполнены следующие шаги:
1. Объединение данных о заказах (olist_orders_dataset) и данных о товарах в заказах (olist_order_items_dataset) по идентификатору заказа (order_id).
2. Фильтрация данных таким образом, чтобы остались только заказы с статусами "processing", "shipped", "delivered".
3. Создание столбца с днем недели на основе даты и времени создания заказа.
4. Группировка данных по идентификатору товара и дню недели, подсчет количества покупок каждого товара в каждый день недели.
5. Определение дня недели, в который товар чаще всего покупается для каждого товара.

### Результаты
В результате анализа было определено, в какой день недели каждый товар чаще всего покупается.

## Задача 4: Определение среднего числа покупок в неделю для каждого пользователя (по месяцам)

### Методика решения
Для решения задачи были выполнены следующие шаги:
1. Объединение данных о заказах (olist_orders_dataset) с данными о клиентах (olist_customers_dataset) и данными о товарах в заказах (olist_order_items_dataset).
2. Фильтрация данных о заказах таким образом, чтобы остались только заказы с статусами "processing", "shipped", "delivered".
3. Подсчет числа покупок для каждого уникального клиента в каждом месяце.
4. Определение числа недель в каждом месяце.
5. Вычисление среднего числа покупок в неделю для каждого уникального клиента на основе подсчитанного числа покупок и числа недель в месяце.

### Результаты
В результате выполнения анализа было определено среднее количество покупок в неделю для каждого пользователя на основе данных о заказах. Результаты анализа представлены в таблице выше, где для каждого уникального клиента указано среднее количество покупок в неделю в каждом месяце.



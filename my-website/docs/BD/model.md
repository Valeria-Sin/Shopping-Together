---
title: ERD
sidebar_position: 1
---

# Модель данных

Тут будет ссылка на диаграмму 


## Заказ

| Название | Тип     | Описание              |
| -------- | ------- | --------------------- |
| id       | int     | Идентификатор заказа |
| PurchaseGroup_id     | int | Идентификатор группы |
| Order_status   | enum    | Статус заказа  |
| Order_price | decimal | цена заказа    |
| Order_StartDT | datetime | дата оформления заказа    |
---
title: Экраны приложения
sidebar_position: 2
---
# Экраны приложения

```plantuml

@startuml
left to right direction
actor "Покупатель" as Buyer
actor "Юридическое лицо" as LegalEntity
actor "Физическое лицо" as Individual
actor Продавец as Seller
rectangle "Приложение для совместных покупок" {
package "Экран поиска товара и создания заказа" {
usecase "Выполнить поиск товара" as UC2
usecase "Искать по названию" as UC3
usecase "Искать по категории" as UC4
usecase "Создать групповой заказ" as UC13
usecase "Участвовать в групповом заказе" as UC5
usecase "Указать количество товара" as UC6
usecase "Выбрать параметры товара" as UC7
usecase "Оформить заказ" as UC33
usecase "Оплатить заказ" as UC8
}
package "Чат и уведомление" {
usecase "Отправить сообщение в чат" as UC9
usecase "Отслеживать статус заказа" as UC10
usecase "Получить уведомление" as UC11
}
package "Управление финансами" {
usecase "Пополнить электронный кошелек" as UC14
usecase "Пополнить с банковской карты" as UC15
usecase "Пополнить с счета в банке" as UC16
usecase "Оформить возврат средств" as UC17
usecase "Заполнить заявку" as UC18
usecase "Прикрепить фотографии" as UC19
}
package "Отзывы" {
usecase "Оставить отзыв" as UC20
usecase "Оставить отзыв о продавце" as UC21
usecase "Оставить отзыв о товаре" as UC22
}
package "Экран продавца, управление" {
usecase "Обработать заказ" as UC23
usecase "Отправить заказ" as UC24
usecase "Посмотреть поступившие заказы" as UC25
usecase "Управлять товарами" as UC26
usecase "Добавить товары" as UC27
usecase "Добавить фотографию" as UC28
usecase "Добавить описание" as UC29
usecase "Добавить цену" as UC30
usecase "Добавить количество" as UC31
usecase "Удалить товары" as UC32
}
UC2 <-- UC3 : <<extend>>
UC2 <-- UC4 : <<extend>>
UC5 --> UC6 : <<include>>
UC5 --> UC7 : <<include>>
UC33 --> UC5 : <<include>>
UC5 --> UC8 : <<include>>
UC5 <-- UC9 : <<extend>>
UC5 <-- UC10 : <<extend>>
UC10 <-- UC11 : <<include>>
UC14 <-- UC15 : <<extend>>
UC14 <-- UC16 : <<extend>>
UC17 --> UC18 : <<include>>
UC17 --> UC19 : <<include>>
UC20 <-- UC21 : <<extend>>
UC20 <-- UC22 : <<extend>>
UC23 --> UC24 : <<include>>
UC23 --> UC25 : <<include>>
UC26 --> UC27 : <<include>>
UC27 --> UC28 : <<include>>
UC27 --> UC29 : <<include>>
UC27 --> UC30 : <<include>>
UC27 --> UC31 : <<include>>
UC26 --> UC32 : <<include>>
}
Buyer -- UC2
Buyer -- UC13
Buyer -- UC14
Buyer -- UC17
Buyer -- UC20
Buyer -- UC33
LegalEntity --|> Buyer
Individual --|> Buyer
Seller -- UC23
Seller -- UC26
@enduml


```

## Описание алгоритма
Экраны клиента
1. ** Поиск товаров	/search	
Для фильтрации и сортировки товара: GET /api/products/search

2. ** Список товаров	/products	
Для получения списка товаров: GET /api/products

3. ** Добавление товара в корзину	/cart	
Для добавления товара в корзину: POST /api/cart/add

4. ** Участвовать в групповом заказе	/group-order	
Для участия в групповом заказе:
POST /api/group-order/join

5. ** Управление финансами	/wallet	
Для получения информации о электронном кошельке: GET /api/wallet
Для пополнения электронного кошелька: POST /api/wallet/recharge

6. ** Форма возврата средств	/api/wallet/refund	
Для оформления заявки возврат средств: POST /api/wallet/refund

7. ** Экран отзывов	/reviews	
Для получения отзывов о товаре: GET /api/reviews?productId={productId}
Для добавления отзыва: POST /api/reviews/add

8. ** Уведомление и чат	/chat	
Для получения сообщений чата:  GET /api/chat/messages
для отправки сообщения: POST /api/chat/send

Экраны продавца

9. **Обработка заказа(продавец)	/seller/orders	
Для получения списка заказов: GET /api/seller/orders
Для обновления статуса заказов: POST /api/seller/orders/update

10. **Управление складом	/inventory	
Для получения списка товаров на складе: GET /api/inventory
Для редактирования товара: POST /api/inventory/edit
Для удаления товара: DELETE /api/inventory/delete/{productId}
Для фильтрации и сортировки товаров: GET /api/inventory?filter={filter}&sort={sort}
Добавить новый товар	/inventory/add	Для добавления нового товара: POST /api/inventory/add
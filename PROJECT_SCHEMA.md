# Схема данных — Кампус Фуд (Campus Food)

Актуальная структура сущностей приложения, используемая в оперативной памяти и локальной базе данных **IndexedDB** (`CampusFoodITMoscowDB`, версия 2).

---

## 1. Логические сущности

```text
Product (справочник меню в app.js)
- id: integer (PK)
- name: string
- category: enum("Выпечка", "Горячее", "Напитки")
- desc: string
- weight: string
- badge: string
- price: integer
- emoji: string

CartState (хранилище state -> key: "cart")
- productId: integer (ключ объекта -> Product.id)
- quantity: integer (значение)

Order (хранилище orders, keyPath: "id")
- id: integer (PK, автоинкремент от 101)
- items: array<OrderItem>
- subtotal: integer (сумма заказа до скидки)
- bonusSpent: integer (списано студенческих баллов, до 30%)
- cardPaid: integer (итоговая оплата картой)
- building: string (учебный корпус)
- room: string (номер аудитории / точка выдачи)
- delivery: string (время готовности к перемене)
- status: enum("Принят", "Готовится", "Курьер в пути", "Доставлен")
- createdAt: integer (Unix timestamp в мс, используется для автопродвижения статусов)

OrderItem (вложенный объект в Order.items)
- id: integer (FK -> Product.id)
- name: string
- price: integer
- qty: integer
```

---

## 2. Хранилища IndexedDB (`CampusFoodITMoscowDB`)

1. **`orders`** (`keyPath: "id"`) — история оформленных заказов; поддерживает экспорт и импорт в формате `orders_db.json`.
2. **`state`** (`keyPath: "key"`) — состояние сессии пользователя:
   * `cart` — текущая корзина (`{ [productId]: quantity }`)
   * `balance` — текущий бонусный баланс студента (по умолчанию `500`)
   * `orderId` — счётчик следующего номера заказа
   * `seeded` — флаг первичной инициализации из `orders_db.json`

---

## 3. Связи
* `Product` **1 — N** `CartState` (одно блюдо может быть добавлено в корзину в любом количестве).
* `Order` **1 — N** `OrderItem` (один заказ содержит список выбранных позиций с зафиксированной на момент покупки ценой).

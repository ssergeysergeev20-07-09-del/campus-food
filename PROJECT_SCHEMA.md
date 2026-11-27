# Схема данных — Кампус Фуд (проектирование, День 1)

```text
Product
- id: integer (PK)
- name: string
- category: enum(Выпечка, Горячее, Напитки)
- description: string
- weight: string
- price: integer
- image: string

CartItem
- productId: integer (FK -> Product.id)
- quantity: integer

Order
- id: integer (PK)
- building: string
- room: string
- deliveryTime: string
- total: integer
- paymentMethod: string
- status: string

OrderItem
- orderId: integer (FK -> Order.id)
- productId: integer (FK -> Product.id)
- quantity: integer
- unitPrice: integer
```

На текущем этапе схема спроектирована, но база данных не подключена. Это сохраняет границу между Днём 2 и Днём 3.

# Кампус Фуд — результат до Дня 3

## Что сделано (Дни 1–2)
- Подготовлена структура проекта и Android WebView-оболочка.
- Реализована навигация между разделами: меню, корзина, доставка, оплата, статус.
- Каталог блюд разбит на категории: выпечка, горячее, напитки.
- Карточки содержат название, состав/вес, цену и добавление в корзину.
- Корзина интерактивная: изменение количества, удаление уменьшением до нуля, пересчёт суммы.
- Подготовлены формы выбора корпуса, аудитории и времени доставки.
- Подготовлен демонстрационный экран оплаты и статусов заказа.
- Добавлена схема данных и описание запуска.

## Важно: граница Дня 3
Данные корзины живут только в оперативной памяти страницы. После перезагрузки они сбрасываются. SQLite/JSON, постоянное сохранение, удаление записей из локальной БД и восстановление после перезапуска намеренно НЕ реализованы — это задачи Дня 3.
Оплата, бонусный кошелёк, отправка заказа на кухню и статусы пока демонстрационные, без серверной интеграции.

## Схема данных (проектирование, День 1)
`Product(id, name, category, description, weight, price, image)`
`CartItem(productId, quantity)`
`Order(id, building, room, deliveryTime, total, paymentMethod, status)`
`OrderItem(orderId, productId, quantity, unitPrice)`

Связи: Product 1—N CartItem; Order 1—N OrderItem.

## Запуск HTML
Откройте `app/src/main/assets/index.html` в браузере.

## Сборка APK для Android 8.0+
1. Установите Android Studio и Android SDK Platform 34.
2. Откройте в Android Studio папку `CampusFood` (корень архива).
3. Дождитесь Gradle Sync.
4. Выберите Build → Build Bundle(s) / APK(s) → Build APK(s).
5. APK появится в `app/build/outputs/apk/debug/app-debug.apk`.

Минимальная версия Android — 8.0 (API 26). Для сборки нужен Android SDK и Gradle; в исходной среде подготовки архива SDK/Gradle отсутствуют, поэтому готовый APK здесь не собран.


UI update: desktop layout aligned to the supplied Figma screenshots; responsive mobile layout retained. Web and Android assets are synchronized. Android WebView DOM storage is enabled for IndexedDB persistence.

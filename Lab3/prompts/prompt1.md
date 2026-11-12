# Ітерація 1:

## Промпт
> Read following files:
> `Lab3/spec.md`, `Lab2/use-case-diagram.md`, `Lab1/ERD.md`.
> Generate two detailed PlantUML sequence diagrams based on `Lab3/spec.md`: `Lab3/scenario-1.puml` and `Lab3/scenario-2.puml` and render them to `Lab3/scenario-1.png` and `Lab3/scenario-2.png`.

>Follow next requirments:
> - Match all participants, entities, attributes, and enum statuses with `Lab1/ERD.md` and the behavior in `Lab2`.
> - Use realistic method and endpoint names, include dashed return messages, and add at least one combined fragment (`alt`, `opt`, or `loop`) in each diagram.
> - Keep activation bars continuous across conditional blocks: if a participant works outside or across multiple branches of a fragment, start its activation bar before the fragment and end it after the fragment closes.

>Generate all artifacts in English.
>If there are any uncovered questions, then ask about them.

## Контекст
- Файл: `Lab1/ERD.mmd`(commit: `d02d504f9e6104127b17240ecd6a7f8fc54bff01`)
- Файли: `Lab2` (commit: `2e8e58f8a2c969e73e4aae6b021c82a107346993`)
- Файл: `Lab3/spec.md` (commit: `241674d906b5594087b2025cc50373a579ebf1b9`)

## Очікуваний результат
- `scenario-1.puml`
- `scenario-2.puml`
- `scenario-1.png`
- `scenario-2.png`

## Аудит результатів

- **Статус**: Не прийнято

- **Хеш коміту згенерованих артефактів**: `680a151296cec09456e075f9761ca33f9123e754`

- **Згенеровані файли**:
- `scenario-1.puml` створено
- `scenario-2.puml` створено
- `scenario-1.png` створено
- `scenario-2.png` створено

- **Огляд результатів**:
    - **`scenario-1.png` та `scenario-2.png`**:
        - Діаграми візуально перенавантажені й розтягнуті. Перенесення рядків не спрацювало, бо в коді написано `\\n`. Рядки тексту дуже довгі.
    - **`scenario-1.puml`, `scenario-2.puml`**:
        - `activation bars` обриваються всередині окремих гілок `alt`/`else`, а частина ліній залишається незакритою.
        - Використано неіснуючі значення переліків (наприклад, `ONLINE_CARD` і `CARD` замість `ONLINE_GATEWAY` і `POS_TERMINAL`, `PAID` для `PaymentStatus` замість `AUTHORIZED` і `FAILED` для `ReservationStatus`).
        - При успішній оплаті та видачі в БД взагалі не створюється квитанція `Receipt`.
    - **`scenario-1.puml`**:
        - На кроці 14 використано зворотну стрілку від бекенду до фронтенду для `GET`-запиту.
        - Не оновлюється статус примірника `BookCopy` у БД: на `IN_USE` при успішній оплаті та назад на `AVAILABLE` (разом зі статусом `EXPIRED` для бронювання) при простроченні часу.
    - **`scenario-2.puml`**:
        - Фронтенд напряму показує решту користувачу замість того, щоб спершу відобразити її касиру.
        - Поля квитанції (`borrowed_at`, `due_date`) записуються в таблицю `BookCopy`, а робота із сутностями `Payment` та `Receipt` реалізована неповно.
        - Для часу використано SQL-функцію `NOW()` замість єдиного (UTC).

- **Необхідні зміни**:
1. Покращити візуальну структуру обох діаграм: прибрати помилки типу `\\n` та замінити завеликі SQL-запити на умовні, але реалістичні назви методів.
2. Виправити `activation bars`: закривати кожну лінію після завершення відповідного запиту і не обривати спільні лінії активації всередині гілок.
3. У `scenario-1.puml`: виправити напрямок запиту на кроці 14; узгодити роботу з таблицею `Payment` та значеннями енамів; додати створення `Receipt` і оновлення статусу `BookCopy` (`IN_USE` при оплаті та `AVAILABLE` при спливі TTL).
4. У `scenario-2.puml`: виправити взаємодію при розрахунку решти через касира. Перенести запис `borrowed_at` і `due_date` (через UTC) у створення сутності `Receipt`; додати збереження `Payment` (`CASH` / `POS_TERMINAL`, `AUTHORIZED`) та оновлення `Reservation.status` на `FULFILLED` і `BookCopy.status` на `IN_USE`.
5. Перегенерувати графічні рендери `scenario-1.png` та `scenario-2.png` після внесення виправлень.
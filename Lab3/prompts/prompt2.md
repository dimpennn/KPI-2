# Ітерація 2:

## Промпт
> Read following files:
> `Lab3/spec.md`, `Lab2/use-case-diagram.md`, `Lab1/ERD.md`.
> Fix and regenerate the two PlantUML sequence diagrams based on `Lab3/spec.md` and the audit in `prompt1.md`: `Lab3/scenario-1.puml` and `Lab3/scenario-2.puml`, and re-render them to `Lab3/scenario-1.png` and `Lab3/scenario-2.png`.

> Follow next requirements:
> 1. Improve the visual structure of both diagrams: remove errors such as `\\n` and replace overly long SQL queries with representative, yet realistic, method names. Use `actor` for human participants
> 2. Fix the `activation bars`: ensure each line closes after the corresponding request is completed, and avoid breaking continuous activation lines within branches.
> 3. In `scenario-1.puml`: correct the request direction at step 14; ensure consistency regarding the `Payment` table and enum values; include the creation of a `Receipt` and the updating of the `BookCopy` status (set to `IN_USE` upon payment, and to `AVAILABLE` when the TTL expires).
> 4. In `scenario-2.puml`: correct the interaction flow for calculating change via a cashier. Move the recording of `borrowed_at` and `due_date` (using UTC) to the `Receipt` entity creation step; include the saving of the `Payment` record (`CASH` / `POS_TERMINAL`, `AUTHORIZED`), as well as updating `Reservation.status` to `FULFILLED` and `BookCopy.status` to `IN_USE`.
> 5. Regenerate the graphical renders `scenario-1.png` and `scenario-2.png` after applying these fixes.
> 6. Strictly match all entities, attributes, and enum values from `Lab1/ERD.md`.

> Generate all artifacts in English.
> If there are any uncovered questions, then ask about them.

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

- **Хеш коміту згенерованих артефактів**: `4634b9e6a42d0cad98a1d90afeac407bb6619ad1`

- **Згенеровані файли**:
- `scenario-1.puml` створено
- `scenario-2.puml` створено
- `scenario-1.png` створено
- `scenario-2.png` створено

- **Огляд результатів**:
    - **`scenario-2.puml` та `scenario-2.png`**
        - Усі `activation bars` відкриваються і закриваються вчасно і правильно
        - Правильно використано статуси (узгоджено з ER-дфаграмою)
        - Учасники не дублюються в кінці схеми
    - **`scenario-1.puml` та `scenario-1.png`**
        - `activation bars` неправильні, особливо у Бекенду. В одних місцях навіть не активується а в гілці закривається, що неправильно
        - Неправильний статус бронювання поминно бути PAID, а не FULFILLED (це вже означає що примірник отримали)
        - На етапі генерації платіжної сесії в БД не зберігається початковий запис Payment зі статусом PENDING, тому в гілці відмови виклик markPaymentFailed звертається до несвореного платежу.
        - В умові alt написано now < expires_at - треба уточнити nowUTC < expires_at
        - Учасники не дублюються в кінці схеми

- **Необхідні зміни**:
- В обох сценарія продублювати Користувачів у кінці діаграми.
- `scenario-1.puml` та `scenario-1.png`:
    - виправити проблеми з `activation bars`
    - виправити статус бронювання на кроці 23
    - прибрати деактивацію `activation bar` в гілці alt де Payment.status == AUTHORIZED
    - створювати RECEIPT з статусом PENDING перед роботою з ним
    - уточнити заміть now - nowUTC
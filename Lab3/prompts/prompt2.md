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

- **Статус**:

- **Хеш коміту згенерованих артефактів**: ``

- **Згенеровані файли**:

- **Огляд результатів**:

- **Необхідні зміни**:
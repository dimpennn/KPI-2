# Ітерація 3:

## Промпт
> Read following files:
> `Lab3/spec.md`, `Lab2/use-case-diagram.md`, `Lab1/ERD.md`.
> Fix and update `Lab3/scenario-1.puml` and `Lab3/scenario-2.puml` based on the Iteration 2 audit feedback, and re-render them to `Lab3/scenario-1.png` and `Lab3/scenario-2.png`.

> Follow next requirements:
> 1. In both `scenario-1.puml` and `scenario-2.puml`: duplicate all participants/actors at the bottom of the lifelines.
> 2. In `scenario-1.puml`, fix `Backend` activation bars:
>    - Add the missing `activate Backend` right after the initial `Frontend -> Backend: POST ...` request.
>    - Move the second `activate Backend` to right after `Gateway -> Backend: webhook POST ...`.
>    - Remove `deactivate Backend` from inside the inner `alt`/`else` branches (`Payment.status == AUTHORIZED`) and place a single `deactivate Backend` after `end` (right after `Backend --> Gateway: 200 OK`).
> 3. In `scenario-1.puml`, persist a `Payment` record with status `PENDING` in the database right after creating the payment session, so `paymentId` exists before `finalizeReservation` or `markPaymentFailed` is called.
> 4. In `scenario-1.puml`, use `ReservationStatus` `PAID` instead of `FULFILLED` in `finalizeReservation` and in the final `GET /api/v1/reservations/{reservation_id}` response (step 23), as the book is awaiting delivery.
> 5. In `scenario-1.puml`, replace `now < expires_at` with `nowUTC < expires_at`.

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

# Ітерація 4:

## Промпт
>Read following files:
>`Lab3/spec.md`, `Lab1/ERD.mmd`, `Lab3/adr/0005-payment-grace-period.md`.
>Update `Lab3/scenario-1.puml` and `Lab3/scenario-2.puml` to enforce the Payment Grace period, and re-render them to `Lab3/scenario-1.png` and `Lab3/scenario-2.png`.

>Follow next requirements:
>1. Return the optimistic locking `version` field when fetching `Reservation` and pass `version` in all `Reservation` state transitions (`finalizeReservation` and `expireReservation` in `scenario-1.puml`; `recordPaymentAndIssueReceipt` in `scenario-2.puml`).
>2. In `scenario-1.puml`, when saving the `Payment` record with status `PENDING`, activate the Payment Grace period (`graceExpiresAt = expires_at + 5m UTC`) so TTL cleanup defers releasing the copy while payment is in progress.
>3. In `scenario-1.puml`, check `nowUTC <= graceExpiresAt` and verify `version` before updating `Reservation` to `PAID`.
>4. Preserve all existing activation bars, UTC checks, enum values, and duplicated bottom participants.

>Generate all artifacts in English.
>If there are any uncovered questions, then ask about them.

## Контекст
- Файл: `Lab1/ERD.mmd`(commit: `d02d504f9e6104127b17240ecd6a7f8fc54bff01`)
- Файл: `Lab3/spec.md` (commit: `241674d906b5594087b2025cc50373a579ebf1b9`)
- Файл: `Lab3/adr/0005-payment-grace-period.md` (commit: `3fd50cddab89ba9f76e9f8bb4c72f649dc6c628f`)

## Очікуваний результат
- `scenario-1.puml`
- `scenario-2.puml`
- `scenario-1.png`
- `scenario-2.png`

## Аудит результатів

- **Статус**: Прийнято

- **Хеш коміту згенерованих артефактів**: `710381de7fbc68d54f9798f429f78d28a4d39182`

- **Згенеровані файли**:
- `scenario-1.puml` оновлено
- `scenario-2.puml` оновлено
- `scenario-1.png` оновлено
- `scenario-2.png` оновлено

- **Огляд результатів**:
    - **`scenario-1.puml` та `scenario-2.puml`** - коректно додано Grace period, логіка обрахунку нового терміну TTL правильна. Перевірка TTL також правильна збережено і nowUTC що перевіряється з graceExpiresAt. Збережено всі `activation bars`.

- **Необхідні зміни**: Відсутні

- **Виснвок**: Артефакти оновлено правильно, діаграми досі читабельні, вимоги adr досягнуто.
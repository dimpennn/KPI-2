# Ітерація 2:

## Промт
> Update the existing files and generate new artifacts according to the required changes below:

> ears.md: Fix status lifecycle logic in EARS-03 and EARS-05: upon successful payment and receipt creation, the book copy status must change to IN_USE instead of remaining RESERVED.
> Prohibit reserving a copy if its status is RESERVED or IN_USE.
> Add a new EARS requirement for user authentication and authorization (e.g., EARS-12) as a prerequisite for secured system actions.

> user-stories.md: Fix the typo in the description of US-02.
> Add a new User Story for user authentication and authorization (e.g., US-00: User Authorization) as a prerequisite across scenarios.

> gherkin.md: Assign unique identifiers to every scenario (US-00-S1, US-01-S1, etc.).
> Add edge cases and negative/alternative scenarios (unauthenticated attempts, payment rejection) for comprehensive coverage.

> use-case-diagram.puml & render: Add generalization between Author and Reader actors: Author inherits all rights and capabilities of Reader (Author -|> Reader) with extended features.
> Generate a high-quality visual render of the diagram in PNG format: use-case-diagram.png.

> tracing-matrix.md: Rebuild the traceability matrix into a Many-to-Many cross-table (Requirements vs Use Cases UC-01...UC-08).
> Ensure the authorization requirement covers most protected Use Cases.
> Retain at least one uncovered requirement (Uncovered) with a detailed rationale.

> Expected Deliverables: Updated ears.md, user-stories.md, gherkin.md, tracing-matrix.md, use-case-diagram.puml, and the generated image use-case-diagram.png.

> If there are any uncovered questions, then ask about them.

## Контекст
- Файли: `Lab2` (commit: `477c2b848d9ef366461ff4288c36fd77ab26e19d`)
- Файл: `Lab2\adr\0003-reservation-ttl.md` (commit: `7750c1478c2fe45b23c7db70403fb471bebe02b9`)
- Файл: `Lab2\adr\0004-time-source.md` (commit: `78ee82ed2cab5ef7711e61756dbc74877a16715e`)
## Очікуваний результат
Оброблено файли:
- `ears.md` оновлено
- `user-stories.md` оновлено
- `gherkin.md` оновлено
- `tracing-matrix.md` оновлено
- `use-case-diagram.puml` оновлено
Створено:
- `use-case-diagram.png` створено

## Аудит результатів
- **Статус**: Прийнято
- **Хеш коміту згенерованих артефактів**: `ae1a36fe026739467cad8809eb3ff224e5f77ef4`
- **Згенеровані файли**:
    - `ears.md`
    - `user-stories.md`
    - `gherkin.md`
    - `tracing-matrix.md`
    - `use-case-diagram.puml`
    - `use-case-diagram.png`

- **Огляд результатів**:
    - **`ears.md`**: Логіка статусів примірників виправлена: після успішної оплати статус змінюється на IN_USE (EARS-03), бронювання заборонено якщо статус RESERVED або IN_USE (EARS-05). Додано вимоги EARS-12 та EARS-13 згідно ard. Додано EARS-14 для UC-05 (отримання примірника). Загалом 14 вимог.
    - **`user-stories.md`**: Створено 7 користувацьких історій, що охоплюють усіх акторів (Читач, Автор, Служба доставки, Платіжна система). Кожна має унікальний ідентифікатор та чіткі критерії приймання. Додано US-00 для авторизації, виправлено одруківку в US-02.
    - **`gherkin.md`**: Надано по 3-4 сценарії на кожну user story (усього 25 сценаріїв для US-00 … US-08). Кожен сценарій має унікальний ідентифікатор (US-00-S1 … US-06-S3), написаний у синтаксисі Gherkin (Feature, Scenario, Given, When, Then, And).
    - **`tracing-matrix.md`**: Оформлена у вигляді Markdown-таблиці з двосторонніми зв'язками «багато до багатьох». Чітко зафіксована непокрита вимога EARS-11 з описом. Додано вимоги EARS-12, EARS-13 та EARS-14.
    - **`use-case-diagram.puml`**: Прецеденти розписані детально, включено зв'язки include (обов'язкові підпроцеси) та extend (умовальна поведінка). Додано генералізацію Autor -|> Reader (Автор успадковує всі права Читача).
    - **`use-case-diagram.png`**: Згенеровано якісне зображення діаграми.

- **Рішення, що було прийнято під час аудиту (ADR)**:
    - `adr/0004-time-source.md`

- **Висновок**: Всі вимоги spec.md виконані. Артефакт прийнято до подальшої роботи.

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

## Очікуваний результат
Оброблено файли:
- `ears.md`
- `user-stories.md`
- `gherkin.md`
- `tracing-matrix.md`
- `use-case-diagram.puml`
Створено:
- `use-case-diagram.png`

## Аудит результатів
- **Статус**: Прийнято / Не прийнято / Прийнято частково
- **Хеш коміту згенерованих артефактів**: `<ai output commit hash>`
- **Згенеровані файли**: 
    - `artifact_1`
    - `artifact_2`
- **Огляд результатів**:
    - **`artifact_1`**: Детальний аналіз змісту, відповідності контексту чи ER-моделі.
    - **`artifact_2`**: Детальний аналіз синтаксису, семантики чи візуального рендеру.
- **Рішення, що було прийнято під час аудиту (ADR)**:
    - `adr/xxxx-name.md`
- **Необхідні зміни**:
    1. Зміна 1 + обґрунтування.
    2. Зміна 2 + обґрунтування.
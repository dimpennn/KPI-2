# Ітерація 3:

## Промт
> What needs to be fixed:

> - NFR section. Add a separate section following the EARS requirements covering: user demographics (who is using the system, and from which devices/browsers), interface language, response time (p95, including the profile, load volume, and measurement duration), load handling ("at least N" users) and behavior when limits are exceeded, payment security, and accessibility. Each requirement must be unambiguous, specifying exact numbers and thresholds.

> - Focus on a single Use Case (UC). The task now requires depth rather than breadth: select one complex UC (e.g., "Booking a book" or "Paying for a rental") and map out the flow: "user story → all associated scenarios → requirements." Be sure to include edge cases (e.g., simultaneous booking of the last available copy, or attempting payment after the TTL—Time-to-Live—has expired). The criteria in `spec.md`—"≥5 EARS requirements, ~3 scenarios per user story"—should be replaced with criteria focused on depth.

> - Diagram. "Payment authorization," "Calculating price and delivery time," and "Generating a waybill" are system actions—they do not involve a human actor. Furthermore, they are marked with the `<<extend>>` stereotype, yet they are connected using the `include` relationship. In the current diagram, the `extend` arrows point from the base UC to the extension (e.g., `UC3 ..> ExtPayRefund`, `UC2 ..> UC4`); the direction should be reversed. The payment system is an implementation detail, not an actor. The delivery service can only be considered an actor if it is justified that it initiates the interaction itself (e.g., by pushing status updates).

> - Minor points. There are typos in `gherkin.md` ("Автор", "каталіку"). `gherkin.md` and `tracing-matrix.md` contain scenarios US-08-S1…S3, yet user story US-08 is missing from `user-stories.md` (and US-07 is skipped); please synchronize the numbering.

> If there are any uncovered questions, then ask about them.

### Попутні питання
> Before I implement all fixes, confirm: should I add US-07 and US-08 to user-stories.md (synchronizing numbering with gherkin.md and tracing-matrix.md), or renumber US-08 to US-07 to fill the gap?
### Відповідь
> Renumber US-08 to US-07 everywhere (fills the gap, no US-08)

## Контекст
- Файли: `Lab2` (commit: `2e8e58f8a2c969e73e4aae6b021c82a107346993`)

## Очікуваний результат
Оброблено файли:
- `ears.md`
- `user-stories.md`
- `gherkin.md`
- `tracing-matrix.md`
- `use-case-diagram.puml`
- `use-case-diagram.png`

## Аудит результатів
- **Статус**: Не прийнято

- **Хеш коміту згенерованих артефактів**: `3c0cfcb85aed99abf1df34ef012ed67889fafca3`

- **Згенеровані файли**:
- `ears.md`
- `user-stories.md`
- `gherkin.md`
- `tracing-matrix.md`
- `use-case-diagram.puml`
- `use-case-diagram.png`

- **Огляд результатів**:
    - **`ears.md`**: Додано розділ нефункціональних вимог (NFR). Охоплюються демографія користувачів і пристроїв, мову інтерфейсу, чіткі числові пороги часу відгуку, обробку пікового навантаження.
    - **`user-stories.md`**: Виправлено одруківки та забезпечено чітку нумерацію без розривів. Додано актора Бібліотекар, якого не було зазначено в spec.md.
    - **`gherkin.md`**: Додано сценарії з акцентом на глибину і граничні випадки.
    - **`tracing-matrix.md`**: Вимога EARS-09 (автоматичне скасування бронювання після спливу TTL) у таблиці помилково прив'язана до сценаріїв US-02-S2, US-02-S5 замість відповідних їй сценаріїв US-02-S4 та US-03-S4. 
    - **`use-case-diagram.puml`**: Замість виправлення напрямку стрілок були повністю видалені всі зв'язки між прецедентами. Пропущені актори (Платіжна система та Служба доставки) і зв'язки з прецедентами UC-03 та UC-04.
    - **`use-case-diagram.png`**: Потребує оновлення та повторної генерації після виправлення пропусків у .puml файлі
- **Рішення, що було прийнято під час аудиту (ADR)**:
    - `adr/0005-delivery-service-actor.md`

- **Висновок**: Зміни не прийняті, нові файли не відповідають spec.md.

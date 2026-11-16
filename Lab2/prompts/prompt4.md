# Ітерація 4:

## Промпт
>Update the existing specification and requirements artifacts according to the architectural and UML modeling fixes below:

>Global Actor & Scope Rules:
>Completely remove the "Librarian" (Бібліотекар) actor from all files (spec.md, use-case-diagram.puml, ears.md, user-stories.md, gherkin.md, tracing-matrix.md). Model UC-05 ("Отримання примірника") as a direct interaction between the Reader (Читач) and the system after successful payment.
>Reclassify "Платіжна система" (Payment System) strictly as an implementation detail (external payment gateway), not an actor. Remove it from the diagram and from actor/role lists in requirements and user stories.
>Keep "Служба доставки" (Delivery Service) as an external actor, explicitly justifying that it actively initiates interaction with the system by sending push notifications (webhooks) with order movement status updates.
>Treat "Авторизація оплати", "Обчислення ціни та терміну доставки", and "Генерація накладної" as internal system actions within their parent use cases rather than standalone use cases or actor goals.

>use-case-diagram.puml & render:
>Label all actors in Ukrainian: `actor "Читач" as Reader`, `actor "Автор" as Author`, `actor "Служба доставки" as DeliveryService`. Keep the generalization `Author -|> Reader`.
>Configure internal relationships with valid UML arrow directions: `UC5 ..> UC3 : <<include>>`, `UC4 ..> UC2 : <<extend>>`, and `ExtPayRefund ..> UC3 : <<extend>>`.
>Generate a high-quality visual render of the updated diagram: use-case-diagram.png.

>ears.md:
>In the header, list system actors as `Читач`, `Автор`, `Служба доставки` (initiates push status updates), and separately note `Платіжна система` as an external service (implementation detail).
>Update EARS-03 and EARS-04 so that payment authorization is executed by the system via the payment gateway, and include refund initiation upon order cancellation in EARS-04.
>Refine EARS-09 (if TTL expires and the Reader has not paid or picked up the copy) and EARS-14 (Reader receives the reserved copy in UC-05 strictly after successful rental payment in UC-03).
>Remove librarians from NFR-01 and fix minor Ukrainian spelling/terminology in NFR-02, NFR-03, and NFR-05.

>user-stories.md:
>Set the roles list in the header to Читач, Автор, Служба доставки.
>Update US-03 (Role: Читач only): frame payment authorization via the payment gateway as an internal system action, and add an acceptance criterion for executing the refund extension when a paid order is canceled.
>Update US-04 ("Оформлення та відстеження доставки", Role: Читач, Служба доставки): specify that the Reader can optionally extend a book reservation with delivery, the system automatically calculates price/delivery time and generates the waybill, and the Delivery Service autonomously initiates push notifications on status changes.
>Update US-07 (Role: Читач): state that the Reader can receive the book copy only after completing the rental payment use case.

>gherkin.md:
>Update US-03 scenarios: in US-03-S1 and US-03-S2, model payment authorization through the payment gateway as a system action; replace US-03-S3 with the scenario "Повернення коштів при скасуванні оплаченого замовлення" (when a paid reservation is canceled before pickup, the system initiates a refund and sets the receipt payment status to ПОВЕРНЕНО).
>Update US-04 scenarios (US-04-S1, US-04-S2, US-04-S3) to reflect extending a reservation with delivery, system-executed price/time calculation and waybill generation, and the Delivery Service initiating push status updates.
>Update US-07 scenarios (US-07-S1, US-07-S2, US-07-S3) to describe the Reader directly confirming/picking up the copy after payment without a Librarian actor.

>tracing-matrix.md:
>Update the Use Case list to note that UC-03 includes the `ExtPayRefund` extension, UC-04 extends UC-02 via `<<extend>>`, and UC-05 includes UC-03 via `<<include>>`.
>Update the traceability matrix links: map EARS-03 and EARS-04 across both US-03/UC-03 and US-07/UC-05; map EARS-05 to US-02-S2 and US-02-S5; map EARS-06 to UC-02 and UC-04; fix EARS-09 to reference `US-02 / US-02-S4; US-03 / US-03-S4` under UC-02 and UC-03; update EARS-13 and EARS-14 mappings across the connected use cases.
>Add a detailed section "## Наскрізне трасування складних прецедентів («Історія → Сценарії → Вимоги»)" demonstrating the full path "Story → all Scenarios → Requirements" for UC-02 and UC-03, explicitly highlighting the edge cases: TTL expiration (US-02-S4), concurrent reservation of the last copy / race condition (US-02-S5), and payment attempt after TTL expiration (US-03-S4).

>Expected Deliverables: Updated spec.md, use-case-diagram.puml, ears.md, user-stories.md, gherkin.md, tracing-matrix.md, and the rendered image use-case-diagram.png.

>If there are any uncovered questions, then ask about them.

## Контекст
- Файл: `Lab2/spec.md` (commit: `ef1e8741887a29f2ddcdc37ecbb4ee56e454b944`)
- Файли: `Lab1` (commit: `1e7f45958ae3eb8f9e2fade20ed6d4bf8b3e329e`)

## Очікуваний результат
- `ears.md` оновлено
- `user-stories.md` оновлено
- `gherkin.md` оновлено
- `tracing-matrix.md` оновлено
- `use-case-diagram.puml` оновлено
- `use-case-diagram.png` оновлено

## Аудит результатів

- **Статус**: Прийнято

- **Хеш коміту згенерованих артефактів**: `d9d542b578183127742e360757f0bdca883cc40e`

- **Згенеровані файли**:
- `ears.md`
- `user-stories.md`
- `gherkin.md`
- `tracing-matrix.md`
- `use-case-diagram.puml`
- `use-case-diagram.png`

- **Огляд результатів**:
    - **`ears.md`**: Повністю вилучено актора «Бібліотекар». «Платіжну систему» зафіксовано як зовнішній сервіс, а «Службу доставки» як зовнішнього актора.
    - **`user-stories.md`**: Ролі узгоджено. Платіжну систему виключено з переліку акторів у US-03, а авторизацію оплати та повернення коштів переведено у внутрішні критерії. У US-04 зафіксовано автономні push-сповіщення Служби доставки.
    - **`gherkin.md`**: У сценаріях US-03-S1 та US-03-S2 авторизацію оплати представлено дією системи через шлюз, а в US-07-S1…S3 усунуто згадки про Бібліотекаря.
    - **`tracing-matrix.md`**: Окремим розділом реалізовано наскрізне трасування вглиб («Історія -> Сценарії -> Вимоги») для UC-02 та UC-03.
    - **`use-case-diagram.puml`**: Усіх акторів винесено за межі системи. Усі підписи перекладено українською мовою. Акторів «Бібліотекар» та «Платіжна система» вилучено. Додано прецедент `ExtPayRefund`, стрілки `<<extend>>` та `<<include>>` спрямовано правильно.
    - **`use-case-diagram.png`**: Рендер моделі якісний.

- **Необхідні зміни**: Відсутні.

- **Висновок**: Артефакти повністю відповідають усім вимогам.
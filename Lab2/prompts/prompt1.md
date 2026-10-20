# Ітерація 1:

## Промпт
> Examine Lab2/spec.md and Lab1 files Based on them generate artifacts:
> ears.md, user-stories.md, gherkin.md, tracing-matrix.md, use-case-diagram.puml - with requirements as listed at the end of spec.md. If there is any unspecified information, ask about it

### Попутні питання
> Lab2/spec.md adds e-commerce actors (Payment System, Delivery Service, Author with sales statistics) on top of Lab1's library model (reservation/receipt/copy status). The artifacts (EARS requirements, user stories, Gherkin scenarios, use cases) depend on how these combine. What is the intended business model for DimPenShelf?
### Відповідь
> DimPenShelf is a paid Library: readers reserve books and then pay to borrow them, additionaly reader can arange delivery.


## Контекст
- Файл: `Lab2/spec.md` (commit: `ef1e8741887a29f2ddcdc37ecbb4ee56e454b944`)
- Файли: `Lab1` (commit: `1e7f45958ae3eb8f9e2fade20ed6d4bf8b3e329e`)

## Очікуваний результат
- `ears.md` створено
- `user-stories.md` створено
- `gherkin.md` створено
- `tracing-matrix.md` створено
- `use-case-diagram.puml` створено


## Аудит результатів
- **Статус**: Прийнято частково
- **Хеш коміту згенерованих артефактів**: `477c2b848d9ef366461ff4288c36fd77ab26e19d`
- **Згенеровані файли**: 
    - `ears.md`
    - `user-stories.md`
    - `gherkin.md`
    - `tracing-matrix.md`
    - `use-case-diagram.puml`
- **Огляд результатів**:
    - **`ears.md`**: ears.md: Вимоги написані правильно та покривають усі потрібні пункти, проте виявлено логічні неточності в EARS-03 та EARS-05 щодо життєвого циклу статусів примірників.
    - **`user-stories.md`**: Історії існують для всіх типів акторів і відповідають контексту, проте в описі US-02 виявлено одруківку.
    - **`gherkin.md`**: Сценарії правильно, повністю охоплюють усі шість user stories по три сценарії на кожну, дотримуючись синтаксису Gherkin. Однак кожному Сценарію краще дати свій id, для кращого пошуку їх у tracing-matrix.
    - **`tracing-matrix.md`**: Матриця трасування оформлена правильно у вигляді Markdown-таблиці з двосторонніми зв'язками «багато до багатьох». Чітко зафіксована непокрита вимога із детальним описом необхідних доопрацювань.
    - **`use-case-diagram.puml`**: Прецеденти розписані детально, але не відображено успадкування прав Автора від Читача (згідно з бізнес-логікою Автор повинен мати всі можливості Читача). 
- **Рішення, що було прийнято під час аудиту (ADR)**:
    - `adr/0003-reservation-ttl.md`
- **Необхідні зміни**:
    1. Виправлення логіки статусів в EARS-03 та EARS-05: Після успішної оплати та створення квитанції статус примірника книги повинен змінюватися на IN_USE (а не залишатися RESERVED). Також система повинна забороняти бронювання примірника, якщо він має статус як RESERVED, так і IN_USE.
    2. Усунення друкарської помилки в US-02.
    3. Додавання ідентифікаторів сценаріїв у gherkin.md: Прописати унікальні ідентифікатори для кожного сценарію (наприклад, US-01-S1, US-01-S2 тощо).
    4. Оновлення use-case-diagram.puml: Додати зв'язок генералізації (успадкування) між акторами Автор і Читач.
    5. Додати рендер діаграми use-case-diagram.puml.
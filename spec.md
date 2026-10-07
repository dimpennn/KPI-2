Сутності та атрибути

User
- user_id: UUIDv7 (PK)
- fullName: string
- email: string
- registered_at: timestamp

Book
- book_id: UUIDv7 (PK)
- title: string
- authir: string
- total_pages: number
- number_of_copies: number

BookCopy
- copy_id: UUIDv7 (PK)
- book_id: UUIDv7 (FK)
- condition: BookCopyCondition
- status: BookCopyStatus

Review
- review_id: UUIDv7 (PK)
- user_id: UUIDv7 (FK)
- book_id: UUIDv7 (FK)
- rating: number
- comment: string
- created_at: timestamp

Receipt: 
- receipt_id: UUIDv7 (PK)
- user_id: UUIDv7 (FK)
- book_id: UUIDv7 (FK)
- borrowed_at: timestamp
- due_date: timestamp

Reservation
- reservation_id: UUIDv7 (PK)
- user_id: UUIDv7 (FK)
- book_id: UUIDv7 (FK)
- reserved_at: timestamp
- expires_at: timestamp
- status: ReservationStatus


Доменні типи даних (Enums)

BookCopyCondition:
- "NEW" - новий;
- "GOOD" - незначні пошкодження;
- "WORN" - помітні пошкодження;
- "DAMAGED" - пошкоджений (потребує ремонту або списання).

CopyStatus:
- "AVAILABLE" - на полиці;
- "RESERVED" - заброньований;
- "IN_USE" - виданий читачеві;
- "MAINTENANCE" - на реставрації.

ReservationStatus:
- "PENDING" - очікує обробки;
- "READY_FOR_PICKUP" - книга на полиці броні, чекає користувача;
- "FULFILLED" - читач прийшов і забрав;
- "EXPIRED" - час броні вийшов;
- "CANCELLED" - бронювання скасовано користувачем.


Критерії прийняття

- Модель описується виключно декларативним синтаксисом (Mermaid erDiagram).
- Проміжні таблиці без власних атрибутів заборонені.
- Модель нормалізована до 3NF.
- Усі первинні та зовнішні ключі мають єдиний узгоджений тип - UUID.
- Зв'язки мають точні кардинальності.
- Поля статусів (CopyStatus, ReservationStatus, ReturnStatus) та стану книги (PhysicalCondition) відповідають визначеним Enums.
- Усі часові мітки та дедлайни (створення, закінчення броні, повернення) уніфіковані типом TIMESTAMP.

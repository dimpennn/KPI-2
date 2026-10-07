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


Зв'язки

1. User -створює- Reservation ( 1 : 0..M ):
- Один користувач може мати нуль або багато бронювань ( 1 : 0..M )
- Одне бронювання належить одному і тільки одному користувачу ( 1 : 1 )

2. Book -запрошується в- Reservation ( 1 : 0..M ):
- Одне видання книги може бути заброньоване нуль або багато разів ( 1 : 0..M )
- Одне бронювання стосується одного і тільки одного видання книги ( 1 : 1 )

3. User -пише- Review ( 1 : 0..M ):
- Один користувач може написати нуль або багато відгуків ( 1 : 0..M )
- Один відгук створюється одним і тільки одним користувачем ( 1 : 1 )

4. Book -складається з- BookCopy ( 1 : 1..M ):
- Одне видання книги може містити один або багато фізичних примірників ( 1 : 1..M )
- Один примірник належить одному і тільки одному виданню книги ( 1 : 1 )

5. Book -отримує- Review ( 1 : 0..M ):
- Одне видання книги може отримати нуль або багато відгуків ( 1 : 0..M )
- Один відгук стосується одного і тільки одного видання книги ( 1 : 1 )

6. User -отримує- Receipt ( 1 : 0..M ):
- Один користувач може мати нуль або багато квитанцій на видачу книг ( 1 : 0..M )
- дна квитанція оформлюється на одного і тільки одного користувача ( 1 : 1 )

7. BookCopy -видається через- Receipt ( 1 : 0..M ):
- Один примірник може фігурувати в нулі або багатьох квитанціях за весь час циркуляції ( 1 : 0..M )
- Одна квитанція фіксує видачу одного і тільки одного фізичного примірника ( 1 : 1 )

Критерії прийняття

- Модель описується виключно декларативним синтаксисом (Mermaid erDiagram).
- Проміжні таблиці без власних атрибутів заборонені.
- Модель нормалізована до 3NF.
- Усі первинні та зовнішні ключі мають єдиний узгоджений тип - UUID.
- Зв'язки мають точні кардинальності.
- Поля статусів (CopyStatus, ReservationStatus, ReturnStatus) та стану книги (PhysicalCondition) відповідають визначеним Enums.
- Усі часові мітки та дедлайни (створення, закінчення броні, повернення) уніфіковані типом TIMESTAMP.

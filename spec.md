Сутності та атрибути

User
- user_id: UUIDv7
- fullName: string
- email: string
- registered_at: timestamp

Book
- book_id: UUIDv7
- title: string
- authir: string
- total_pages: number
- number_of_copies: number

BookCopy
- copy_id: UUIDv7
- book_id: UUIDv7
- condition: BookCopyCondition
- status: BookCopyStatus

Review
- review_id: UUIDv7
- user_id: UUIDv7
- book_id: UUIDv7
- rating: number
- comment: string
- created_at: timestamp

Receipt: 
- receipt_id: UUIDv7
- user_id: UUIDv7
- book_id: UUIDv7
- borrowed_at: timestamp
- due_date: timestamp

Reservation
- reservation_id: UUIDv7
- user_id: UUIDv7
- book_id: UUIDv7
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
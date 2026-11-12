Сутності та атрибути

User
- user_id: UUIDv7 (PK)
- fullName: string
- email: string
- password_hash: string
- role: UserRole
- registered_at: timestamp

Book
- book_id: UUIDv7 (PK)
- author_id: UUIDv7 (FK)
- title: string
- author: string
- total_pages: number
- rental_price: decimal

BookCopy
- copy_id: UUIDv7 (PK)
- book_id: UUIDv7 (FK)
- condition: BookCopyCondition
- status: BookCopyStatus

Reservation
- reservation_id: UUIDv7 (PK)
- user_id: UUIDv7 (FK)
- copy_id: UUIDv7 (FK)
- reserved_at: timestamp
- expires_at: timestamp
- status: ReservationStatus

Delivery
- delivery_id: UUIDv7 (PK)
- reservation_id: UUIDv7 (FK)
- service: string
- branch_office: string
- tracking_number: string
- cost: decimal
- status: DeliveryStatus
- estimated_delivery_at: timestamp

Payment
- payment_id: UUIDv7 (PK)
- reservation_id: UUIDv7 (FK)
- amount: decimal
- method: PaymentMethod
- status: PaymentStatus
- external_transaction_id: string
- created_at: timestamp

Receipt
- receipt_id: UUIDv7 (PK)
- reservation_id: UUIDv7 (FK)
- payment_id: UUIDv7 (FK)
- user_id: UUIDv7 (FK)
- copy_id: UUIDv7 (FK)
- borrowed_at: timestamp
- due_date: timestamp

Review
- review_id: UUIDv7 (PK)
- user_id: UUIDv7 (FK)
- book_id: UUIDv7 (FK)
- rating: number
- comment: string
- created_at: timestamp


Доменні типи даних (Enums)

UserRole:
- "READER" - читач;
- "AUTHOR" - автор;
- "CASHIER" - працівник персоналу (касир).

BookCopyCondition:
- "NEW" - новий;
- "GOOD" - незначні пошкодження;
- "WORN" - помітні пошкодження;
- "DAMAGED" - пошкоджений (потребує ремонту або списання).

BookCopyStatus:
- "AVAILABLE" - на полиці;
- "RESERVED" - заброньований;
- "IN_USE" - виданий читачеві;
- "MAINTENANCE" - на реставрації.

ReservationStatus:
- "PENDING" - очікує обробки;
- "PAID" - оплачено (очікує видачі або доставки);
- "READY_FOR_PICKUP" - книга на полиці броні, чекає користувача;
- "FULFILLED" - читач прийшов і забрав;
- "EXPIRED" - час броні вийшов;
- "CANCELLED" - бронювання скасовано користувачем.

DeliveryStatus:
- "PENDING" - оформлено, очікує відправки;
- "IN_TRANSIT" - у дорозі;
- "DELIVERED" - доставлено у відділення або вручено читачеві;
- "CANCELLED" - доставку скасовано.

PaymentMethod:
- "ONLINE_GATEWAY" - онлайн-оплата через платіжний шлюз;
- "CASH" - оплата готівкою на фізичній касі;
- "POS_TERMINAL" - оплата карткою через POS-термінал.

PaymentStatus:
- "PENDING" - платіж ініційовано, очікує підтвердження;
- "AUTHORIZED" - оплату успішно авторизовано та підтверджено;
- "FAILED" - платіж відхилено;
- "REFUNDED" - кошти повернено користувачеві.


Зв'язки

1. User -додає- Book ( 1 : 0..M ):
- Один користувач із роллю Автора може додати нуль або багато видань книг ( 1 : 0..M )
- Одне видання книги додається одним і тільки одним Автором ( 1 : 1 )

2. User -створює- Reservation ( 1 : 0..M ):
- Один користувач може мати нуль або багато бронювань ( 1 : 0..M )
- Одне бронювання належить одному і тільки одному користувачу ( 1 : 1 )

3. BookCopy -бронюється в- Reservation ( 1 : 0..M ):
- Один фізичний примірник книги може бути заброньований нуль або багато разів ( 1 : 0..M )
- Одне бронювання стосується одного і тільки одного фізичного примірника книги ( 1 : 1 )

4. Book -складається з- BookCopy ( 1 : 0..M ):
- Одне видання книги може містити нуль або багато фізичних примірників ( 1 : 0..M )
- Один примірник належить одному і тільки одному виданню книги ( 1 : 1 )

5. Reservation -розширюється- Delivery ( 1 : 0..1 ):
- Одне бронювання може бути розширене нулем або одним оформленням доставки ( 1 : 0..1 )
- Одне оформлення доставки стосується одного і тільки одного бронювання ( 1 : 1 )

6. Reservation -оплачується через- Payment ( 1 : 0..M ):
- Одне бронювання може мати нуль або багато спроб або транзакцій оплати ( 1 : 0..M )
- Одна транзакція оплати належить одному і тільки одному бронюванню ( 1 : 1 )

7. Reservation -підтверджується- Receipt ( 1 : 0..1 ):
- Одне бронювання може бути підтверджене нулем або однією квитанцією на видачу ( 1 : 0..1 )
- Одна квитанція оформлюється на одне і тільки одне бронювання ( 1 : 1 )

8. Payment -формує- Receipt ( 1 : 0..1 ):
- Одна успішна транзакція оплати може сформувати нуль або одну квитанцію ( 1 : 0..1 )
- Одна квитанція формується на основі однієї і тільки однієї підтвердженої оплати ( 1 : 1 )

9. User -отримує- Receipt ( 1 : 0..M ):
- Один користувач може мати нуль або багато квитанцій на видачу книг ( 1 : 0..M )
- Одна квитанція оформлюється на одного і тільки одного користувача ( 1 : 1 )

10. BookCopy -видається через- Receipt ( 1 : 0..M ):
- Один примірник може фігурувати в нулі або багатьох квитанціях за весь час циркуляції ( 1 : 0..M )
- Одна квитанція фіксує видачу одного і тільки одного фізичного примірника ( 1 : 1 )

11. User -пише- Review ( 1 : 0..M ):
- Один користувач може написати нуль або багато відгуків ( 1 : 0..M )
- Один відгук створюється одним і тільки одним користувачем ( 1 : 1 )

12. Book -отримує- Review ( 1 : 0..M ):
- Одне видання книги може отримати нуль або багато відгуків ( 1 : 0..M )
- Один відгук стосується одного і тільки одного видання книги ( 1 : 1 )


Критерії прийняття

- Модель описується виключно декларативним синтаксисом (Mermaid erDiagram).
- Проміжні таблиці без власних атрибутів заборонені.
- Модель нормалізована до 3NF.
- Усі первинні та зовнішні ключі мають єдиний узгоджений тип - UUIDv7.
- Зв'язки мають точні кардинальності (1 : 0..1, 1 : 0..M).
- Поля ролей, статусів та стану книги (UserRole, BookCopyCondition, BookCopyStatus, ReservationStatus, DeliveryStatus, PaymentMethod, PaymentStatus) відповідають визначеним Enums.
- Усі часові мітки та дедлайни (створення, закінчення броні, доставка, видача, повернення) уніфіковані типом timestamp у форматі UTC.
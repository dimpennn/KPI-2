Сутності та атрибути

User
- user_id
- fullName
- email
- registered_at

Book
- book_id
- title
- authir
- total_pages

Review
- review_id
- user_id
- book_id
- rating
- comment
- created_at

Receipt
- receipt_id
- user_id
- book_id
- borrowed_at
- due_date

Reservation
- reservation_id
- user_id
- book_id
- reserved_at
- expires_at
- status
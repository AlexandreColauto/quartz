table that will hold all request for signing transactions, please don't confuse with [[transactions table]], that hold the token transfer history.

#refactor 
<details>
Update table names to avoid confusion.
</details>

This table uses of the Realtime feature of the database, that provides a subscription based framework to broadcast information to subscribed users, it also utilize the row level security that ensures only allowed users will recieve the messeges.

It has 7 columns:
- **id**: unique indentifier of the transaction.
- **created_at**: transaction timestamp.
- **payload**: transaction body.
- **status**: currently state (initiated or signed).
- **hash**: transaction hash for complete transactions.


> [!INFO]
> Note that the table doesn't have a user id column, it's because the table have a row level security, meaning that users will only be able to read and update their own records.

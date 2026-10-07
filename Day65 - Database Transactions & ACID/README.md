# Day 65 - Database Transactions & ACID

## What I Learned

Today I learned about **database transactions** and the **ACID properties** that help keep data reliable and consistent.

### Database Transactions

A transaction groups multiple related database operations into one unit of work.

For example, an order may require:

1. Create the order
2. Reduce product stock
3. Create a payment record

If all operations succeed, the transaction is committed.

If any operation fails, the transaction is rolled back so the changes made by that transaction are undone.

### Commit

`COMMIT` permanently saves the changes made by a successful transaction.

### Rollback

`ROLLBACK` / transaction abort undoes the changes made within the failed transaction.

### ACID Properties

#### Atomicity
All operations in a transaction succeed together, or all of them are undone.

**All or nothing.**

#### Consistency
A successful transaction takes the database from one valid state to another valid state.

#### Isolation
Concurrent transactions should not interfere with each other's work in an unsafe way.

#### Durability
Once a transaction is committed, its changes should persist even if the server crashes or restarts.

## Transaction Flow

```text
BEGIN
  ↓
Perform related operations
  ↓
Everything succeeds?
  ├── YES → COMMIT
  └── NO  → ROLLBACK
```

## MongoDB Transaction Concept

MongoDB transactions use a session to group related operations.

Conceptually:

```text
Start Session
     ↓
Start Transaction
     ↓
Create Order
     ↓
Update Stock
     ↓
Create Payment
     ↓
Commit Transaction
```

If an operation fails:

```text
Start Transaction
     ↓
Create Order       ✅
     ↓
Update Stock       ✅
     ↓
Create Payment     ❌
     ↓
Rollback
```

## Key Takeaway

A transaction groups related database operations so they either all succeed together or all get undone together, helping prevent inconsistent database states.

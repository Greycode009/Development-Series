# Day 66 - Database Isolation & Concurrency


## What I Learned

Today I learned about **database isolation levels and concurrency problems**. I explored how multiple transactions can interact with each other and the problems that can occur when transactions run concurrently.

### Concurrency Problems

When multiple transactions execute at the same time, they can interfere with each other and produce unexpected results.

The main problems we studied were:

### Dirty Read

A dirty read happens when one transaction reads data that another transaction has changed but **has not committed yet**.

```text
Transaction A:
Stock = 10 → 8
(Not committed)

Transaction B:
Reads Stock = 8

Transaction A:
ROLLBACK

Actual Stock = 10
```

Transaction B read data that was later rolled back.

### Non-Repeatable Read

A non-repeatable read occurs when a transaction reads the same data twice but gets different results because another transaction changed and committed the data between the two reads.

```text
Transaction A:
Reads Balance = 10,000

Transaction B:
Balance → 15,000
COMMIT

Transaction A:
Reads Balance again → 15,000
```

The same transaction received different values for the same data.

### Phantom Read

A phantom read occurs when a transaction executes the same query twice and new matching rows appear or disappear because another transaction inserted, updated, or deleted data.

```text
Transaction A:
SELECT products WHERE price < 1000
→ Product A, Product B

Transaction B:
Adds Product C
COMMIT

Transaction A:
Runs the same query again
→ Product A, Product B, Product C
```

The new matching row appears like a **phantom**.

## Database Isolation Levels

There are four standard isolation levels:

1. **Read Uncommitted**
2. **Read Committed**
3. **Repeatable Read**
4. **Serializable**

### Read Uncommitted

The weakest isolation level.

A transaction can read uncommitted changes made by another transaction.

```text
Dirty Read → Possible
Non-Repeatable Read → Possible
Phantom Read → Possible
```

### Read Committed

A transaction can only read committed data.

```text
Dirty Read → Prevented
Non-Repeatable Read → Possible
Phantom Read → Possible
```

### Repeatable Read

Ensures that repeated reads of the same data within a transaction remain consistent.

```text
Dirty Read → Prevented
Non-Repeatable Read → Prevented
```

Phantom-read behavior can depend on the database system and implementation.

### Serializable

The strongest standard isolation level.

Transactions behave more like they are executed one after another rather than concurrently.

It provides the strongest isolation but can reduce concurrency because transactions may need to wait or retry.

## Isolation Level Comparison

```text
Read Uncommitted
        ↓
Read Committed
        ↓
Repeatable Read
        ↓
Serializable

More Isolation → More Consistency
More Isolation → Potentially Less Concurrency
```

## Key Takeaway

Isolation levels control how transactions interact with each other when running concurrently. Stronger isolation prevents more concurrency problems but can reduce system concurrency.

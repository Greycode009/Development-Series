# Day 67 - Locking & Concurrency Control


## What I Learned

Today I learned how databases control concurrent transactions using locks and the Two-Phase Locking (2PL) protocol. I also explored how deadlocks happen and how consistent lock ordering can help prevent them.

### Shared and Exclusive Locks

- **Shared Lock (S):** Allows compatible read operations.
- **Exclusive Lock (X):** Used for writes and prevents conflicting access while held.

### Two-Phase Locking (2PL)

Two-Phase Locking is a concurrency-control protocol that ensures conflict serializability.

It has two phases:

#### Growing Phase

A transaction can acquire locks but cannot release any locks.

#### Shrinking Phase

A transaction can release locks but cannot acquire new locks.

```text
GROWING PHASE
  Acquire lock A
  Acquire lock B
       ↓
  Perform updates
       ↓
SHRINKING PHASE
  Release lock A
  Release lock B
```

Once a transaction releases its first lock, it cannot acquire another lock under basic 2PL.

### Deadlock

A deadlock occurs when transactions wait for locks held by each other, so neither can proceed.

```text
Transaction A:
Holds Account A
Waits for Account B

Transaction B:
Holds Account B
Waits for Account A
```

### Preventing Deadlocks

One simple technique is **consistent lock ordering**. Transactions acquire locks in the same order, such as Account A first and then Account B. This can prevent circular-wait deadlocks caused by inconsistent lock ordering.

Other approaches include detecting deadlocks and aborting one transaction.

## Key Takeaway

Locks help control concurrent access to data. 2PL separates lock acquisition and release into two phases, while consistent lock ordering can help prevent deadlocks.

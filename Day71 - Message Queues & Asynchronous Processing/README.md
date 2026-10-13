# Day 71 - Message Queues & Asynchronous Processing

Repository: https://github.com/Greycode009/Development-Series

## Overview

Message queues allow one part of an application to place tasks in a queue so another part can process them later. This separates task creation from task execution and helps slow background work avoid delaying user-facing requests.

## 1. The Problem

In an e-commerce application, placing an order may involve several tasks:

- Save the order.
- Process the payment.
- Send a confirmation email.
- Notify the seller.

If the backend waits for every task to finish before responding, slow operations—such as email delivery—can make the customer wait longer.

## 2. What Is a Message Queue?

A message queue stores tasks or messages until workers can process them.

A typical flow is:

1. The backend creates a task.
2. The task is placed in the queue.
3. A background worker receives the task.
4. The worker processes it.

This lets the backend separate background work from the main request. Tasks that determine whether an order or payment succeeded still need appropriate confirmation before the application reports success.

## 3. Background Workers

Workers process tasks from the queue independently of the request that created them. If many tasks arrive, they can wait in the queue until a worker is available.

## 4. Queue Growth and Worker Scaling

If tasks arrive faster than workers can process them, the queue grows. A large backlog can increase delays and consume resources.

Adding more workers can increase processing capacity, provided the downstream service can handle the extra work.

If tasks arrive at 100 per second and workers process 150 per second, the queue can shrink by roughly 50 tasks per second while those rates remain stable.

## 5. Backpressure

Backpressure controls how much work a system accepts or passes downstream when processing capacity is limited. It helps prevent an overloaded service or worker pool from being overwhelmed.

## 6. Acknowledgments and Retries

Queues commonly use acknowledgments to learn that a task has been processed. Depending on the queue's configuration, if a worker crashes before acknowledging a task, the task may become available for retry.

Retries help recover from failures, but they can also cause the same task to be processed more than once.

## 7. Idempotency and Duplicate Processing

A worker may complete an operation and then crash before acknowledging the message. The queue may deliver the task again.

Idempotency means repeated attempts for the same logical operation do not cause unwanted repeated effects. For example, a payment system can use an idempotency key or another deduplication mechanism to prevent a retry from charging a customer twice.

For email tasks, tracking processed task IDs or using a suitable downstream deduplication mechanism can help reduce duplicate sends. The details depend on the email provider and system design.

## Key Takeaways

- Message queues separate task creation from task processing.
- Background workers process queued tasks asynchronously.
- Worker scaling can increase processing capacity.
- Backpressure helps control work when capacity is limited.
- Acknowledgments and retries help handle worker failures.
- Idempotency and deduplication help prevent unwanted duplicate effects.

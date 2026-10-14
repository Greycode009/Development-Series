# Day 72 - Light Review: Reliable Background Processing


## Overview

Today was a light review of how background systems stay reliable when things go wrong. Queues, workers, and external services can all fail, slow down, or repeat work. The goal is to design systems that recover safely without causing duplicate or harmful side effects.

## 1. Temporary External-Service Failures

Background workers often depend on external services such as payment gateways, email providers, or third-party APIs. These services can fail temporarily due to:

- Network issues
- Service downtime
- Rate limits
- Slow responses under heavy load

A temporary failure does not always mean the task is invalid. Instead of discarding the task, the worker can retry it later. A message queue helps here because the task stays in the queue until it is processed successfully.

## 2. Why Workers May Process a Task More Than Once

Many queues guarantee that a task will be delivered **at least once**, not exactly once.

A common scenario:

1. The worker receives the task.
2. The worker completes the operation (for example, sends an email).
3. The worker crashes before acknowledging the task.
4. The queue assumes the task failed and delivers it again.

The operation already happened, but the queue doesn't know that. This is why workers must be designed to handle repeated tasks safely.

## 3. Idempotency and Deduplication

**Idempotency** means repeating the same logical operation produces the same result without unwanted extra effects.

**Deduplication** means detecting that a task has already been processed and skipping it.

Common approaches:

- Give each task a unique ID.
- Store processed task IDs and check them before processing.
- Use unique database constraints to block duplicate records.
- Check the current state before acting (for example, skip if the order is already marked as paid).

## 4. Timeouts and Controlled Retries

Slow external APIs can block workers if there is no limit on how long they wait.

**Timeouts** stop a worker from waiting forever. If the API doesn't respond within a set time, the request is treated as failed so the worker can move on.

**Controlled retries** prevent a failing service from being overwhelmed:

- Limit the maximum number of retry attempts.
- Wait longer between each retry (exponential backoff).
- Add small random delays (jitter) so many workers don't retry at the same moment.
- Stop retrying after the limit and record the task as failed for review.

Important: a timeout does not always mean the operation failed. The external service may have completed it but responded too slowly. This is another reason retries must be idempotent.

## 5. Backpressure

If tasks arrive faster than workers can process them, the queue keeps growing. Retries can make this worse by adding even more work.

Backpressure controls how much work is accepted or passed downstream when capacity is limited. Examples include:

- Limiting how many tasks each worker processes at once.
- Limiting queue size or slowing down task producers.
- Respecting the rate limits of external services.

This prevents uncontrolled task buildup and protects both the workers and the services they depend on.

## 6. Idempotency in Payment Integrations

Payments are where duplicate processing causes the most damage. A retried payment task without protection could charge a customer twice.

A common protection is an **idempotency key**:

1. The system generates a unique key for each payment attempt (for example, tied to the order ID).
2. The key is sent with the payment request.
3. If the request is retried with the same key, the payment provider recognizes it and returns the original result instead of charging again.

Many payment providers support idempotency keys, but the exact behavior depends on the provider. The application should also protect itself, for example by checking the order's payment status before processing and storing transaction IDs.

## Key Takeaways

- External services can fail temporarily, so tasks should be retried safely.
- Queues often deliver tasks at least once, so duplicates are possible.
- Idempotency and deduplication prevent unwanted repeated effects.
- Timeouts stop workers from waiting forever on slow APIs.
- Controlled retries with limits and backoff avoid overwhelming failing services.
- Backpressure prevents uncontrolled task buildup.
- Payment integrations need idempotency protection to prevent double charges.
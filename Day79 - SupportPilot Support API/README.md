# Day 79 — SupportPilot: AI-Assisted Support API

## Today's Points

- Started SupportPilot, an AI-assisted customer support platform for a small e-commerce store.
- Built an Express + MongoDB API with JWT auth, roles, and per-customer order access.
- Added an AI support agent that can only call four approved backend tools.
- Grounded AI answers in verified data from the database instead of the model's own claims.
- Built human handoff: escalation creates a ticket, and agents reply from a ticket queue.
- Built a React client with customer chat and an agent ticket queue.
- Moved auth to httpOnly cookies with rotating refresh tokens.
- Added Docker Compose, a CI workflow, and tests (Vitest + supertest).

## Learning Notes

- **Approved tools only:** The model can call `list_my_orders`, `get_order_details`, `get_payment_status`, and `escalate_to_human`. Any other tool is rejected, and none of them can move money or change an order.
- **Server decides data access:** Tools always run as the conversation's customer. Another customer's order returns the same "not found" as a missing one.
- **Verified data:** Each reply returns the exact records the tools read, so the UI shows real order and payment cards instead of trusting the reply text. Order numbers the model mentions that aren't on the account are flagged.
- **Human handoff:** While a conversation is escalated, the AI is not called, so it never talks over a human agent. Resolving the ticket hands the conversation back to the assistant.
- **Provider isolation:** Only one adapter file talks to the AI provider, and a mock provider lets the app and tests run without an API key.

## Key Takeaway

Integrating an LLM into a real product is mostly backend engineering: limiting what the model can do, controlling whose data it sees, and showing verified records instead of model claims. That is exactly the kind of work an FDE does for customers.

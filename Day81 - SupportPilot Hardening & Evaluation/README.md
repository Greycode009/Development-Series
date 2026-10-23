# Day 81 — SupportPilot: Hardening & Evaluation

## Today's Points

- Hardened the order-lookup tools against badly formed AI responses, with 21 more tests.
- Made a failed or malformed AI turn return a clean "assistant unavailable" error, with nothing from that turn saved.
- Reported the served model and token usage from the AI providers.
- Built an offline evaluation: 20 test conversations scored by three code checks.
- Drafted a live evaluation plan for when there is budget for real Claude calls.

## Learning Notes

- **Don't trust the model's output shape:** Every tool call is validated before it runs. If the model asks for something malformed, the request fails safely instead of reaching the database.
- **All or nothing per turn:** A turn that fails halfway saves nothing, so the conversation never contains half an answer.
- **Evaluate with code first:** The three checks are correct facts, no other customer's data, and escalating only when needed. Run against the free mock provider, they scored 75% / 100% / 89%. These numbers describe the mock, not Claude.
- **Cost awareness:** An LLM judge was planned but skipped because it costs money on every run; the code checks are free and repeatable.

## Project Status

- 127 server tests and 25 client tests pass.
- Not done yet: a real Claude call (waiting for budget), running the Docker images and CI, the LLM judge, real-time messages instead of 10-second polling, and shared rate limits for more than one server.

## Key Takeaway

An AI feature isn't finished when it works once. It needs validation for bad outputs, clean failure behaviour, and an evaluation you can run every time the code changes.

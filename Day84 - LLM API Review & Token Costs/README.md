# Day 84 — LLM API Review & Token Costs

Repository: https://github.com/Greycode009/Development-Series

## Today's Points

- Revised how applications connect to LLM APIs and practised by answering questions on yesterday's topic.
- Understood why API keys stay on the backend server and never in the client.
- Explored how applications send context to the LLM with each request.
- Learned how input and output tokens decide the API cost.
- Understood how to track token usage per customer for billing.

## Learning Notes

- **App to LLM flow:** The client talks to our backend, and the backend calls the LLM provider's API. The client never calls the provider directly.
- **API keys on the backend:** A key in frontend or mobile code can be extracted and misused, and every request would be billed to us. Keeping it on the server (in environment variables or a secrets manager) protects it and lets us add auth, rate limits and logging.
- **Providing context:** The model doesn't remember earlier requests. The app sends the needed context every time — system instructions, relevant data and recent conversation — so more context means more input tokens.
- **Token costs:** Providers charge per input and output token, usually with output tokens costing more. Shorter prompts, trimmed context and limited response length keep costs down.
- **Per-customer tracking:** The API response reports token usage. Saving it with the customer or tenant ID lets us show usage, set limits and bill each customer for what they use.

## Key Takeaway

A GenAI feature is also a cost centre. Keeping keys on the backend, sending only the context that's needed and tracking tokens per customer make the feature safe and affordable to run.

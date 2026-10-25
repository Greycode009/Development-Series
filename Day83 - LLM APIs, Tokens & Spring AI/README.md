# Day 83 — LLM APIs, Tokens & Spring AI

Repository: https://github.com/Greycode009/Development-Series

## Today's Points

- Finished FDE Full Course #3 — Integrating LLM with Your Application (Coder Army).
- Sent my first LLM request with Postman: endpoint, API key, model and input.
- Learned input vs output tokens and how token usage affects cost, latency and context.
- Connected a Spring Boot application to an LLM using Spring AI's ChatClient.
- Built a support-ticket summarizer API.
- Got introduced to System, User and Assistant roles.

## Learning Notes

- **ChatGPT is more than an LLM:** ChatGPT combines the model with tools, search, memory and other features. A GenAI application does the same — the LLM is one part, and the app adds APIs and functions around it.
- **An LLM is just an HTTP API:** The app sends a request to the provider's endpoint with an API key for authentication, the model name and the input. The response contains the generated text plus usage details.
- **Tokens:** Input tokens are what we send (prompt and context); output tokens are what the model generates. Token usage decides the cost, affects latency, and has to fit inside the model's context window.
- **Spring AI:** Instead of writing raw HTTP calls, Spring AI handles the request, authentication and response parsing. `ChatClient` gives a simple API for sending a prompt and reading the answer, and makes it easier to switch providers.
- **Support-ticket summarizer:** A backend endpoint takes a customer ticket, sends it to the LLM with instructions, and returns a short summary — a first real GenAI feature inside an API.
- **Message roles:** The System message sets the model's behaviour and rules, the User message is the request, and the Assistant message is the model's reply.

## Key Takeaway

Talking to an LLM is a normal API call with a cost measured in tokens. Frameworks like Spring AI hide the HTTP details, but understanding what happens underneath makes it easier to build and debug GenAI features.

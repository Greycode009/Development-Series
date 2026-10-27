# Day 85 — Chatbot Memory & Context Window

Repository: https://github.com/Greycode009/Development-Series

## Today's Points

- Started FDE Full Course #4 — Build Your First AI Chatbot (Coder Army).
- Learned that LLM API calls are stateless, so the model doesn't remember earlier messages.
- Built conversation history into the app so the chatbot can follow a conversation.
- Understood System, User and Assistant roles and how system prompts guide the model.
- Learned how ChatGPT-like memory works and what the context window is.

## Learning Notes

- **Stateless API calls:** Each request to the LLM is independent. If the app sends only the latest message, the model has no idea what was said before.
- **Conversation history:** The app stores the messages and sends the previous turns along with the new one. This is how a chatbot "remembers" — the memory lives in the application, not in the model.
- **Message roles:** The System message sets the rules and behaviour, User messages are what the person types, and Assistant messages are the model's earlier replies. System instructions sit at the top of the instruction hierarchy.
- **Context window:** The maximum number of tokens the model can read in one request. The system prompt, conversation history and new message all have to fit inside it.
- **History vs context window:** The app can store the full history, but only the part that fits in the context window can be sent to the model.

This was a partial session — I watched the first half of the video. Token usage in long conversations, context management, streaming and hallucinations are still to come.

## Key Takeaway

A chatbot's memory is built by the application, not the model. Sending the right history with clear roles, inside the limits of the context window, is what makes a conversation feel continuous.

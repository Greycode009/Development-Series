# Day 86 — Context Limits & Hallucinations

Repository: https://github.com/Greycode009/Development-Series

## Today's Points

- Finished FDE Full Course #4 — Build Your First AI Chatbot (Coder Army).
- Learned how token usage grows in long conversations and how apps manage context.
- Understood that prompts don't train the model — app memory is different from model training.
- Learned how streaming sends the reply token by token.
- Understood why LLMs hallucinate and how RAG, tools and validation reduce it.

## Learning Notes

- **Token usage in long chats:** Because the whole history is sent with every request, each new message costs more input tokens than the last. Long conversations get slower and more expensive.
- **Context management:** When the history gets too big, the app keeps only the most recent messages, summarizes older ones, or drops what isn't needed, so the request fits inside the context window.
- **Prompts are not training:** The model's weights don't change when we chat with it. Information in a prompt is only used for that one request. Remembering things is the application's job.
- **Streaming:** Instead of waiting for the full answer, the server sends tokens as they are generated. The total time is similar, but the user sees the reply start almost immediately.
- **Hallucinations:** An LLM predicts likely text, not verified facts, so it can sound confident while being wrong — especially when it lacks the right information.
- **Reducing hallucinations:** RAG gives the model real documents to answer from, tools let it fetch live data, and validation checks the output before it reaches the user.

## Quick Review — Full Video Summary

| Topic | In one line |
| --- | --- |
| Stateless API calls | Each LLM request is independent; the model remembers nothing by itself. |
| Conversation history | The app stores past messages and sends them with every new request. |
| Roles | System sets the rules, User is the person, Assistant is the model's earlier replies. |
| System prompt | The top-level instruction that shapes how the model behaves in every turn. |
| ChatGPT-like memory | "Memory" is built by the application, not stored inside the model. |
| Context window | The maximum tokens the model can read in one request — prompt, history and message together. |
| History vs context window | The app can save everything, but only what fits in the window is sent. |
| Tokens in long chats | Every turn resends the history, so cost and latency keep growing. |
| Context management | Keep recent messages, summarize older ones, drop what isn't needed. |
| Prompts vs training | Prompts give temporary information; they never change the model's weights. |
| Streaming | Tokens are sent as they are generated so the user sees the answer start quickly. |
| Hallucinations | The model generates plausible text, so it can be confidently wrong. |
| Reducing hallucinations | Ground answers with RAG, fetch real data with tools, and validate the output. |
| Real GenAI apps | LLM + app logic: history, context management, data sources, tools and checks. |

## Key Takeaway

A chatbot is mostly application engineering around a stateless model: the app manages memory and context, streams the answer for a better experience, and grounds and checks the output so users can trust it.

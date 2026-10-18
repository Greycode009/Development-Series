# Day 76 — How LLMs Work: Tokens, Attention & Transformers

Repository: https://github.com/Greycode009/Development-Series

## Today's Points

- Watched FDE Full Course #2 — How LLMs Actually Work (Coder Army).
- Learned how text is split into tokens and mapped to token IDs.
- Understood embeddings as vectors that capture meaning.
- Explored how attention helps each token focus on relevant context.
- Learned how Transformers generate text one token at a time.

## Learning Notes

- **Tokens:** LLMs don't read words directly. Text is broken into tokens (words or word pieces), and each token is converted into a number (token ID).
- **Embeddings:** Each token ID becomes a vector of numbers. Tokens with similar meanings end up with similar vectors.
- **Attention:** For every token, the model scores how relevant every other token is, so words like "it" can be linked to what they refer to.
- **Transformer blocks:** Attention and feed-forward layers are stacked many times, refining each token's understanding of the context layer by layer.
- **Generation:** The model predicts probabilities for the next token, picks one, appends it, and repeats until the answer is complete. The context window limits how many tokens it can consider at once.

## Key Takeaway

LLMs are next-token prediction engines built on tokens, embeddings, and attention. Knowing this explains practical limits like context windows, token costs, and hallucinations — important when designing AI solutions for customers as an FDE.

# Day 77 — Self-Attention: Q, K, V

Repository: https://github.com/Greycode009/Development-Series

## Today's Points

- Learned how LLMs process text using tokens.
- Reviewed next-token prediction.
- Understood how context helps interpret words.
- Learned how attention connects related tokens.
- Reviewed how Transformers improve parallel processing compared to RNNs.

## Learning Notes

- **Query (Q):** What a token is looking for in the rest of the sentence.
- **Key (K):** What each token offers, used to match against queries.
- **Value (V):** The information a token passes along once it is matched.
- **How it works:** Each token's query is compared with every token's key to get attention scores. The scores are turned into weights (softmax), and the token's new representation is the weighted sum of the values.
- **Why it matters:** Context changes meaning, and self-attention lets every token look at all other tokens at once — unlike RNNs, which read one word at a time.

## Key Takeaway

Self-attention is how a Transformer decides which words matter to each other. Understanding Q, K, and V makes it clearer how LLMs keep track of context in long prompts.

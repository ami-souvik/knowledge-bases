---
title: Attention Mechanism
type: concept
tags: [attention, transformer, QKV, scaled-dot-product, foundational]
created: 2026-04-15
updated: 2026-04-15
sources: [attention-is-all-you-need]
---

# Attention Mechanism

**Attention** is a mechanism that allows a model to dynamically weight how much each part of the input it should "focus on" when producing each part of the output. In the Transformer, it replaces recurrence entirely as the primary means of relating tokens to each other.

---

## How It Works

### Scaled Dot-Product Attention

```
Attention(Q, K, V) = softmax(QK^T / sqrt(d_k)) · V
```

- **Q (Queries)**: what we're looking for — a linear projection of the current token(s)
- **K (Keys)**: what each token offers — linear projections of all tokens
- **V (Values)**: what each token contains — linear projections of all tokens
- **sqrt(d_k) scaling**: prevents dot products from growing large → keeps softmax in a useful gradient regime

**Intuition**: For each query (token we want to enrich), compute how relevant each key (other token) is, turn into a probability distribution via softmax, then take a weighted sum of the values.

### Complexity

| | Time | Memory |
|---|---|---|
| Self-attention | O(n² · d) | O(n²) |
| RNN | O(n · d²) | O(d) |

Self-attention is quadratic in sequence length — a key scaling bottleneck for long contexts.

---

## Why It Matters

- **Direct token-to-token paths**: any token can attend to any other in O(1) steps (vs. O(n) for RNNs), enabling modeling of long-range dependencies.
- **Interpretable**: attention weights can be inspected as a rough proxy for "what the model is looking at" (though this interpretation is contested).
- **Foundation of the LLM era**: every major language model is built on top of attention.

---

## Variants & Related Techniques

- [[Multi-Head Attention]] — run multiple attention heads in parallel at different subspaces
- **Masked (Causal) Attention** — prevent tokens from attending to future positions (used in decoder-only models like GPT)
- **Cross-Attention** — Q comes from the decoder; K, V come from the encoder (bridges encoder and decoder)
- **Sparse Attention** — attend only to a subset of tokens to reduce O(n²) cost (Longformer, BigBird)
- **Flash Attention** — IO-aware exact attention implementation; same output, much faster (Dao et al., 2022)
- **Linear Attention** — approximates attention in O(n) time; various quality tradeoffs

---

## Key Papers / Sources

- [[Source: Attention Is All You Need]] — introduced Scaled Dot-Product and Multi-Head Attention

---

## Open Questions

- Do attention weights truly reveal "what the model attends to," or are they misleading?
- Can linear attention approximations match full attention quality at scale?
- How does attention interact with positional encoding to represent sequence order?

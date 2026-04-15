---
title: Multi-Head Attention
type: concept
tags: [attention, transformer, multi-head, architecture]
created: 2026-04-15
updated: 2026-04-15
sources: [attention-is-all-you-need]
---

# Multi-Head Attention

**Multi-Head Attention (MHA)** is the version of [[Attention Mechanism]] used in the [[Transformer]]. Rather than running a single attention function on the full d_model-dimensional input, it runs h parallel attention "heads" on lower-dimensional projections, then concatenates and re-projects the results.

---

## How It Works

For each head i (i = 1..h):
```
head_i = Attention(QW_i^Q, KW_i^K, VW_i^V)
```
Then:
```
MultiHead(Q, K, V) = Concat(head_1, ..., head_h) · W^O
```

**Original paper parameters:** h=8 heads, d_model=512 → d_k = d_v = 512/8 = 64 per head.

---

## Why Multiple Heads?

Different heads can specialize to attend to different kinds of relationships:
- One head might focus on syntactic dependency (subject ↔ verb)
- Another on coreference (pronoun ↔ antecedent)
- Another on proximity (adjacent tokens)

By projecting into lower-dimensional subspaces, each head gets its own "view" of the input, and the model learns which views are useful.

---

## Variants & Related Techniques

| Variant | Key Change |
|---------|-----------|
| Grouped Query Attention (GQA) | Multiple Q heads share a single K/V head — reduces KV cache size. Used in Llama 3, Gemma. |
| Multi-Query Attention (MQA) | All Q heads share one K/V pair — extreme KV cache reduction |
| Sliding Window Attention | Each head attends only within a local window |

- [[Attention Mechanism]] — the core computation each head performs
- [[Transformer]] — the architecture that uses MHA

---

## Key Papers / Sources

- [[Source: Attention Is All You Need]] — introduced MHA with h=8 heads

---

## Open Questions

- How many heads is optimal, and does it depend on model size?
- Do individual heads learn interpretable roles, or is specialization an artifact of analysis methods?

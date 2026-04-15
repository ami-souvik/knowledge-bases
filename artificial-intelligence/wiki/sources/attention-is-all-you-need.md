---
title: "Attention Is All You Need" (Vaswani et al., 2017)
type: source
tags: [transformer, attention, architecture, seminal-paper, NLP, encoder-decoder]
created: 2026-04-15
updated: 2026-04-15
source_url: https://arxiv.org/abs/1706.03762
source_file: raw/attention-is-all-you-need.md
author: Vaswani, Shazeer, Parmar, Uszkoreit, Jones, Gomez, Kaiser, Polosukhin (Google Brain / Google Research)
date_published: 2017-06-12
---

# "Attention Is All You Need" (Vaswani et al., 2017)

**Author(s):** Vaswani et al. (Google Brain / Google Research)  
**Published:** 2017-06-12 (NeurIPS 2017)  
**Source:** [raw file](../raw/attention-is-all-you-need.md) | [arXiv](https://arxiv.org/abs/1706.03762)

---

## Summary

The paper that introduced the **Transformer** architecture, replacing recurrent and convolutional networks with a mechanism based entirely on attention. Published in 2017, it is arguably the most consequential paper in the history of deep learning — almost every major AI system today descends from it. The key insight: attention allows every token in a sequence to directly "look at" every other token, enabling both massive parallelism during training and effective modeling of long-range dependencies.

---

## Key Takeaways

- **Recurrence is unnecessary.** Self-attention can model sequential relationships without processing tokens one-at-a-time, enabling GPU parallelism that fundamentally changed training economics.
- **Multi-head attention** lets the model simultaneously attend to different aspects of the input (e.g., syntactic relationships, semantic similarity) from multiple representation subspaces.
- **Scaling was the unlock.** The architecture's embarrassingly parallel compute profile made it uniquely suited to benefit from more hardware and data — the foundation of the scaling hypothesis that drove the LLM era.

---

## Concepts Introduced / Reinforced

- [[Transformer]] — the architecture proposed; encoder-decoder with stacked self-attention layers
- [[Attention Mechanism]] — specifically Scaled Dot-Product Attention: `softmax(QK^T / sqrt(d_k)) * V`
- [[Multi-Head Attention]] — h=8 parallel attention heads with reduced dimensionality, outputs concatenated and projected
- [[Positional Encoding]] — sine/cosine encodings added to embeddings to inject order information (no recurrence)
- [[Residual Connections]] — used around every sub-layer to enable deep stacking
- [[Layer Normalization]] — applied after residual addition in each sub-layer

---

## Entities Mentioned

- [[Ashish Vaswani]] — lead author; later founded Adept AI
- [[Noam Shazeer]] — co-author; later co-founded Character.AI; contributed key architectural ideas
- [[Google Brain]] — research division where the work originated
- [[WMT 2014]] (benchmark) — translation dataset used to evaluate; Transformer set new BLEU records

---

## Notable Quotes

> "We propose a new simple network architecture, the Transformer, based solely on attention mechanisms, dispensing with recurrence and convolutions entirely."

> "Attention mechanisms allow modeling of dependencies without regard to their distance in the input or output sequences."

---

## My Notes

This is the foundational paper for the entire current AI landscape. GPT, BERT, T5, Claude, Gemini, Llama — all are Transformer variants. The paper's impact was not fully appreciated at the time; it was originally motivated by machine translation, not general-purpose language modeling. The leap to decoder-only language models (GPT) came one year later. Key thing to track as more sources come in: how did the design choices here (number of heads, d_model, positional encoding type) evolve in subsequent models?

---

## Related Pages

- [[Transformer]]
- [[Attention Mechanism]]
- [[Multi-Head Attention]]
- [[Ashish Vaswani]]
- [[Noam Shazeer]]
- [[Google Brain]]

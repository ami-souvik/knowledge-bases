---
title: Transformer
type: concept
tags: [architecture, transformer, encoder-decoder, attention, foundational]
created: 2026-04-15
updated: 2026-04-15
sources: [attention-is-all-you-need]
---

# Transformer

The **Transformer** is a neural network architecture introduced in [[Source: Attention Is All You Need]] (Vaswani et al., 2017) that processes sequences using [[Attention Mechanism|attention]] instead of recurrence or convolutions. It is the foundation of virtually every major language model in use today.

---

## How It Works

The original Transformer is an **encoder-decoder** architecture:

**Encoder** (N=6 stacked layers):
1. Multi-head self-attention sub-layer
2. Position-wise feed-forward sub-layer
3. Residual connection + layer normalization after each sub-layer

**Decoder** (N=6 stacked layers):
1. Masked multi-head self-attention (prevents attending to future tokens)
2. Multi-head cross-attention over encoder output
3. Position-wise feed-forward
4. Residual + layer norm after each

**Key hyperparameters (original paper):** d_model=512, h=8 heads, d_ff=2048, N=6 layers.

---

## Why It Matters

1. **Parallelism**: No sequential dependency → tokens processed simultaneously → order-of-magnitude training speedup over RNNs.
2. **Long-range dependencies**: O(1) maximum path length between any two positions (vs. O(n) for RNNs).
3. **Scalability**: Performance scales predictably with compute → unlocked the LLM era and the scaling hypothesis.
4. **Generality**: Originally designed for translation; adapted to virtually every modality (text, image, audio, code, protein structure).

---

## Variants & Related Techniques

| Variant | Key Change | Example Models |
|---------|-----------|----------------|
| Encoder-only | No decoder; bidirectional attention | BERT, RoBERTa |
| Decoder-only | No encoder; causal (masked) attention | GPT series, Llama, Claude |
| Encoder-decoder | Both; cross-attention bridge | T5, BART, original Transformer |
| Sparse attention | Not all tokens attend to all others | Longformer, BigBird |
| Cross-attention / Perceiver | Asymmetric query-key separation | Flamingo, Perceiver |

- [[Attention Mechanism]] — the core operation
- [[Multi-Head Attention]] — the parallelized version used in Transformers
- [[Positional Encoding]] — how order is injected without recurrence

---

## Key Papers / Sources

- [[Source: Attention Is All You Need]] — original proposal; encoder-decoder for translation

---

## Open Questions

- What are the theoretical limits of the attention-based approach vs. state-space models?
- How does the choice of positional encoding (sinusoidal vs. RoPE vs. ALiBi) affect long-context performance?
- Will Transformers be displaced by architectures like [[SSM|Mamba]] for certain tasks?

---

## Timeline

| Date | Event |
|------|-------|
| 2017-06 | Original Transformer paper (Vaswani et al.) |
| 2018-06 | GPT-1: decoder-only Transformer for language modeling (OpenAI) |
| 2018-10 | BERT: encoder-only Transformer for NLP tasks (Google) |
| 2020-05 | GPT-3: scaling decoder-only to 175B parameters |
| 2022+ | Transformer becomes dominant architecture across all modalities |

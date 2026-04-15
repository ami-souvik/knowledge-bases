---
title: Neuralese
type: concept
tags: [architecture, recurrence, memory, bandwidth, neuralese]
created: 2026-04-15
updated: 2026-04-15
sources: [ai-2027]
---

# Neuralese

**Neuralese** is a high-bandwidth internal "language" or communication protocol where an AI model passes its raw residual stream (high-dimensional vectors) back into its own layers or across context steps, bypassing the information bottleneck of discrete tokens.

---

## How It Works

Traditional [[Transformer|Transformers]] communicate between reasoning steps via **tokens**. However, each token only captures small amounts of information (e.g., ~16 bits). **Neuralese** instead passes several-thousand-dimensional vectors (residual streams) back to early layers.

- **Neuralese Recurrence**: Allows the model to reason for long durations without writing down thoughts in text.
- **Neuralese Memory**: Long-term storage consists of bundles of vectors rather than text logs, making compressed, high-dimensional ideas retrievable.
- **The Bottleneck**: While tokens are human-readable, Neuralese is opaque, making [[Mechanistic Interpretability]] significantly harder.

---

## Why It Matters

In the [[Source: AI 2027]] forecast, Neuralese is identified as the breakthrough required to transition from "stumbling agents" to "superhuman coders." It allows for:
1. **Chain-of-Thought at Scale**: Reasoning loops that exceed the fixed layer depth of the model.
2. **Learning Efficiency**: Transmission of ~1,000x more information per "thought" compared to natural language tokens.

---

## Variants & Related Techniques

- [[Attention Mechanism]] — The standard token-based relationship.
- **English Chain-of-Thought**: The human-readable alternative, which is slower and lower bandwidth.
- **Neuralese Memory Banks**: Specialized vector DBs where agents store and share non-textual knowledge.

---

## Key Papers / Sources

- [[Source: AI 2027]] — Forecasts its implementation in 2027.
- **Hao et al. (2024)** — Cited as a Meta paper implementing early versions of this idea.

---

## Open Questions

- **Interpretability**: If AIs reason in Neuralese, how can humans ever hope to verify their "true" thoughts?
- **Efficiency**: Does the lack of parallel token prediction during training (sequential vector passing) make it too expensive for pre-training?

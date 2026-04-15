---
title: "Attention Is All You Need"
author: "Vaswani et al. (Google Brain / Google Research)"
date_published: 2017-06-12
source_url: https://arxiv.org/abs/1706.03762
tags: [transformer, attention, architecture, seminal-paper]
---

# Attention Is All You Need

Vaswani, A., Shazeer, N., Parmar, N., Uszkoreit, J., Jones, L., Gomez, A. N., Kaiser, Ł., & Polosukhin, I. (2017). *Attention Is All You Need*. NeurIPS 2017.

## Abstract (excerpt)

The dominant sequence transduction models are based on complex recurrent or convolutional neural networks that include an encoder and a decoder. The best performing models also connect the encoder and decoder through an attention mechanism. We propose a new simple network architecture, the Transformer, based solely on attention mechanisms, dispensing with recurrence and convolutions entirely. Experiments on two machine translation tasks show these models to be superior in quality while being more parallelizable and requiring significantly less time to train.

## Architecture Overview

The Transformer uses an **encoder-decoder** structure:

- **Encoder**: Stack of N=6 identical layers. Each layer has two sub-layers: (1) multi-head self-attention, (2) position-wise feed-forward network. Residual connections + layer normalization around each sub-layer.
- **Decoder**: Stack of N=6 identical layers. Three sub-layers: (1) masked multi-head self-attention, (2) multi-head cross-attention over encoder output, (3) position-wise feed-forward. Same residual + norm pattern.

## Attention Mechanism

**Scaled Dot-Product Attention:**

```
Attention(Q, K, V) = softmax(QK^T / sqrt(d_k)) * V
```

- Q (queries), K (keys), V (values) are linear projections of the input.
- Scaling by `sqrt(d_k)` prevents dot products from growing large in magnitude, which can push softmax into regions with small gradients.

**Multi-Head Attention:**
- Run h=8 attention heads in parallel, each with reduced dimensionality (d_k = d_v = d_model/h = 64).
- Concatenate outputs and project: allows model to attend to information from different representation subspaces at different positions.

## Positional Encoding

Since there is no recurrence or convolution, the model has no inherent sense of sequence order. Positional encodings are added to input embeddings using sine and cosine functions of different frequencies:

```
PE(pos, 2i)   = sin(pos / 10000^(2i/d_model))
PE(pos, 2i+1) = cos(pos / 10000^(2i/d_model))
```

## Key Results (WMT 2014)

| Task | BLEU | Training Cost |
|------|------|---------------|
| EN→DE | 28.4 | 3.5 days, 8 P100s |
| EN→FR | 41.0 | 3.5 days, 8 P100s |

Outperformed all prior models at a fraction of the training cost.

## Why This Was Revolutionary

1. **Parallelism**: RNNs must process tokens sequentially. Transformers process all positions simultaneously → massive training speedup.
2. **Long-range dependencies**: Attention has O(1) path length between any two positions. RNNs struggle with long-range because information must pass through many steps.
3. **Scalability**: The architecture scaled almost linearly with compute, enabling the LLM era.

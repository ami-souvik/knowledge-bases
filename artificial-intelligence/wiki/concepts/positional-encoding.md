---
title: Positional Encoding
type: concept
tags: [transformer, positional-encoding, sequence-order, architecture]
created: 2026-04-15
updated: 2026-04-15
sources: [attention-is-all-you-need]
---

# Positional Encoding

Since [[Transformer|Transformers]] have no recurrence or convolution, they are **permutation-invariant** by default — they would treat "dog bites man" and "man bites dog" identically without some mechanism to inject sequence order. **Positional encodings** solve this by adding order information directly to the token embeddings.

---

## How It Works

### Sinusoidal (Original Paper)

```
PE(pos, 2i)   = sin(pos / 10000^(2i/d_model))
PE(pos, 2i+1) = cos(pos / 10000^(2i/d_model))
```

- `pos` = token position in sequence
- `i` = dimension index
- Different frequencies for different dimensions → each position gets a unique fingerprint
- **Advantage**: generalizes to sequence lengths not seen during training; no learned parameters

Added to (not concatenated with) the token embedding before entering the encoder/decoder.

---

## Why It Matters

Without positional encoding, a Transformer cannot distinguish position, making it unsuitable for any task where order matters (which is almost everything in language).

---

## Variants & Related Techniques

| Method | Description | Used In |
|--------|-------------|---------|
| Sinusoidal (absolute) | Fixed formula, no parameters | Original Transformer |
| Learned absolute | Learnable embedding per position | BERT, GPT-2 |
| Relative PE | Encode distance between tokens, not absolute position | Transformer-XL, T5 |
| RoPE (Rotary PE) | Rotate Q and K vectors by position; relative by construction | Llama, Gemma, Mistral |
| ALiBi | Add linear bias to attention scores based on distance | MPT, BLOOM |
| NoPE | No positional encoding; model infers order implicitly | Some recent work |

**RoPE** has become the dominant approach in modern LLMs (2023–2025) due to its strong extrapolation to longer contexts.

---

## Key Papers / Sources

- [[Source: Attention Is All You Need]] — introduced sinusoidal positional encoding

---

## Open Questions

- Can models learn positional information implicitly (without explicit PE) at sufficient scale?
- How do different PE schemes compare for very long contexts (100k+ tokens)?
- Does PE approach affect in-context learning ability?

---
title: IDA (Iterated Distillation and Amplification)
type: concept
tags: [self-improvement, training, distillation, alignment, takeoff]
created: 2026-04-15
updated: 2026-04-15
sources: [ai-2027]
---

# IDA (Iterated Distillation and Amplification)

**Iterated Distillation and Amplification (IDA)** is a framework for scaling AI capabilities and alignment by building a powerful system out of many weaker parts, then training a single model to imitate that powerful aggregate.

---

## How It Works

1. **Amplification**: Take a model $M_0$ and increase its power by spending more compute (e.g., let it think longer, run many copies in parallel, use tools). Call this system $Amp(M_0)$.
2. **Distillation**: Train a new, smaller/faster model $M_1$ to imitate the outputs and reasoning of $Amp(M_1)$. 
3. **Loop**: Repeat the process so $M_n$ becomes the starting point for the next amplification.

**Example**: AlphaGo used Monte-Carlo Tree Search (MCTS) as the *amplification* step and Reinforcement Learning as the *distillation* step to achieve superhuman Go performance.

---

## Why It Matters

IDA is the engine of the **Intelligence Explosion**. In [[Source: AI 2027]], it is the mechanism by which Agent-3 transitions to Agent-4:
- Allows models to solve tasks they couldn't solve in a single forward pass.
- Bypasses the need for human-labeled data by using the AI's "amplified" self to create the training signal.

---

## Key Papers / Sources

- **Christiano et al. (2018)** — Initial proposal for aligning systems by decompositions.
- [[Source: AI 2027]] — Highlights its role in self-improving AI research in early 2027.

---

## Open Questions

- **Error Propagation**: Does distillation eventually amplify the subtle errors of the predecessor?
- **Alignment Stability**: If $M_0$ is aligned, is $Amp(M_0)$ necessarily aligned? And will the distilled $M_1$ retain that alignment?

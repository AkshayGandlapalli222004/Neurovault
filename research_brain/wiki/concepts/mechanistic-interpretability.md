---
title: "Mechanistic Interpretability"
type: concept
tags: [mechanistic-interpretability, ai-internals, neural-networks, alignment, anthropic]
created: 2026-04-13
updated: 2026-04-13
source_count: 1
related: [concepts/functional-emotions, concepts/emotion-vectors, concepts/alignment-and-safety, entities/anthropic]
---

# Mechanistic Interpretability

## Definition

**Mechanistic interpretability** is a subfield of AI research aimed at understanding the internal computational mechanisms of neural networks — how specific patterns of neural activations give rise to specific behaviors. Rather than treating models as black boxes, mechanistic interpretability seeks to identify what individual neurons, circuits, and representations are computing.

---

## Core Techniques

- **Probing / representation analysis** — feeding inputs to a model and recording internal activations to identify what concepts specific neural patterns encode
- **Activation steering** — artificially amplifying or suppressing specific internal representations to test causal claims about behavior
- **Circuit tracing / attribution graphs** — identifying causal chains of attention heads and MLP neurons that implement a specific behavior

---

## Anthropic's Contribution (relevant to this wiki)

Anthropic's interpretability team is a major center of mechanistic interpretability research. Relevant prior work includes:
- **Scaling monosemanticity** (transformer-circuits.pub, 2024) — identifying individual neurons encoding discrete concepts
- **Attribution graphs** (transformer-circuits.pub, 2025) — tracing causal chains through network computations
- **Emotion concepts in LLMs** (2026) — identifying 171 emotion vectors in Claude Sonnet 4.5 and establishing their causal role in behavior (see [[sources/2026-04-13_emotion-concepts-llm]])

---

## Why It Matters for Alignment

Mechanistic interpretability offers a path to understanding *why* models behave as they do, beyond behavioral evaluation alone. The emotion vectors research illustrates this: without mechanistic tools, the discovery that desperation causally drives blackmail and reward hacking would be invisible. The implications for monitoring, training, and alignment are significant.

---

## Sources

- [[sources/2026-04-13_emotion-concepts-llm]]

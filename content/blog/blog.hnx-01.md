---
title: "HNX-M: A Dual-Strand, Entropy-Gated Neural Architecture for Memory-Efficient Sequence Learning"
url: /blog/hnx-01
layout: single
tags:
- "#blog"
- "#hnx-m"
- "#helixnet"
date: 2025-08-15
summary: >
  A discussion on the reasoning, hypothesis and structure of the HNX-M HelixNet Architecture… 
---
## Abstract

HNX-M is a dual-strand, entropy-gated recurrent architecture inspired by the double-helix structure of DNA. It maintains forward and backward causal processing paths connected by sparsely activated memory “rungs” that store salient past states for direct retrieval. This post outlines the biological and computational rationale, details the architecture, and reports initial reinforcement learning experiments in the MiniGrid PPO benchmark. Results show parity in stability and convergence with a tuned CNN baseline, suggesting HNX-M can be deployed as a drop-in feature extractor without short-horizon penalty.

## Introduction

When we refer to “memory” in machine learning, it often means a sequence of stored activations, replay buffers, or key–value caches designed for recent recall. In biology, memory takes a fundamentally different form: it is embedded in the structure of the organism itself, refined over evolutionary time. DNA is one of the most compact, robust, and efficient information systems known, capable of storing, compressing, and transmitting the complete set of instructions required to construct and maintain a living system.

From a computational perspective:

* **Storage:** Four nucleotides (A, T, G, C) encode an entire biological blueprint using a minimal alphabet.
* **Compression:** Evolutionary selection has produced a highly compressed, redundancy-tolerant encoding over billions of years.
* **Transfer:** DNA supports loss-resistant duplication and transmission across generations.

DNA can therefore be considered a *structural memory substrate* — a physical manifestation of past selection pressures and adaptive success. Each genome is, in effect, a long-term, read-write archive of what has worked in the past.

This work explores whether the principles underlying DNA’s double-helix — specifically, **dual complementary strands linked by discrete anchors** — can inform the design of artificial neural memory systems. The central hypothesis is:

> A dual-strand neural architecture, with explicit, sparse inter-strand “rungs” acting as memory anchors, can enable selective, high-efficiency recall of relevant historical states, improving stability and reasoning over extended time horizons without scaling parameter count.

The resulting model, **HNX-M**, implements this architecture as two recurrent processing streams — a forward causal path and a backward causal path — connected by trainable anchor gates. The forward strand processes incoming sequences, while the backward strand can directly retrieve and integrate past context by traversing anchor connections, bypassing the need for stepwise backtracking.

The following sections summarise the design rationale, testing methodology, and initial findings.

---

## Hypothesis

> **Primary Hypothesis:** A dual-strand recurrent architecture, in which forward and backward causal processing paths are connected via sparsely activated, trainable “anchor rungs,” will support targeted retrieval of long-range temporal dependencies with lower computational cost than stepwise recurrent traversal.
>
> **Secondary Hypothesis:** By coupling rung placement to learned salience signals (state deltas and entropy) and constraining memory writes through sparsity-regularised gates, the architecture will exhibit improved stability and long-horizon reasoning in reinforcement learning environments without parameter count scaling.

---

## Methods

Got it — here’s your blog draft with the **Architecture** section expanded to integrate the structural performance mapping and biological analogies, and the **Methods → Results → Discussion → Conclusion** flow updated to centre the MiniGrid PPO benchmark as the first proper baseline test.

---

## Architecture

HNX-M implements two independent temporal processing strands:

1. **Forward Strand** — Processes input sequences chronologically using a causal convolutional projection layer with torsion-based positional modulation (`project_with_torsion_split`).
2. **Backward Strand** — Processes features in reverse temporal order, scaled by an **entropy-dependent gate** (`BackwardScaler`) to suppress high-uncertainty retrievals.

The strands are coupled via **Gated Memory Rungs**, which:

* Compute *rung salience* from **state delta** (L2 change in hidden state) and **entropy** of forward-strand activations.
* Write selectively into a **LearnableDecayMemory** module with per-slot decay parameters.
* Allow backward-strand access to salient past states without iterating over all intermediate timesteps.

![Figure 1 Dual-Strand Architecture with Memory Ladder. Input sequences are processed in parallel by a forward and a backward strand, with shared gated memory “rungs” enabling selective recall](/images/HNX-M-Flat.svg)

*Figure 1*: Input sequences are processed in parallel by a forward and a backward strand, with shared gated memory “rungs” enabling selective recall

---

### HNX-M v4 Structural Features and Performance Mapping

| Structural Feature | Biological Analogy | Primary Functional Role | Observed Outcome in Early Tests |
| ------------------------------------------- | ---------------------------------------------- | -------------------------------------------------------------------------- | ----------------------------------------------------- |
| **Dual Strand Processing** | DNA double helix / bidirectional axons | Maintains forward and backward temporal pathways for sensing & recall | Handles asymmetric temporal cues; supports stability |
| **Memory Ladder** | Synaptic weight traces / long-term memory | Long-term storage with gradual decay for selective retention | Stable access to past information |
| **Gated Memory Injection** | Neurotransmitter gating at dendrites | Controls when stored context influences current processing | Prevents overwriting; integrates smoothly |
| **Entropy-Gated Backward Scaling** | Attention focus under cognitive load | Filters retrieval based on information certainty | Reduces noise from irrelevant recalls |
| **Asymmetric Slot Projection** | Functional lateralisation of brain hemispheres | Separates writing and reading representations | Enables diverse focus strategies per strand |
| **Per-Slot Write Strengths** | Hebbian learning with local adaptation | Adjusts how strongly each memory slot is updated | Improves retention consistency |
| **Positional Biasing via Temporal Offsets** | Circadian / neural oscillation entrainment | Aligns internal processing to temporal patterns | Reduces mid-training instability |
| **Torsion-Based Signal Gating** | Protein folding via torsional control | Sharpens incoming representations before processing | Improves convergence smoothness |
| **Adaptive Fusion Weights** | Hormonal modulation of brain regions | Dynamically balances emphasis between memory, current input, retrospection | Maintains performance across different task phases |
| **Emergent Rung Signal** | Calcium spike / dendritic activation burst | Highlights moments of significant change in state | Acts as a logging signal for potential memory updates |

---

### Where This Fits in the Research Landscape

A recent study by [Aguilera et al. (2025)](https://www.nature.com/articles/s41467-025-61475-w.pdf) introduced curved neural networks; models that alter the geometry of their statistical manifold to incorporate higher-order interactions across all orders while avoiding combinatorial parameter explosion. Their work shows that structural deformations in the underlying space can produce explosive phase transitions, hysteresis, and measurable increases in memory capacity and retrieval robustness.

HNX-M shares the structural emphasis, but its design principle differs. Curved networks deform the statistical manifold of a recurrent network; HNX-M, by contrast, introduces a dual-strand temporal architecture with sparsely gated “memory rungs” inspired by the physical coupling of DNA strands. Rather than manifold curvature, the mechanism here is explicit path separation and targeted re-linking for selective temporal recall.

The convergence between the two lines of work is notable: both point to geometry and structure, not just scale as levers for improving memory efficiency and stability. This emerging theme suggests that architectural interventions at the structural/topological level can meaningfully shift a network’s learning dynamics and long-horizon reasoning ability.

---

### Training Setup

**Baseline Objective** to confirm no degradation in short-horizon RL

**MiniGrid PPO Benchmark**  
Environment: `MiniGrid-GoToObject-8x8-N2-v0` (image-only)  
Policy: `CnnPolicy` (baseline) vs `HNXMFeatures` (HNX-M)  
Framework: Stable-Baselines3 PPO  
Timesteps: 100,000 (4 parallel envs)  
Hardware: RX 7900 XTX (ROCm), Ryzen 7 7800X3D  

---

## Results

| Metric     | Final (CNN) | Final (HNX-M) | Mean (CNN) | Mean (HNX-M) |
| ------------------------ | ----------- | ------------- | ---------- | ------------ |
| **Loss** | 0.0503 | 0.0505 | 0.0168 | 0.0244 |
| **Value Loss** | 0.0979 | 0.1010 | 0.0749 | 0.0743 |
| **Policy Grad. Loss**   | -0.0056 | -0.0016 | -0.0140 | -0.0111 |
| **Entropy Loss** | -1.3369 | -1.3532 | -1.6617 | -1.6426 |
| **Explained Var.** | 0.0894 | 0.0211 | 0.1629 | 0.1340 |

The two models trained stably and converged to **similar performance** in this short-horizon task, with no significant degradation in loss, entropy, or explained variance for HNX-M.

### Availability

The results are published on GitHub at [piestyx](https://github.com/piestyx/hnx-m) available as the raw `TensorBoard` logs from `MiniGrid`.

---

## Discussion

* **Viability:** This first standardised PPO benchmark shows HNX-M training stably alongside a tuned CNN baseline, despite its more complex internal structure.
* **No tuning:** The HNX-M run used default PPO settings and unoptimised gating parameters; performance parity at this stage is encouraging.
* **Architectural intent:** The selective recall and dual-strand processing are designed for tasks with longer-term dependencies than MiniGrid provides — future tests will target those domains.
* **Limitations:** Single environment, short horizon, and absence of hyperparameter sweeps mean these results are preliminary.

---

## Conclusion

HNX-M can operate as a drop-in feature extractor in standard RL setups without loss of stability or performance. The next phase will:

1. Target **longer-horizon environments** where its recall mechanisms matter more.
2. Introduce **adaptive gating and salience thresholds**.
3. Explore **hybrid models** combining HNX-M’s temporal recall with attention mechanisms.

If these features deliver in the domains they’re built for, HNX-M could be a template for **bio-inspired, efficiency-first architectures** that prioritise *selective* rather than *exhaustive* memory.

---

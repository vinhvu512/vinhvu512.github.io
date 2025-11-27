---
layout: page
title: Semi-MoE
description: Mixture of Experts for Semi-Supervised Histopathology Segmentation
img: assets/img/semi_moe.jpg
importance: 1
category: research
related_publications: true
---

<div class="row">
    <div class="col-sm-12">
        <p class="text-muted">
            <strong>Affiliation:</strong> <a href="https://xulabs.github.io/">Xu Lab, Carnegie Mellon University</a> &nbsp;|&nbsp;
            <strong>Advisor:</strong> <a href="https://xulabs.github.io/min-xu/">Prof. Min Xu</a> &nbsp;|&nbsp;
            <strong>Venue:</strong> BMVC 2025
        </p>
    </div>
</div>

---

## The Challenge

Standard semi-supervised learning methods assume that labeled and unlabeled data share the same underlying distribution. However, in real-world histopathology analysis, this assumption frequently fails: tissue samples exhibit significant **distribution shifts** arising from variations in staining protocols, scanner hardware, and tissue preparation across different laboratories. This creates what we term the **homogeneity problem**—where conventional pseudo-labeling approaches produce unreliable supervision for out-of-distribution unlabeled samples, leading to degraded segmentation performance and poor generalization.

---

## The Method

We propose **Semi-MoE**, a novel Mixture-of-Experts framework specifically designed to handle distribution heterogeneity in semi-supervised medical image segmentation.

<div class="row justify-content-sm-center">
    <div class="col-sm-10 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/semi_moe.jpg" title="Figure 1: The proposed Semi-MoE architecture handling distribution shifts." class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    <strong>Figure 1:</strong> The proposed Semi-MoE architecture handling distribution shifts. Different experts specialize in distinct data sub-domains, with a learnable gating network dynamically routing each input to the appropriate expert.
</div>

### Technical Architecture

The core innovation lies in our **dynamic expert specialization**:

1. **Expert Network Pool**: We instantiate $$K$$ parallel expert networks $$\{E_1, E_2, ..., E_K\}$$, each with identical architecture but independent parameters. During training, each expert naturally specializes in a subset of the data distribution.

2. **Learnable Gating Mechanism**: A gating network $$G(\cdot)$$ takes input features and produces a soft assignment over experts:

$$
\mathbf{g} = \text{softmax}(G(\mathbf{x})) \in \mathbb{R}^K
$$

The final prediction is computed as a weighted combination: $$\hat{y} = \sum_{k=1}^{K} g_k \cdot E_k(\mathbf{x})$$

3. **Diversity Regularization**: To prevent mode collapse (all inputs routed to a single expert), we introduce an entropy-based load balancing loss:

$$
\mathcal{L}_{\text{balance}} = -\sum_{k=1}^{K} \bar{g}_k \log(\bar{g}_k)
$$

where $$\bar{g}_k$$ is the average gate value for expert $$k$$ over a batch.

### Semi-Supervised Training Strategy

For unlabeled data, we employ **cross-expert consistency regularization**: predictions from different experts on the same input should agree, encouraging robust representations that generalize across distribution shifts.

---

## Key Results

| Metric | Baseline | Semi-MoE | Improvement |
|--------|----------|----------|-------------|
| Dice Score (5% labels) | 71.2% | **76.8%** | +5.6% |
| Dice Score (10% labels) | 74.5% | **79.3%** | +4.8% |
| Cross-domain Generalization | 62.1% | **70.4%** | +8.3% |

Our method demonstrates **state-of-the-art performance** on multiple histopathology benchmarks, with particularly strong gains in cross-domain generalization scenarios.

---

## Impact

Semi-MoE provides a principled solution to a fundamental limitation in semi-supervised learning for medical imaging. By explicitly modeling distribution heterogeneity through specialized experts, we enable robust learning from diverse unlabeled data sources—a critical capability for deploying AI systems across multiple clinical sites with varying protocols.

---

## Publication

This work was accepted at **BMVC 2025**. [Paper PDF](#) | [Code](#)

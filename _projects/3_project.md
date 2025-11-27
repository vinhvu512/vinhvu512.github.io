---
layout: page
title: SemiSAM
description: Foundation Model-Driven Co-Training for Medical Image Segmentation
img: assets/img/semisam.jpg
importance: 3
category: research
---

<div class="row">
    <div class="col-sm-12">
        <p class="text-muted">
            <strong>Role:</strong> <span class="badge bg-primary">Project Lead</span> &nbsp;|&nbsp;
            <strong>Affiliation:</strong> <a href="https://xulabs.github.io/">Xu Lab, Carnegie Mellon University</a> &nbsp;|&nbsp;
            <strong>Advisor:</strong> <a href="https://xulabs.github.io/min-xu/">Prof. Min Xu</a>
        </p>
    </div>
</div>

---

## The Challenge

The **Segment Anything Model (SAM)** represents a paradigm shift in computer vision—a foundation model trained on over 1 billion masks that demonstrates remarkable zero-shot generalization. However, SAM's power comes with a critical limitation for medical imaging: **it lacks domain-specific knowledge**. Medical images (histopathology, CT, MRI, ultrasound) have fundamentally different characteristics from natural images, and SAM's prompt-based interface requires expert guidance for every prediction, making it impractical for clinical deployment.

The naive solution—fine-tuning SAM on medical data—risks catastrophic forgetting of the rich generalizable representations that make SAM powerful in the first place.

---

## The Method

We propose **SemiSAM**, a foundation-model-driven co-training framework that transfers SAM's knowledge to a lightweight medical segmentation network without destroying SAM's pretrained representations.

<div class="row justify-content-sm-center">
    <div class="col-sm-10 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/semisam.jpg" title="Figure 1: Co-training pipeline between SAM and the student network." class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    <strong>Figure 1:</strong> Co-training pipeline between SAM and the student network. SAM provides pseudo-labels for unlabeled medical images, while the student network learns domain-specific features. Bidirectional knowledge distillation ensures complementary learning.
</div>

### Framework Architecture

**SemiSAM** operates through a principled two-branch co-training scheme:

1. **SAM Branch (Teacher)**: The frozen SAM model processes unlabeled medical images using automatically generated prompts (derived from image saliency or prior anatomical knowledge). SAM's predictions serve as pseudo-labels for the student network.

2. **Student Branch**: A lightweight medical segmentation network (e.g., U-Net, TransUNet) learns from:
   - **Labeled data**: Standard supervised loss on expert annotations
   - **Pseudo-labels**: Distillation loss from SAM's predictions on unlabeled data

3. **Bidirectional Knowledge Transfer**: The key innovation is that learning flows both ways:

$$
\mathcal{L}_{\text{total}} = \mathcal{L}_{\text{sup}}(y, \hat{y}_{\text{student}}) + \lambda_1 \mathcal{L}_{\text{distill}}(\hat{y}_{\text{SAM}}, \hat{y}_{\text{student}}) + \lambda_2 \mathcal{L}_{\text{consistency}}
$$

### Prompt-Free Deployment

A critical advantage of SemiSAM is that the trained student network requires **no prompts at inference time**. The student has internalized SAM's segmentation knowledge while learning domain-specific medical features, enabling fully automatic segmentation.

### Technical Innovations

| Component | Description |
|-----------|-------------|
| **Automatic Prompt Generation** | Saliency-based and anatomical prior prompts eliminate manual annotation |
| **Confidence-Weighted Distillation** | High-confidence SAM predictions receive larger weights |
| **Feature Alignment Loss** | Intermediate feature matching preserves SAM's representation structure |

---

## Why This Matters

SemiSAM exemplifies my research philosophy of **foundation-model-driven design**:

> *"Rather than treating foundation models as black boxes to fine-tune, we leverage their complementary strengths through principled co-training."*

This approach offers three key advantages:
1. **Preserves SAM's generalization**: SAM remains frozen, retaining its powerful zero-shot capabilities
2. **Enables efficient deployment**: The student network is lightweight and prompt-free
3. **Maximizes unlabeled data**: Abundant unannotated medical images become useful training signal

---

## Current Status

This is an **ongoing project** where I serve as the **lead researcher**, coordinating the experimental design, implementation, and manuscript preparation. Results are being prepared for submission to a top-tier venue.

---

## Related Work

This project builds on my broader research in semi-supervised medical imaging:
- Semi-MoE (BMVC 2025): Mixture-of-Experts for handling distribution shifts
- HDC (CVPRW 2025): Hierarchical distillation for noise-robust pseudo-labels

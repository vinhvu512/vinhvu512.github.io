---
layout: page
title: Stain-Structure Disentanglement
description: Learning Robust Representations for Histopathology under Staining Variability
img: assets/img/3.jpg
importance: 2
category: research
related_publications: true
---

## Overview

**Stain-Structure Disentanglement** tackles the challenge of H&E (Hematoxylin & Eosin) staining variability in histopathology image analysis. Different laboratories use varying staining protocols, leading to significant color shifts that confuse deep learning models.

This work was conducted at the [Machine and Hybrid Intelligence Lab, Northwestern University](https://www.mhilab.org/), under the supervision of Prof. Ulas Bagci.

---

## The Challenge

Histopathology slides are stained with H&E dyes to visualize tissue structures:
- **Hematoxylin** (purple/blue): stains cell nuclei
- **Eosin** (pink): stains cytoplasm and extracellular matrix

However, staining intensity and color balance vary significantly across:
- Different laboratories
- Batch-to-batch variations
- Scanner hardware differences

This variability causes models trained on one dataset to fail on others—a critical limitation for clinical deployment.

---

## Our Solution

We propose a **mean-teacher framework** that explicitly disentangles:

1. **Stain appearance**: Color and intensity characteristics of the staining
2. **Structural content**: Underlying tissue morphology independent of staining

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/1.jpg" title="Original H&E" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/3.jpg" title="Stain Variations" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/5.jpg" title="Structure Preserved" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Illustration of staining variability across different histopathology samples.
</div>

---

## Technical Approach

Our framework employs:

- **Dual encoders**: Separate pathways for stain and structure features
- **Consistency regularization**: Structure representations remain stable under stain augmentation
- **Mean-teacher training**: Temporal ensembling for stable pseudo-labels

The key insight is that while staining varies, the underlying tissue structure—the true diagnostic signal—remains constant.

---

## Impact

By separating appearance from content, our method:

- **Generalizes** across different staining protocols without retraining
- **Reduces** the annotation burden for multi-center studies
- **Enables** robust analysis with minimal labeled examples

---

## Publication

This work was accepted at the **MICCAI Workshop on Computational Pathology (COMPAYL) 2025**.

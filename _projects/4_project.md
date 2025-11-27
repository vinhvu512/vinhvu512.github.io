---
layout: page
title: 3D Y-Net for Single-Cell Tracking
description: Siamese Architecture for 3D Time-Lapse Microscopy Analysis
img: assets/img/6.jpg
importance: 4
category: research
---

## Overview

During my **international research internship** at the [Integrated MechanoBioSystems Lab](https://sites.google.com/site/imbs3dprinting/Home?authuser=0), National Cheng Kung University (NCKU), Taiwan, I developed a **Y-Net Siamese architecture** for tracking single cells in 3D time-lapse microscopy images.

This project represents my experience in **3D Computer Vision** and **international research collaboration**.

---

## The Problem

Cell tracking in 3D time-lapse microscopy is fundamental to understanding:
- Cell migration dynamics
- Cell division and proliferation
- Response to mechanical stimuli

However, 3D cell tracking presents unique challenges:

1. **Volumetric complexity**: Cells move in all three spatial dimensions
2. **Temporal associations**: Linking cells across time frames requires robust feature matching
3. **Morphological changes**: Cells deform, divide, and sometimes die during observation

---

## Our Solution: 3D Y-Net Siamese Architecture

<div class="row justify-content-sm-center">
    <div class="col-sm-10 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/6.jpg" title="3D Y-Net Architecture" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Conceptual illustration of the Y-Net Siamese network for 3D cell tracking.
</div>

### Architecture Design

The **Y-Net** architecture combines:

- **Siamese backbone**: Twin networks process cell candidates from consecutive time frames
- **3D convolutions**: Capture volumetric spatial features essential for 3D analysis
- **Multi-scale feature fusion**: The "Y" structure merges features at multiple resolutions

### Key Features

1. **Embedding learning**: Cells are mapped to a discriminative feature space where matched pairs are close
2. **Temporal consistency**: Exploits the assumption that cells move smoothly between frames
3. **Division handling**: Special provisions for tracking daughter cells after mitosis

---

## International Collaboration

This project was conducted during my **NSTC-funded internship** in Taiwan, providing invaluable experience in:

- Working with an international research team
- Adapting to different research cultures and methodologies
- Communicating complex technical ideas across language barriers

---

## Technical Highlights

| Aspect | Details |
|--------|---------|
| **Dimension** | Full 3D volumetric processing |
| **Architecture** | Y-Net with Siamese branches |
| **Input** | 3D time-lapse microscopy stacks |
| **Output** | Cell trajectories across time |

---

## Skills Developed

- **3D Computer Vision**: Volumetric feature extraction and analysis
- **Siamese Networks**: Metric learning for object association
- **Biomedical Imaging**: Understanding of microscopy data characteristics
- **International Research**: Cross-cultural scientific collaboration

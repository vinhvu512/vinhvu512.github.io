---
layout: page
title: DragPC
description: Interactive 3D Point Cloud Editing via Denoising Diffusion Models
img: assets/img/dragpc.jpg
importance: 5
category: research
---

<div class="row">
    <div class="col-sm-12">
        <p class="text-muted">
            <strong>Affiliation:</strong> FPT Software AI Center &nbsp;|&nbsp;
            <strong>Domain:</strong> Generative AI, 3D Computer Vision
        </p>
    </div>
</div>

---

## The Challenge

Interactive editing of 3D point clouds is a fundamental task in computer graphics, CAD design, and 3D content creation. However, existing approaches face a critical bottleneck: **editing 3D point clouds interactively is computationally expensive and difficult to control**. Traditional mesh-based deformation requires complex manual rigging, while learning-based methods often produce artifacts or fail to preserve geometric consistency. The recent success of "drag-based" editing in 2D images (e.g., DragGAN) raises a compelling question: *Can we enable intuitive drag-and-drop editing for 3D point clouds?*

---

## The Method

We propose **DragPC**, a generative framework that leverages **Denoising Diffusion Implicit Models (DDIM)** to enable interactive, semantically-aware 3D point cloud editing through latent space manipulation.

<div class="row justify-content-sm-center">
    <div class="col-sm-10 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/dragpc.jpg" title="Figure 1: Interactive 3D point cloud editing results using DragPC." class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    <strong>Figure 1:</strong> Interactive 3D point cloud editing results using DragPC. Users specify source (red) and target (green) points, and the diffusion model generates geometrically consistent deformations.
</div>

### Technical Framework

**DragPC** operates through three key stages:

#### 1. DDIM Inversion
Given an input point cloud $$\mathbf{P}_0$$, we invert the diffusion process to recover its latent representation:

$$
\mathbf{z}_T = \text{DDIM-Invert}(\mathbf{P}_0, \epsilon_\theta)
$$

This inversion maps the point cloud into the diffusion model's latent space while preserving reconstruction fidelity.

#### 2. Latent Space Manipulation
User-specified drag operations (source point $$\mathbf{p}_s$$ → target point $$\mathbf{p}_t$$) are encoded as latent modifications:

$$
\mathbf{z}'_T = \mathbf{z}_T + \Delta\mathbf{z}(\mathbf{p}_s, \mathbf{p}_t)
$$

The modification $$\Delta\mathbf{z}$$ is computed through gradient-based optimization that:
- Minimizes distance between source and target in the generated output
- Preserves global structure of non-edited regions
- Maintains local geometric consistency

#### 3. Guided Denoising
The modified latent $$\mathbf{z}'_T$$ is passed through the DDIM sampling process with geometric guidance:

$$
\mathbf{P}'_0 = \text{DDIM-Sample}(\mathbf{z}'_T, \epsilon_\theta, \mathcal{G})
$$

where $$\mathcal{G}$$ is a guidance function ensuring the output satisfies the drag constraints.

### Why DDIM?

We chose Denoising Diffusion Implicit Models over standard DDPM for three critical advantages:

| Property | Benefit for DragPC |
|----------|-------------------|
| **Deterministic Sampling** | Enables precise control—same latent always produces same output |
| **Efficient Inference** | 10-50 denoising steps (vs. 1000 for DDPM) |
| **Invertibility** | Faithful reconstruction of input before editing |

---

## Applications

DragPC enables intuitive 3D content creation across multiple domains:

- **CAD/Product Design**: Rapid prototyping and design iteration
- **Gaming/VR**: Interactive asset creation and modification
- **Medical Education**: Deformable 3D anatomy models for teaching
- **Robotics Simulation**: Generating diverse object variations for training

---

## Industry Research Experience

This project was conducted at **FPT Software AI Center**, providing valuable exposure to industry-scale AI research:

- Working with large-scale GPU clusters for training diffusion models
- Balancing research novelty with practical deployment requirements
- Collaborating across engineering and product teams
- Translating cutting-edge generative AI research into usable tools

---

## Technical Implementation

```
Framework:     PyTorch
Model:         Custom Point-Cloud DDIM (based on Point-Voxel CNN)
Training:      ShapeNet (55 categories, 51k models)
Evaluation:    ModelNet40, user study
Visualization: Open3D, PyVista
```

---

## Broader Impact

DragPC demonstrates my versatility beyond medical imaging—showcasing expertise in **generative AI** and **3D deep learning**. The diffusion modeling techniques developed here directly inform my medical imaging research, where generative models are increasingly important for data augmentation, anomaly detection, and counterfactual analysis.

#  Noise → Masterpiece: Build Stable Diffusion from First Principles


[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.9+](https://img.shields.io/badge/python-3.9+-blue.svg)](https://www.python.org/downloads/)
[![PyTorch](https://img.shields.io/badge/PyTorch-2.0+-red.svg)](https://pytorch.org/)

This repository is the complete guide and codebase for a 13‑week journey from the math of randomness to a working text‑to‑image diffusion model — built entirely by you, from scratch. No black boxes, no pre‑built pipelines, no API wrappers.

---

##  What I will Build

A **text‑to‑image diffusion model** — your own mini Stable Diffusion.

Feed it a prompt like `"a dog on the moon"` or `"the digit 3"`. Watch it generate matching images starting from pure random noise. You will implement all three core pillars:

- **Variational Autoencoder (VAE)** – compresses images into a compact latent space
- **Denoising Diffusion Probabilistic Model (DDPM)** – learns to reverse the noise process
- **CLIP text conditioning** – makes the model listen to your words

Every component is written, trained, and understood by you. No copying. No wrappers.

---

## 🗺️ The Journey — 5 Milestones

The project is a **single growing codebase**, not isolated assignments. Each week you extend what you built before.

| Milestone | Week | What you'll achieve |
|-----------|------|----------------------|
| **1** | 3 | First generative model – linear VAE on 2D synthetic data |
| **2** | 6 | Face VAE – morphing GIFs, latent space arithmetic on 200K faces |
| **3** | 8 | Forward diffusion – destroy images with controlled noise (T=1000) |
| **4** | 10 | Unconditional DDPM – generate MNIST & CIFAR‑10 from pure noise |
| **5** | 12 | **Text‑to‑image** – final project with CLIP conditioning |

---

## 📅 Week‑by‑Week Roadmap

| Week | Topic | Deliverable |
|------|-------|--------------|
| 0 | Python + NumPy + PyTorch + Probability basics | Linear regression in PyTorch |
| 1 | Math of uncertainty (Gaussians, Bayes, KL) | Intuition built |
| 2 | Deriving the VAE loss (ELBO) | Paper derivation + numerical check |
| 3 | **Milestone 1** – linear VAE on 2D data | Latent space plots |
| 4 | Convolutional VAE on MNIST | Sharper reconstructions |
| 5 | VAE on CelebA (200K faces) | Trained face model |
| 6 | **Milestone 2** – latent space surgery | Face interpolation GIF |
| 7 | Mathematics of noise (schedules, closed‑form) | Noise schedule implementation |
| 8 | **Milestone 3** – forward diffusion pipeline | Visualisation x₀ → x_T |
| 9 | Build the denoiser (UNet from scratch) | UNet with time embeddings |
| 10 | **Milestone 4** – unconditional DDPM | Samples from noise (MNIST, CIFAR) |
| 11 | Conditional generation (class labels + CFG) | “Generate a 7” |
| 12 | **Milestone 5** – text‑to‑image with CLIP | Final project done |



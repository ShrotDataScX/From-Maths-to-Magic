
# Week 3 --- Variational Autoencoder (VAE): Your First Generative Model

> **From Maths to Magic** --- Week 3 Milestone

## Overview

This project implements a **Linear Variational Autoencoder (VAE)** in
PyTorch on a simple 2D synthetic dataset. The objective is to understand
how a VAE learns a smooth latent representation capable of generating
new samples rather than simply reconstructing existing data.

Unlike a conventional autoencoder, a VAE learns a **probability
distribution** over the latent space, enabling meaningful sampling and
interpolation.

------------------------------------------------------------------------

## Project Objectives

-   Implement a Linear VAE from scratch
-   Understand the Encoder--Latent--Decoder pipeline
-   Implement the Reparameterization Trick
-   Derive and implement the ELBO loss
-   Visualize reconstructions, latent space and generated samples
-   Build intuition for probabilistic generative modelling

------------------------------------------------------------------------

## Architecture

``` text
Input (2D Point)
        │
        ▼
 Linear Encoder
        │
        ├────────► μ
        │
        └────────► log(σ²)
                    │
                    ▼
        Reparameterization
        z = μ + σ·ε
                    │
                    ▼
            Linear Decoder
                    │
                    ▼
        Reconstructed Point
```

------------------------------------------------------------------------

## Mathematical Foundation

The encoder approximates the posterior distribution

$$ q(z|x)=\mathcal{N}(\mu,\sigma^2I) $$

Instead of sampling directly,

$$ z=\mu+\sigma\odot\epsilon,\;\epsilon\sim\mathcal{N}(0,I) $$

where

$$ \sigma=\exp\left(\frac{1}{2}\log(\sigma^2)\right) $$

The reconstruction loss is

$$ \mathcal{L}_{recon}=||x-\hat{x}||_2^2 $$

The KL divergence between the learned posterior and the standard normal
prior is

$$ D_{KL}(q(z|x)\Vert p(z))=-\frac12\sum\left(1+\log(\sigma^2)-\mu^2-\sigma^2\right) $$

The complete Evidence Lower Bound (ELBO) is

$$ \mathcal{L}_{VAE}=\mathcal{L}_{recon}+D_{KL}(q(z|x)\Vert p(z)) $$

------------------------------------------------------------------------

## Model Components

### Encoder

Maps the input into two vectors:

-   Mean ($\mu$)
-   Log-variance ($\log(\sigma^2)$)

### Reparameterization Trick

Separates randomness from the network so gradients can flow through the
sampling process.

### Decoder

Maps latent variable $z$ back to the original input space.

------------------------------------------------------------------------

## Dataset

The implementation uses **`make_moons()`** from Scikit-Learn.

Reasons:

-   Fast CPU training
-   Easy visualization
-   Clear nonlinear structure
-   Ideal for understanding latent spaces

------------------------------------------------------------------------

## Training

Optimizer:

-   Adam

Loss:

-   Mean Squared Error
-   KL Divergence

------------------------------------------------------------------------

## Results

The notebook demonstrates:

-   Decreasing training loss
-   Accurate reconstructions
-   Structured latent representation
-   New samples generated from random latent vectors

------------------------------------------------------------------------

## Engineering Decisions

-   Linear layers only to focus on VAE mathematics.
-   Latent dimension kept small for visualization.
-   Adam optimizer chosen for stable convergence.
-   MSE used because the dataset consists of continuous coordinates.

------------------------------------------------------------------------

## Repository Structure

``` text
Week_3/
│── soc_week3_ass.ipynb
│── README.md
```

------------------------------------------------------------------------

## Key Learnings

-   Difference between Autoencoders and VAEs
-   Probabilistic latent representations
-   Reparameterization Trick
-   ELBO optimization
-   KL Divergence regularization
-   Latent space interpolation
-   Generative sampling

------------------------------------------------------------------------

## Future Work

-   Convolutional VAE on MNIST
-   β-VAE
-   Conditional VAE
-   CelebA generation
-   Diffusion Models

------------------------------------------------------------------------

## References

-   Kingma, D. P., & Welling, M. (2014). *Auto-Encoding Variational
    Bayes*.
-   PyTorch Documentation
-   Scikit-Learn Documentation

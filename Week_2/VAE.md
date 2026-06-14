# Variational Autoencoders (VAEs): Understanding the Mathematics Through Intuition

## Introduction

When I first learned about Variational Autoencoders (VAEs), I understood what a normal autoencoder was:

* An encoder compresses an input into a latent representation.
* A decoder reconstructs the original input from that representation.

However, I quickly encountered a fundamental question:

> If autoencoders already compress data, why do we need VAEs?

The answer lies in generation.

A normal autoencoder learns how to reconstruct data, but it does not learn a well-structured latent space from which we can generate new samples. VAEs solve this problem by treating latent representations probabilistically.

This blog explains the intuition behind VAEs from first principles.

---

# From Autoencoders to VAEs

A normal autoencoder works as follows:

```text
Input Image
     ↓
   Encoder
     ↓
 Latent Vector z
     ↓
   Decoder
     ↓
Reconstructed Image
```

For example, an image of the digit 5 might be mapped to:

```text
z = [2.1, -0.8]
```

The problem is that every image gets mapped to a single fixed point.

If we randomly choose another latent vector:

```text
z = [10, -7]
```

and feed it to the decoder, there is no guarantee that the decoder will generate anything meaningful.

The latent space is not organized.

---

# The Main Idea of a VAE

Instead of mapping an image to a single point, a VAE maps it to a probability distribution.

Instead of:

```text
Image → z
```

we learn:

```text
Image → Distribution over z
```

For example, the encoder outputs a mean and a standard deviation:

$$ \mu = 2.1,\ \sigma = 0.3 $$

This means:

> The image is not represented by exactly one latent point. It is represented by a small region around that point.

In other words, a digit 5 occupies a neighborhood in latent space rather than a single point.

---

# What Does Sampling Mean?

Suppose the encoder outputs:

$$ \mu = 3,\ \sigma = 0.5 $$

This describes a Gaussian distribution centered at 3.

Now we randomly choose a value from this distribution:

```text
z = 2.8
z = 3.2
z = 3.1
```

This process is called **sampling**.

Each sampled value represents a slightly different version of the same concept.

For example:

```text
z = 2.8 → thin handwritten 5
z = 3.1 → normal handwritten 5
z = 3.3 → curved handwritten 5
```

Sampling enables generation of diverse but realistic outputs.

---

# But Isn't x a Vector?

One question that initially confused me was:

> If images are vectors, how can we create a probability distribution over them?

Consider an MNIST image:

```text
28 × 28 pixels = 784 dimensions
```

Therefore:

$$ x \in \mathbb{R}^{784} $$

This means that x is not a single number but a 784-dimensional vector.

The answer is that probability distributions can exist over vectors as well.

Instead of a one-dimensional Gaussian:

$$ N(\mu,\sigma^2) $$

we use a multivariate Gaussian:

$$ N(\mu,\Sigma) $$

where:

* $\mu$ is a mean vector.
* $\Sigma$ is a covariance matrix.

The distribution now describes an entire cloud of possible vectors.

---

# What Is the Covariance Matrix?

The covariance matrix determines the shape and spread of the distribution.

Suppose:

$$ z = \begin{bmatrix} z_1 \ z_2 \end{bmatrix} $$

The mean tells us where the distribution is centered:

$$ \mu = \begin{bmatrix} 2 \ 3 \end{bmatrix} $$

The covariance matrix tells us:

1. How much each dimension varies.
2. Whether dimensions are correlated.

For example:

$$ \Sigma = \begin{bmatrix} 1 & 0 \ 0 & 1 \end{bmatrix} $$

means both dimensions vary independently.

But:

$$ \Sigma = \begin{bmatrix} 1 & 0.9 \ 0.9 & 1 \end{bmatrix} $$

means that when one dimension increases, the other usually increases as well.

The covariance matrix therefore controls the shape of the probability cloud.

---

# Why Don't VAEs Learn Full Covariance Matrices?

Suppose the latent space has 100 dimensions.

A full covariance matrix would contain:

$$ 100 \times 100 = 10,000 $$

parameters.

This is expensive and difficult to train.

Therefore most VAEs assume:

$$ \Sigma = \mathrm{diag}(\sigma^2) $$

which means:

```text
z₁ independent of z₂
z₂ independent of z₃
...
```

The encoder only predicts:

$$ \mu_1,\mu_2,\mu_3,\ldots $$

and

$$ \sigma_1,\sigma_2,\sigma_3,\ldots $$

instead of thousands of covariance terms.

This simplification makes training practical.

---

# How Sampling Is Actually Performed

The encoder outputs:

$$ \mu $$

and

$$ \sigma $$

Then we sample:

$$ \epsilon \sim N(0,I) $$

and compute:

$$ z = \mu + \sigma \odot \epsilon $$

where $\odot$ denotes element-wise multiplication.

For example:

$$ \mu = 3,\ \sigma = 0.5,\ \epsilon = 0.8 $$

Then:

$$ z = 3 + 0.5 \times 0.8 $$

Therefore:

$$ z = 3.4 $$

This gives us a sample from the learned latent distribution.

---

# Why Not Simply Use the Mean?

If we always used:

$$ z = \mu $$

then every image would map to a single point.

The model would lose its generative capability.

Sampling introduces diversity and allows the decoder to generate multiple realistic outputs.

---

# The Generative Story of a VAE

A VAE assumes that data is generated in two steps.

### Step 1: Sample a Latent Vector

$$ z \sim p(z) $$

Usually:

$$ p(z) = N(0,I) $$

### Step 2: Generate Data from the Latent Vector

$$ x \sim p(x|z) $$

Conceptually:

```text
Sample z
    ↓
 Decoder
    ↓
Generated Image
```

The goal of training is to learn a decoder that can generate realistic data from latent vectors.

---

# The Encoder Distribution

Given an image x, the encoder predicts a latent distribution:

$$ q_\phi(z|x) = N(\mu,\mathrm{diag}(\sigma^2)) $$

This means:

> Given the image x, what latent vectors z are plausible representations of that image?

Instead of mapping an image to a single point, we map it to a probability distribution.

---

# Why Do We Need KL Divergence?

The reconstruction loss ensures:

$$ \hat{x} \approx x $$

However, we also want all latent distributions to resemble a standard Gaussian:

$$ N(0,I) $$

This is enforced using KL divergence.

The KL divergence term is:

$$ D_{KL}(q_\phi(z|x),|,p(z)) $$

It encourages:

* Means close to zero.
* Variances close to one.
* Smooth latent spaces.
* Better generation.

Without this term, the latent space would become chaotic and random sampling would fail.

---

# The VAE Loss Function

The complete VAE objective consists of two terms:

$$ \mathcal{L} = \text{Reconstruction Loss} + D_{KL}(q_\phi(z|x),|,p(z)) $$

The reconstruction term ensures that outputs resemble inputs.

The KL divergence term ensures that latent representations follow a well-structured probability distribution.

Together, these two objectives create a latent space from which meaningful new samples can be generated.

---

# Final Intuition

A normal autoencoder learns:

```text
Image → Point
```

A Variational Autoencoder learns:

```text
Image → Probability Distribution
```

Instead of representing data as isolated points, VAEs represent data as smooth regions in latent space.

This allows:

* Sampling
* Interpolation
* Generation of new data
* Structured latent representations

This simple idea transforms an autoencoder from a compression model into a powerful generative model.

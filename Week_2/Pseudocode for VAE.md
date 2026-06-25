# Simple Pseudocode for Training a VAE and Generating an Image

In this example, assume:

```text
Input dimension = 10
Latent dimension = 4
```

This means each input data point has 10 values, and the VAE will compress it into a 4-dimensional latent vector.

But because this is a VAE, the encoder does not directly output 4 latent values. Instead, it outputs:

```text
4 mean values
4 log-variance values
```

So the encoder output has 8 numbers.

```text
mu = [mu1, mu2, mu3, mu4]
logvar = [logvar1, logvar2, logvar3, logvar4]
```

The actual bottleneck vector is still 4-dimensional:

```text
z = [z1, z2, z3, z4]
```

---

# Part 1: Model Structure

```text
Input x with 10 values
        ↓
Encoder
        ↓
mu with 4 values
logvar with 4 values
        ↓
Sampling step
        ↓
z with 4 values
        ↓
Decoder
        ↓
Reconstructed output with 10 values
```

The encoder learns how to convert input data into a probability distribution.

The decoder learns how to convert a sampled latent vector back into the original type of data.

---

# Part 2: Encoder Pseudocode

```text
Take input x with 10 values

Pass x through encoder hidden layers

From the final hidden layer, create two outputs:

    mu = 4 numbers

    logvar = 4 numbers

Return mu and logvar
```

Example:

```text
Input x = [x1,x2,x3,x4,x5,x6,x7,x8,x9,x10]

Encoder outputs:

mu = [2.1,-1.3,0.7,4.2]

logvar = [-2.0,0.5,-1.0,-3.0]
```

Here, `logvar` can be negative because it is not variance directly. It is the logarithm of variance.

$$ logvar = \log(\sigma^2) $$

To get variance back:

$$ \sigma^2 = e^{logvar} $$

To get standard deviation:

$$ \sigma = e^{0.5 \times logvar} $$

---

# Part 3: Sampling Pseudocode

The VAE needs to sample a latent vector `z`.

But we do not sample directly from `mu` and `logvar`.

We use the reparameterization trick.

```text
Take mu

Take logvar

Convert logvar into standard deviation:

    std = exp(0.5 * logvar)

Create random noise epsilon from normal distribution:

    epsilon = random normal values with shape 4

Create latent vector:

    z = mu + std * epsilon

Return z
```

Mathematically:

$$ z = \mu + \sigma \times \epsilon $$

where:

$$ \epsilon \sim \mathcal{N}(0,1) $$

Example:

```text
mu = [2.1,-1.3,0.7,4.2]

std = [0.36,1.28,0.60,0.22]

epsilon = [0.5,-1.0,0.2,1.5]

z = mu + std * epsilon

z = [2.28,-2.58,0.82,4.53]
```

Now `z` has only 4 values.

This is the actual bottleneck vector.

---

# Part 4: Decoder Pseudocode

```text
Take z with 4 values

Pass z through decoder hidden layers

Output reconstructed data with 10 values

Return reconstructed output
```

Example:

```text
z = [2.28,-2.58,0.82,4.53]

Decoder output:

x_reconstructed = [0.9,0.1,0.7,0.3,0.8,0.2,0.4,0.6,0.5,0.9]
```

The decoder tries to recreate the original input.

---

# Part 5: Loss Function

A VAE has two losses.

## 1. Reconstruction Loss

This checks how close the reconstructed output is to the original input.

```text
If reconstruction is close to input, reconstruction loss is small.

If reconstruction is very different, reconstruction loss is large.
```

Simple idea:

$$ Reconstruction\ Loss = difference\ between\ x\ and\ x_{reconstructed} $$

## 2. KL Loss

This forces the encoder's learned distribution to stay close to a normal distribution.

The standard normal distribution is:

$$ \mathcal{N}(0,1) $$

The KL loss for a VAE is:

$$ KL = -0.5 \times \sum(1 + logvar - \mu^2 - e^{logvar}) $$

The full VAE loss is:

$$ Total\ Loss = Reconstruction\ Loss + KL\ Loss $$

---

# Part 6: Training Pseudocode

```text
Start with random encoder weights

Start with random decoder weights

Repeat for many epochs:

    Take one batch of training data

    Send the batch into the encoder

    Encoder outputs mu and logvar

    Convert logvar into standard deviation

    Create random noise epsilon

    Create z using:

        z = mu + std * epsilon

    Send z into the decoder

    Decoder produces reconstructed output

    Compare reconstructed output with original input

    Calculate reconstruction loss

    Calculate KL loss

    Add both losses:

        total loss = reconstruction loss + KL loss

    Use backpropagation to calculate gradients

    Use optimizer to update encoder and decoder weights

Repeat until the model learns good reconstructions
```

---

# Part 7: Full Training Algorithm in Simple English

```text
1. Give the model real training data.

2. The encoder looks at the input.

3. The encoder outputs mu and logvar.

4. Convert logvar into standard deviation.

5. Add controlled random noise to mu.

6. This gives a latent vector z.

7. Send z to the decoder.

8. Decoder tries to recreate the original input.

9. Compare the recreated output with the real input.

10. Penalize the model if reconstruction is bad.

11. Also penalize the model if the latent distribution moves too far away from normal distribution.

12. Update the model weights.

13. Repeat many times.
```

---

# Part 8: Generating New Data or Image After Training

After training, we do not need the encoder.

The encoder is used during training to learn the latent space.

For generation, we only need the decoder.

```text
Create random z from normal distribution

Send z into trained decoder

Decoder outputs a new generated sample
```

Mathematically:

$$ z \sim \mathcal{N}(0,1) $$

Then:

```text
generated_output = decoder(z)
```

If the VAE was trained on images, the output will be a new generated image.

---


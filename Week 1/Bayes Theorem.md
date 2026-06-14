# Bayes' Theorem 

Bayes' Theorem helps us update our belief about something after observing new evidence.

## Bayes' Theorem Formula

\[
P(H|D)=\frac{P(D|H)\cdot P(H)}{P(D)}
\]

Where:

- **H** = Hypothesis (what we want to know)
- **D** = Data (what we observed)

Read as:

> Probability of the hypothesis after seeing the data  
> =  
> Probability of the data given the hypothesis × Prior belief  
> ÷  
> Probability of the data

---

# Key Terms

## 1. Prior Probability

### Formula

\[
P(H)
\]

### Meaning

The probability of the hypothesis **before** seeing any data.

### Example

Suppose only 1% of people have a disease.

\[
P(Disease)=0.01
\]

This is the prior probability.

### Intuition

Ask yourself:

> "Before seeing any evidence, how likely is this?"

---

## 2. Likelihood

### Formula

\[
P(Data|H)
\]

### Meaning

The probability of observing the data if the hypothesis is true.

### Example

If a person has the disease, the test correctly returns positive 99% of the time.

\[
P(Positive|Disease)=0.99
\]

This is the likelihood.

### Intuition

Ask yourself:

> "If my hypothesis is true, how likely am I to observe this data?"

---

## 3. Evidence (Marginal Probability)

### Formula

\[
P(Data)
\]

### Meaning

The overall probability of observing the data.

### Example

\[
P(Positive)
\]

This includes both:

- True positives
- False positives

### Intuition

Ask yourself:

> "How common is this observation in the entire population?"

---

## 4. Posterior Probability

### Formula

\[
P(H|Data)
\]

### Meaning

The probability of the hypothesis after observing the data.

### Example

\[
P(Disease|Positive)
\]

Probability that a person has the disease after receiving a positive test result.

### Intuition

Ask yourself:

> "Now that I've seen the evidence, what should I believe?"

---

# Bayes Workflow

```text
Prior Belief
      ↓
Observe Data
      ↓
Apply Bayes' Theorem
      ↓
Posterior Belief
```

Or simply:

```text
Old Belief
     +
New Evidence
     =
Updated Belief
```

---

# Example: Medical Test

Suppose:

- 1% of the population has a disease

\[
P(D)=0.01
\]

- The test correctly identifies the disease 99% of the time

\[
P(Pos|D)=0.99
\]

- The false positive rate is 5%

\[
P(Pos|\bar D)=0.05
\]

---

## Step 1: Calculate Evidence

Using the Law of Total Probability:

\[
P(Pos)=P(Pos|D)P(D)+P(Pos|\bar D)P(\bar D)
\]

Substituting values:

\[
=0.99(0.01)+0.05(0.99)
\]

\[
=0.0099+0.0495
\]

\[
=0.0594
\]

---

## Step 2: Calculate Posterior

Applying Bayes' Theorem:

\[
P(D|Pos)=\frac{0.99\times0.01}{0.0594}
\]

\[
\approx0.1667
\]

---

## Result

\[
P(D|Pos)\approx16.7\%
\]

Even after testing positive, the probability that the person actually has the disease is only about **16.7%**.

### Why?

Because:

- The disease is very rare.
- False positives occur much more frequently than true positives.

This is one of the most famous examples demonstrating the importance of Bayes' Theorem.

---

# Detective Analogy

Imagine you're a detective.

## Prior

Before seeing any clues:

> "I think there's a 10% chance this suspect is guilty."

---

## Likelihood

You find a fingerprint.

Ask:

> "If the suspect were guilty, how likely would it be to find this fingerprint?"

---

## Evidence

Ask:

> "How common are fingerprints like this in general?"

---

## Posterior

After examining the fingerprint:

> "What is the probability that the suspect is guilty now?"

---

# Bayes in Machine Learning

Bayesian Machine Learning follows the same idea:

1. Start with a prior belief about model parameters.
2. Observe training data.
3. Update beliefs using Bayes' Theorem.
4. Obtain a posterior distribution.

```text
Prior
  +
Data
  ↓
Posterior
```

When more data arrives:

```text
Posterior (old)
      ↓
Becomes
      ↓
Prior (new)
```

and the process repeats.

---

# Summary Table

| Term | Formula | Meaning |
|--------|---------|---------|
| Prior | P(H) | Belief before seeing data |
| Likelihood | P(D\|H) | Probability of data if hypothesis is true |
| Evidence | P(D) | Overall probability of observing the data |
| Posterior | P(H\|D) | Updated belief after seeing data |

---

# Memory Trick

> Posterior = Prior × Likelihood ÷ Evidence

or

> Updated Belief = Old Belief + New Evidence

(Bayes' Theorem is the mathematical way of performing this update.)
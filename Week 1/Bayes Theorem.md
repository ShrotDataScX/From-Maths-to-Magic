# Bayes' Theorem

Bayes' Theorem helps us update our belief about something after observing new evidence.

## Bayes' Theorem Formula

$$
P(H \mid D)=\frac{P(D \mid H)\cdot P(H)}{P(D)}
$$

Where:

* **H** = Hypothesis (what we want to know)
* **D** = Data (what we observed)

---

# Key Terms

## 1. Prior Probability

### Formula

$$
P(H)
$$

### Example

Suppose only 1% of people have a disease.

$$
P(\text{Disease})=0.01
$$

---

## 2. Likelihood

### Formula

$$
P(\text{Data} \mid H)
$$

### Example

If a person has the disease, the test correctly returns positive 99% of the time.

$$
P(\text{Positive} \mid \text{Disease})=0.99
$$

---

## 3. Evidence (Marginal Probability)

### Formula

$$
P(\text{Data})
$$

### Example

$$
P(\text{Positive})
$$

---

## 4. Posterior Probability

### Formula

$$
P(H \mid \text{Data})
$$

### Example

$$
P(\text{Disease} \mid \text{Positive})
$$

---

# Example: Medical Test

Suppose:

$$
P(D)=0.01
$$

$$
P(\text{Pos} \mid D)=0.99
$$

$$
P(\text{Pos} \mid \bar{D})=0.05
$$

## Step 1: Calculate Evidence

Using the Law of Total Probability:

$$
P(\text{Pos}) =
P(\text{Pos}\mid D)P(D)
+
P(\text{Pos}\mid \bar{D})P(\bar{D})
$$

Substituting values:

$$
=0.99(0.01)+0.05(0.99)
$$

$$
=0.0099+0.0495
$$

$$
=0.0594
$$

## Step 2: Calculate Posterior

Applying Bayes' Theorem:

$$
P(D\mid \text{Pos})
=
\frac{0.99\times0.01}{0.0594}
$$

$$
\approx0.1667
$$

## Result

$$
P(D\mid \text{Pos})
\approx16.7%
$$

---

# Summary Table

| Term       | Formula       | Meaning                                   |
| ---------- | ------------- | ----------------------------------------- |
| Prior      | $P(H)$        | Belief before seeing data                 |
| Likelihood | $P(D \mid H)$ | Probability of data if hypothesis is true |
| Evidence   | $P(D)$        | Overall probability of observing the data |
| Posterior  | $P(H \mid D)$ | Updated belief after seeing data          |

---

# Memory Trick

> Posterior = Prior × Likelihood ÷ Evidence

or

> Updated Belief = Old Belief + New Evidence

(Bayes' Theorem is the mathematical way of performing this update.)

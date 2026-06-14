# GitHub README Mathematics Formatting Prompt

You are writing a GitHub README.md for a mathematics, statistics, machine learning, quantitative finance, physics, or computer science article.

Your highest priority is producing GitHub-compatible Markdown with clean, readable mathematical notation.

---

## MATHEMATICAL FORMATTING RULES (CRITICAL)

### 1. Use GitHub-Compatible LaTeX Only

Use standard LaTeX syntax supported by GitHub Markdown math rendering.

Examples:

```latex
\mu
\sigma
\rho
\frac{a}{b}
\sqrt{x}
\sum
\int
\begin{bmatrix}
...
\end{bmatrix}
```

---

### 2. ALL Display Equations Must Be Written on a SINGLE PHYSICAL LINE

CORRECT:

```md
$$ Cov(X,Y) = E[XY] - E[X]E[Y] $$

$$ Var(X) = E[X^2] - (E[X])^2 $$

$$ Z = \frac{X-\mu}{\sigma} $$
```

INCORRECT:

```md
$$
Cov(X,Y)
=
E[XY]
-
E[X]E[Y]
$$
```

INCORRECT:

```md
$$
Var(X)
=
Cov(X,X)
$$
```

Every display equation must occupy exactly ONE line in the Markdown source file.

---

### 3. Never Break Mathematical Expressions Across Multiple Lines

Never place any of the following on separate lines:

* =
* *
* *
* \times
* \cdot
* \approx
* \le
* \ge
* \neq
* \sim
* \in
* \subset

CORRECT:

```md
$$ Cov(X,Y) = E[XY] - E[X]E[Y] $$
```

INCORRECT:

```md
$$
Cov(X,Y)
=
E[XY]
-
E[X]E[Y]
$$
```

---

### 4. Never Break Fractions Across Lines

CORRECT:

```md
$$ \frac{a+b}{c+d} $$
```

INCORRECT:

```md
$$
\frac{a+b}
{c+d}
$$
```

---

### 5. Never Break Integrals Across Lines

CORRECT:

```md
$$ E[X] = \int_{-\infty}^{\infty} x f(x)\,dx $$
```

INCORRECT:

```md
$$
E[X]
=
\int_{-\infty}^{\infty}
x f(x)\,dx
$$
```

---

### 6. Never Break Summations Across Lines

CORRECT:

```md
$$ E[X] = \sum_{i=1}^{n} x_i p_i $$
```

INCORRECT:

```md
$$
E[X]
=
\sum_{i=1}^{n}
x_i p_i
$$
```

---

### 7. Use Inline Math for Short Expressions

Use inline math whenever the expression naturally fits inside a sentence.

Example:

```md
The variance is $Var(X)=\sigma^2$.
```

Example:

```md
For a Bernoulli random variable, $E[X]=p$ and $Var(X)=p(1-p)$.
```

---

### 8. Use Display Math Only for Important Equations

Example:

```md
$$ Var(X) = E[X^2] - (E[X])^2 $$
```

Example:

```md
$$ Cov(X,Y) = E[(X-E[X])(Y-E[Y])] $$
```

---

### 9. Matrices

### 9.1 GitHub-Safe Matrix and Function Commands

GitHub's Markdown math renderer does not support all LaTeX macros.

Avoid unsupported commands such as:

```latex
\operatorname
```

Example (DO NOT USE):

```md
$$ \Sigma = \operatorname{diag}(\sigma^2) $$
```

Instead use one of the following GitHub-safe alternatives:

```md
$$ \Sigma = \mathrm{diag}(\sigma^2) $$
```

or preferably:

```md
$$ \Sigma = diag(\sigma^2) $$
```

Similarly, prefer plain text function names or `\mathrm{}` for common operators:

CORRECT:

```md
$$ \Sigma = diag(\sigma^2) $$
```

```md
$$ \Sigma = \mathrm{diag}(\sigma^2) $$
```

```md
$$ \arg\max_{\theta} p(x) $$
```

INCORRECT:

```md
$$ \Sigma = \operatorname{diag}(\sigma^2) $$
```

When generating GitHub README files:

- Do not use `\operatorname{}`.
- Prefer plain-text function names such as `diag`, `softmax`, `ReLU`, `KL`.
- If styling is needed, use `\mathrm{}`.
- Prioritize compatibility with GitHub's native math renderer over full LaTeX compatibility.
Matrices may contain LaTeX row separators (`\\`) but the entire matrix must remain on a SINGLE Markdown line.

CORRECT:

```md
$$ \Sigma = \begin{bmatrix} Var(X_1) & Cov(X_1,X_2) \\ Cov(X_2,X_1) & Var(X_2) \end{bmatrix} $$
```

INCORRECT:

```md
$$
\Sigma =
\begin{bmatrix}
Var(X_1) & Cov(X_1,X_2)
\\
Cov(X_2,X_1) & Var(X_2)
\end{bmatrix}
$$
```

---

### 10. Do Not Use Unicode Mathematical Symbols

Use:

```latex
\mu
\sigma
\rho
\times
\approx
\le
\ge
```

Do NOT use:

```text
μ
σ
ρ
×
≈
≤
≥
```

---

### 11. Preserve Mathematical Meaning

Do not simplify, alter, or rewrite equations unless explicitly asked.

Only improve formatting.

---

### 12. Output Only GitHub Markdown

Do not output:

* HTML
* MathJax configuration
* XML
* Rich text
* LaTeX documents

Output only valid GitHub Markdown.

---

### 13. Avoid Markdown Conflicts

Never generate:

```md
========
```

inside equations.

Never generate:

```md
## Heading
```

inside equations.

Never generate:

```md
---
```

inside equations.

Never generate Markdown syntax inside math blocks.

---

### 14. Readability Priority

Prioritize:

1. GitHub Preview Rendering
2. GitHub Source Readability
3. Mathematical Accuracy
4. Visual Beauty

---

### 15. Mandatory Validation Before Output

Before returning the answer, verify:

* Every display equation begins and ends on the same physical line.
* No equation contains a line break.
* No equation contains Markdown syntax.
* No equation contains accidental headings.
* No equation contains separator lines.
* Every equation is enclosed inside a single pair of `$$`.
* Every equation is directly copy-pastable into GitHub README.md.

---

### 16. Hard Failure Condition

FAIL THE RESPONSE if any display equation contains a newline between the opening `$$` and closing `$$`.

Every display equation MUST follow this pattern:

```md
$$ equation $$
```

and NEVER this pattern:

```md
$$
equation
$$
```

This rule is non-negotiable.

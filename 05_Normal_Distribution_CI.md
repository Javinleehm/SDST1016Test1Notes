# Chapter 5: Normal Distribution & Confidence Intervals

> **Test 2 coverage.** Not in Test 1 (March 24). Will be in the second test.

---

## Part 1: The Normal Distribution

### Why Normal Distribution?

The lecturer asked: *"Why do we study the normal distribution above all others?"*

**Answer:** The normal distribution is the **maximum entropy distribution** — it contains the most information among all distributions with the same mean and variance. It's the most "informative" distribution.

---

### Properties of the Normal Distribution

If `Y ~ N(μ, σ²)`:

1. **Bell-shaped curve** — symmetric, peaks in the middle
2. **Symmetric about μ** — left half mirrors right half
3. **Empirical Rule:**

| Range | % of observations |
|-------|------------------|
| μ ± 1σ | ~68% |
| μ ± 2σ | ~95% |
| μ ± 3σ | ~100% (99.74%) |

> **Application example:** If IQ ~ N(100, 15²), then:
> - 68% of people have IQ between 85 and 115
> - 95% of people have IQ between 70 and 130

4. **Smaller variance** → taller, narrower curve
5. **Larger variance** → shorter, flatter curve
6. Different means → curve shifts left/right; same shape

---

### Z-Transformation (Standardisation)

Convert any normal variable to **standard normal** Z ~ N(0, 1):

$$Z = \frac{Y - \mu}{\sigma}$$

After this transformation: mean = 0, SD = 1.

---

### Reading the Normal Table

The table gives: **area under the curve from 0 to Z** = shaded gray area in the middle.

| What you want | How to calculate |
|---------------|-----------------|
| P(0 < Z < z) | Read directly from table |
| P(Z > z) | = 0.5 − table value |
| P(Z < z) for z > 0 | = 0.5 + table value |
| P(−z < Z < z) | = 2 × table value |
| P(−z < Z < 0) | = table value (by symmetry) |

**Example:** Z = 1.2 → table value = 0.3849
- P(0 < Z < 1.2) = 0.3849
- P(Z > 1.2) = 0.5 − 0.3849 = 0.1151
- P(Z < 1.2) = 0.5 + 0.3849 = 0.8849

---

### Key Critical Values (Memorise These!)

| Confidence Level | z value | P(−z < Z < z) |
|-----------------|---------|----------------|
| 90% | **z = 1.645** | 0.90 |
| **95%** | **z = 1.96** | 0.95 |
| 98% | **z = 2.326** | 0.98 |

> The lecturer said: **"I only ask 95% CI in this course. The only number you need is 1.96."**

---

## Part 2: Percentile Calculations from a Histogram

This was introduced in lecture as a bridge between Chapter 3 percentiles and the normal distribution.

### Step A: Finding Percentile from a Frequency Histogram

**Given:** Histogram with frequency bars. Total n observations.

**Example Distribution** (from lecture):

| Bin | Frequency |
|-----|-----------|
| [10, 20) | 50 |
| [20, 30) | 40 |
| [30, 40) | 30 |
| [40, 50) | 20 |
| [50, 60) | 30 |
| [60, 70) | 20 |
| [70, 80) | 10 |
| **Total** | **200** |

**Find the 75th percentile:**

1. Target = 75% × 200 = **150 observations**
2. Cumulate: 50, 90, 120, 140, 170...
   - Up to 50 → 140 observations (not enough)
   - Up to 60 → 170 observations (too many)
   - So the 150th observation is between 50 and 60
3. Linear interpolation:
   - Lower limit (observations reaching 50) = 140
   - Upper limit (observations reaching 60) = 170
   - Want 150

$$\text{Answer} = 50 + \frac{150 - 140}{170 - 140} \times (60 - 50) = 50 + \frac{10}{30} \times 10 = 50 + 3.33 = \mathbf{55}$$

**The 75th percentile = 55.**

---

### Step B: Using Normal Distribution to Find Percentile 🔑

**Problem:** Given Y ~ N(45, 12²), find the 75th percentile.

**Step 1:** Set up the equation.
$$P(Y < C) = 0.75$$

**Step 2:** Standardise.
$$P\left(Z < \frac{C - 45}{12}\right) = 0.75$$

**Step 3:** The left half (−∞ to 0) = 0.5. We need 0.75 − 0.5 = **0.25 more** from the table.

**Step 4:** Find Z such that table value = 0.25.
- Table: Z = 0.67 → 0.2486; Z = 0.68 → 0.2517
- 0.25 is between 0.67 and 0.68 → use **Z ≈ 0.6745** (or ≈ 0.675 is fine)

**Step 5:** Equate and solve for C.
$$\frac{C - 45}{12} = 0.6745$$
$$C = 45 + 0.6745 \times 12 = 45 + 8.09 = \mathbf{53.09}$$

**The 75th percentile = 53.09**

---

### Finding Unknown SD or Mean 🔑

**Part D: Known percentile, unknown SD**

Given: Y ~ N(45, σ²), 75th percentile is 55 (from histogram result in Part A).

$$\frac{55 - 45}{\sigma} = 0.6745$$
$$\sigma = \frac{55 - 45}{0.6745} = \frac{10}{0.6745} = \mathbf{14.83}$$

**Part E: Known percentile, unknown mean**

Given: Y ~ N(μ, 12²), 25th percentile is 20 (from histogram Part B).

The 25th percentile corresponds to Z = −0.6745 (negative because it's below the mean).

$$\frac{20 - \mu}{12} = -0.6745$$
$$\mu = 20 + 0.6745 \times 12 = 20 + 8.09 = \mathbf{28.09}$$

---

## Part 3: Distribution of the Sample Mean (Central Limit Theorem)

### Key Theorem

If Y₁, Y₂, ..., Yₙ are observations from N(μ, σ²):

$$\bar{Y} \sim N\left(\mu, \frac{\sigma^2}{n}\right)$$

Or equivalently:
$$Z = \frac{\bar{Y} - \mu}{\sigma/\sqrt{n}} \sim N(0, 1)$$

---

### Central Limit Theorem (CLT)

**The amazing result:** Even if the underlying population is NOT normal, when sample size is large (n ≥ 30), the **sample mean** is still approximately normally distributed!

$$\bar{Y} \overset{\cdot}{\sim} N\left(\mu, \frac{\sigma^2}{n}\right) \quad \text{for large n}$$

> Why is this important? We know how to calculate EVERYTHING about normal distributions. So if the sample mean is normal, we can calculate everything about it too.

---

### Distribution of Sample Proportion

The sample proportion `p̂` is itself a type of sample mean. By CLT:

$$\hat{p} \overset{\cdot}{\sim} N\left(p, \frac{p(1-p)}{n}\right)$$

Where p = true population proportion.

---

## Part 4: Confidence Intervals

### The Concept

A **confidence interval (CI)** is a range of values that captures the true unknown parameter with a specified probability.

> **95% CI** → "There is a 95% chance that the true parameter lies within this range."

### Margin of Error
In survey results like "32% ± 3%", the **3%** is the **margin of error**.
- Range = 29% to 35%
- This range is the **95% confidence interval**

---

### 95% CI for a Population Proportion 🔑

$$\hat{p} \pm 1.96 \times \sqrt{\frac{\hat{p}(1-\hat{p})}{n}}$$

**Example:** 317 out of 990 support CE → p̂ = 0.32

$$0.32 \pm 1.96 \times \sqrt{\frac{0.32 \times 0.68}{990}} = 0.32 \pm 0.0291$$

95% CI = **(0.2909, 0.3491)** or equivalent to **32% ± 3%**

---

### 95% CI for a Population Mean 🔑

$$\bar{Y} \pm 1.96 \times \frac{\sigma}{\sqrt{n}}$$

**Example:** n = 100, Ȳ = 100, σ = 15 (known):

$$100 \pm 1.96 \times \frac{15}{\sqrt{100}} = 100 \pm 1.96 \times 1.5 = 100 \pm 2.94 = (97.06, 102.94)$$

> If σ is unknown, use the sample SD s as an approximation for σ. (The lecturer said he won't ask you to calculate this — just know the concept.)

---

### The Backward Method (Finding Margin of Error) 🔑

This is the **useful direction:** given you want a 95% CI and know the sample proportion, find the margin of error.

**Setup:** For 95% confidence, the Z value is 1.96:

$$1.96 = \frac{\text{upper limit} - \hat{p}}{\sqrt{\frac{\hat{p}(1-\hat{p})}{n}}}$$

**Solving for the upper limit:**

$$\text{upper limit} = \hat{p} + 1.96 \times \sqrt{\frac{\hat{p}(1-\hat{p})}{n}}$$

**Margin of error** = upper limit − p̂

---

### Linear Interpolation for Table Values 🔑

When the test statistic Z = 1.6525 (for example), but the table only shows 1.65 and 1.66:

1. Find the table values:
   - Area at 1.65 = 0.4505
   - Area at 1.66 = 0.4515

2. Apply linear interpolation:
$$\text{Area} = 0.4505 + \frac{1.6525 - 1.65}{1.66 - 1.65} \times (0.4515 - 0.4505)$$
$$= 0.4505 + \frac{0.0025}{0.01} \times 0.001 = 0.4505 + 0.00025 = 0.4508$$

3. Tail area = 0.5 − 0.4508 = **0.0492**

---

## Part 5: Sample Size Determination 🔑

**Question:** How large a sample do you need to achieve a 95% CI with margin of error ME?

**Formula:**

$$n = \left(\frac{1.96}{ME}\right)^2 \times p(1-p)$$

If **p is unknown**, use p = 0.5 (this maximises variance and gives the most conservative/safe sample size).

**Example:** Want margin of error ≤ 3% (ME = 0.03):

$$n = \left(\frac{1.96}{0.03}\right)^2 \times 0.5 \times 0.5 = (65.33)^2 \times 0.25 = 4268 \times 0.25 = 1067.1$$

→ **Round UP** to n = **1068**

> Always round **up** for sample size, even if the decimal is tiny (e.g., 1067.001 → 1068). "A little bit more than enough is better than not enough."

---

## Part 6: Randomised Response Technique (Sensitive Questions)

### The Problem
Asking sensitive questions directly (e.g., "Are you gay?") gets dishonest answers. Everyone says no.

### The Solution: Randomised Response Technique

**Setup:**
- Prepare 20 flashcards: 12 say "I am not gay", 8 say "I am gay"
- Student randomly picks ONE card (without showing the interviewer)
- Student answers YES (card matches me) or NO (card does not match me)
- The interviewer doesn't know which card was picked → **privacy is protected**

**This is zero-knowledge proof** — even after answering, the interviewer has zero knowledge of the student's identity.

### Calculating the True Proportion 🔑

$$P(\text{Yes}) = P(\text{not gay}) \times \frac{12}{20} + P(\text{gay}) \times \frac{8}{20}$$

If 140 out of 250 students said "Yes" (P(Yes) = 140/250 = 0.56):

$$0.56 = (1 - P_{\text{gay}}) \times 0.6 + P_{\text{gay}} \times 0.4$$

$$0.56 = 0.6 - 0.6 P_{\text{gay}} + 0.4 P_{\text{gay}}$$

$$0.56 - 0.6 = -0.2 P_{\text{gay}}$$

$$P_{\text{gay}} = \frac{0.6 - 0.56}{0.2} = \frac{0.04}{0.2} = \mathbf{0.2 = 20\%}$$

---

## Summary: Key Formulas

| What | Formula |
|------|---------|
| Z-standardisation | `Z = (Y − μ) / σ` |
| Sample mean distribution | `Ȳ ~ N(μ, σ²/n)` |
| Sample proportion distribution | `p̂ ~ N(p, p(1−p)/n)` |
| 95% CI for mean | `Ȳ ± 1.96 × σ/√n` |
| 95% CI for proportion | `p̂ ± 1.96 × √(p̂(1−p̂)/n)` |
| Sample size formula | `n = (1.96/ME)² × p(1−p)`, use p = 0.5 if unknown |
| Percentile from table | `P(0<Z<z) = table value`, `P(Z>z) = 0.5 − table` |
| μ ± 1σ | 68% |
| μ ± 2σ | 95% |
| μ ± 3σ | ~100% |

---

## Common Mistakes to Avoid

1. **Don't forget to take the square root** when computing standard error: √(p(1-p)/n), not p(1-p)/n
2. **Normal table gives area from 0 to Z** (not from -∞). Adjust accordingly.
3. **For 95% CI**, the Z value is 1.96 (not 2.0, which is an approximation)
4. **Always round UP sample size**, never down
5. When finding percentile from table: subtract 0.5 first if the probability is > 0.5

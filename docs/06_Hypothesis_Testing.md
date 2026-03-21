# Chapter 6: Hypothesis Testing

> **Test 2 coverage.** Not in Test 1.

---

## What Is Hypothesis Testing?

Hypothesis testing is a formal procedure for deciding, based on data, whether to reject a claimed value of a population parameter.

**The 5-Step Procedure:**
1. State H₀ (null hypothesis) and H₁ (alternative hypothesis)
2. Collect random sample, compute sample statistic
3. **Assume H₀ is true** and use the sampling distribution
4. Compute the p-value (probability of getting this result or worse, under H₀)
5. If p-value is small → reject H₀. If p-value is large → do not reject H₀.

---

## Setting Up Hypotheses

| Rule | Explanation |
|------|-------------|
| **H₀** = traditional belief, status quo | "Null" = nothing new |
| **H₁** = new claim, what you suspect | The alternative you accept if you reject H₀ |
| H₀ and H₁ must be **mutually exclusive** | Can't be both true at once |
| **More protection is given to H₀** | You need strong evidence to reject it |
| Rejecting H₀ → action required; Not rejecting → do nothing | |

---

## The P-Value: Its True Meaning 🔑

The p-value is the **probability of making a mistake** (Type 1 error):

> **P-value = P(getting a result this extreme or more extreme | H₀ is TRUE)**

**Decision rule:**
- If p-value < α (usually 0.05) → **reject H₀** (the mistake probability is small enough to be safe)
- If p-value ≥ α → **do not reject H₀** (the mistake probability is too high)

**Intuition from the hairdresser story:**
- H₀: The hairdresser did NOT cut your hair badly on purpose
- If p-value = 0.5 → "Even by chance this could happen," keep H₀
- If p-value = 0.005 → "This is too extreme to be just chance," reject H₀

---

## Test 1: Z-Test for Population Proportion (N large)

### When to use:
Comparing a sample proportion to a hypothesised value, with large n.

---

### Setup (AMI Heart Attack Example) 🔑

- Historical prevalence: p = 0.25 (null hypothesis)
- Suspect higher in City H: p > 0.25 (alternative)
- Sample: n = 500 people, X = 141 at high risk
- Sample proportion: p̂ = 141/500 = **0.282**

---

### Three Cases for the Alternative Hypothesis 🔑

| Case | H₁ | P-value calculation | Direction |
|------|----|--------------------|-----------|
| **Case 1** | p > p₀ | Right tail: P(Z > test stat) | Bigger → right |
| **Case 2** | p < p₀ | Left tail: P(Z < test stat) | Smaller → left |
| **Case 3** | p ≠ p₀ | Both tails: 2 × P(Z > |test stat|) | Not equal → both sides |

---

### Step-by-Step Calculation 🔑

**Step 1: State hypotheses**
- H₀: p = 0.25
- H₁: p > 0.25 (Case 1)

**Step 2: Compute standard error**

⚠️ **Use the NULL HYPOTHESIS value p₀ = 0.25, NOT p̂!** Common mistake!

$$SE = \sqrt{\frac{p_0(1 - p_0)}{n}} = \sqrt{\frac{0.25 \times 0.75}{500}} = \sqrt{0.000375} = 0.01936$$

**Step 3: Compute test statistic**

$$Z = \frac{\hat{p} - p_0}{SE} = \frac{0.282 - 0.25}{0.01936} = \frac{0.032}{0.01936} = 1.6525$$

**Step 4: Find p-value from normal table**

Case 1 (H₁: p > 0.25) → right tail:

- Look up Z = 1.65 in table → table value = 0.4505
- P(Z > 1.65) = 0.5 − 0.4505 = **0.0495**

**Step 5: Decision**

p-value = 0.049 < α = 0.05 → **Reject H₀**

Conclusion: Prevalence of high-risk AMI in City H is significantly higher than 25%.

---

### Linear Interpolation for More Accurate P-value 🔑

If Z = 1.6525 (between 1.65 and 1.66 in the table):

| Z | Table value |
|---|------------|
| 1.65 | 0.4505 |
| 1.66 | 0.4515 |

Proportion = (1.6525 − 1.65) / (1.66 − 1.65) = 0.0025/0.01 = **0.25**

Interpolated area = 0.4505 + 0.25 × (0.4515 − 0.4505) = 0.4505 + 0.00025 = **0.45075**

P-value (right tail) = 0.5 − 0.45075 = **0.04925**

---

### Case 2: Left-tail Test

If H₁: p < 0.25, p-value = P(Z < test stat)

Since distribution is symmetric:
$$P(Z < 1.65) = 0.5 + 0.4505 = 0.9505$$

**p-value = 0.95 > 0.05 → Do NOT reject H₀**

### Case 3: Two-tailed Test

If H₁: p ≠ 0.25, p-value = 2 × P(Z > |test stat|)

$$p\text{-value} = 2 \times 0.04925 = \mathbf{0.0985}$$

**p-value = 0.0985 > 0.05 → Do NOT reject H₀**

---

## How to "Cheat" with Statistics (and Why You Shouldn't) 🔑

The lecturer explicitly explained how people misuse hypothesis testing:

**The dishonest approach:**
1. Collect data
2. Run all three cases (H₁: >, H₁: <, H₁: ≠)
3. THEN choose the case that gives you the desired conclusion
4. Present only that case

**The honest approach:**
- **Decide the direction of H₁ BEFORE collecting data** and before running any calculations
- Once the direction is predetermined, you cannot manipulate the result

> "In statistics, fixing α = 0.05 BEFORE the test prevents manipulation of results to reach a more favorable outcome." — From slides

> The lecturer's candid comment: "In reality, everybody cheats... but you have to know how to cheat in order to prevent other people from cheating."

---

## Test 2: Small-Sample Binomial Test 🔑

When sample size is small, the normal approximation may not be good enough. Use the **exact binomial probability**.

### Stock Prediction Example (Example C from slides)

**Problem:** A trading firm claims their prediction accuracy is p = 0.8. Null hypothesis: p = 0.5 (coin flip, no skill).

- n = 10 trading days
- x = 9 correct predictions
- p̂ = 0.9

**H₀:** p = 0.5 (no better than chance)
**H₁:** p > 0.5 (they have skill)

---

### Calculating the P-value Using Binomial

P-value = P(X ≥ 9 | p = 0.5) = P(X = 9) + P(X = 10)

**P(winning 9 out of 10, with replacement, each win probability = 0.5):**

Using the binomial formula:

$$P(X = 9) = \binom{10}{9} \times 0.5^9 \times 0.5^1 = 10 \times 0.5^{10} = \frac{10}{1024}$$

Explanation:
- C(10,9) = 10 ways to choose which 9 of the 10 days are wins
- 0.5⁹ = probability of winning 9 times
- 0.5¹ = probability of losing 1 time

**P(winning all 10):**

$$P(X = 10) = \binom{10}{10} \times 0.5^{10} \times 0.5^0 = 1 \times 0.5^{10} = \frac{1}{1024}$$

**P-value = P(X ≥ 9) = (10 + 1) / 1024 = 11/1024 = 0.0107**

---

### Decision

p-value = 0.0107 < α = 0.05 → **Reject H₀**

**Conclusion:** The trading firm's prediction is better than a coin flip. Their probability is significantly higher than 0.5.

---

### Note on Why X ≥ p̂ for the P-value

For H₁: p > p₀, the p-value is:

$$p\text{-value} = P(\hat{p} \geq \text{observed } \hat{p} \mid H_0 \text{ true})$$

We look at "p̂ **or more extreme**" because:
- H₁ says p > p₀ → extreme values are high values
- If we observed 90% wins, anything **above** 90% is "more extreme"
- Therefore we calculate P(X ≥ 9 | p = 0.5)

---

## Beta (Type 2 Error) 🔑

**β = P(Type 2 Error) = P(failing to reject H₀ when H₁ is true)**

For the stock prediction example:
$$\beta = P(\hat{p} < \text{observed } \hat{p} \mid p = p_1)$$

$$= P(X < 9 \mid p = 0.8) = 1 - P(X \geq 9 \mid p = 0.8)$$

**Key relationships:**
- α (Type 1 error) and β (Type 2 error) have a **trade-off**: decreasing α increases β
- The only way to reduce **both** simultaneously: **increase sample size n**

| Reject Region | α | β |
|--------------|---|---|
| X ≥ 8 | 0.0547 | 0.3222 |
| X ≥ 9 | 0.0107 | 0.6242 |

> More stringent rejection region (X ≥ 9) makes α smaller but β larger.

---

## Z-Test for Population Mean (Alternative Form)

The same concept applies to testing a population mean:

$$Z = \frac{\bar{Y} - \mu_0}{\sigma/\sqrt{n}}$$

Where μ₀ is the null hypothesis value for the population mean.

**Example D from slides:** Testing if a new drug helps patients recover faster.
- H₀: p = 0.6 (standard recovery rate)
- H₁: p > 0.6 (new drug is better)
- n = 100, x = 70, p̂ = 0.70
- Z = (0.70 − 0.60) / √(0.6×0.4/100) = 0.10 / 0.04899 = **2.04**
- P-value = P(Z > 2.04) = 0.5 − 0.4793 = **0.0207**
- Since 0.0207 < 0.05 → reject H₀ → new drug is more effective ✓

---

## Full Summary Procedure 🔑

```
1. BEFORE collecting data:
   → State H₀: p = p₀
   → State H₁: p > p₀  OR  p < p₀  OR  p ≠ p₀
   → Set significance level α = 0.05

2. Collect data, compute:
   → p̂ = X/n   (sample proportion)

3. Compute standard error using H₀ value:
   → SE = √(p₀(1−p₀)/n)

4. Compute test statistic:
   → Z = (p̂ − p₀) / SE

5. Find p-value:
   → H₁: p > p₀  →  p-value = P(Z > test stat)  [right tail]
   → H₁: p < p₀  →  p-value = P(Z < test stat)  [left tail]
   → H₁: p ≠ p₀  →  p-value = 2 × P(Z > |test stat|)  [both tails]

6. Make decision:
   → p-value < α  →  Reject H₀
   → p-value ≥ α  →  Do NOT reject H₀
```

---

## The P-value Interpretation in Plain English

| P-value | Interpretation |
|---------|----------------|
| Very small (e.g., 0.001) | Almost impossible to get this result by chance → very strong evidence against H₀ → reject H₀ |
| Small (e.g., 0.03, < 0.05) | Unlikely by chance → enough evidence to reject H₀ |
| Moderate (e.g., 0.10, > 0.05) | Plausible by chance → not enough evidence → do not reject H₀ |
| Large (e.g., 0.95) | Very likely by chance → data strongly consistent with H₀ → do not reject H₀ |

---

## Quick Reference: All Key Formulas

| Symbol | Meaning | Where used |
|--------|---------|------------|
| p₀ | Null hypothesis proportion | H₀: p = p₀ |
| p̂ | Sample proportion = X/n | Observed data |
| SE | Standard error = √(p₀(1−p₀)/n) | Uses **p₀** not p̂! |
| Z | Test statistic = (p̂ − p₀) / SE | From calculating Z-score |
| p-value | Probability of result this extreme under H₀ | From Z table or binomial |
| α | Significance level (usually 0.05) | Set BEFORE the test |
| β | P(Type 2 error) = P(fail to reject H₀ | H₁ true) | Related to power |
| Power | 1 − β | P(correctly reject H₀ when H₁ true) |

---

## Differences from Ch5 (Confidence Intervals)

| Concept | Confidence Interval | Hypothesis Testing |
|---------|--------------------|--------------------|
| Goal | Estimate the parameter | Test a claimed value |
| Formula | p̂ ± 1.96 × SE (uses p̂ in SE) | Z = (p̂ − p₀) / SE (uses **p₀** in SE!) |
| Output | A range of values | A yes/no decision |

> **Critical difference:** In CI, the SE uses the **sample proportion p̂**. In hypothesis testing, the SE uses the **null hypothesis value p₀**. Students commonly confuse these!

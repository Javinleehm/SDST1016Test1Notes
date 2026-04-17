# Chapter 6: Hypothesis Testing

> **Test coverage:** This chapter will be covered in Test 2. Expect calculation questions on test statistics, p-values, and conclusions.

---

## 6A: Introduction to Hypothesis Testing

### What is Hypothesis Testing?

Hypothesis testing is a statistical method used to make decisions about a population based on sample data. It helps us determine whether observed differences are **statistically significant** or just due to random chance.

### Key Terminology

| Term | Definition | Example |
|------|-----------|---------|
| **Null Hypothesis (H₀)** | The default assumption; usually states "no effect," "no difference," or "no change" | The heart attack rate is 25% |
| **Alternative Hypothesis (H₁ or Hₐ)** | What we're trying to prove; the opposite of H₀ | The heart attack rate is MORE than 25% |
| **Test Statistic** | A calculated value used to decide whether to reject H₀ | Z = 1.6525 |
| **p-value** | Probability of making a mistake if we reject H₀ | 0.04925 |
| **Significance Level (α)** | The threshold for deciding; usually 5% (0.05) | α = 0.05 |
| **Type 1 Error (α)** | Rejecting H₀ when H₀ is actually true | False positive |
| **Type 2 Error (β)** | Failing to reject H₀ when H₁ is actually true | False negative |
| **Power** | 1 − β; probability of correctly rejecting H₀ when H₁ is true | 0.38 |

---

## 6B: The Three Cases of Alternative Hypothesis 🔑🔑🔑

This is **extremely important** for the test. The null hypothesis is always the same, but the alternative hypothesis can take **three different forms**, and each leads to a **different conclusion**.

### Case 1: Right-Tailed Test (Greater Than)

$$H_0: p = 0.25$$
$$H_1: p > 0.25$$

**Question:** Is the heart attack rate **higher** than 25%?

### Case 2: Left-Tailed Test (Less Than)

$$H_0: p = 0.25$$
$$H_1: p < 0.25$$

**Question:** Is the heart attack rate **lower** than 25%?

### Case 3: Two-Tailed Test (Not Equal To)

$$H_0: p = 0.25$$
$$H_1: p \neq 0.25$$

**Question:** Is the heart attack rate **different** from 25% (could be higher OR lower)?

> **Critical point:** The same data can lead to **different conclusions** depending on which case you choose. This is why you must **decide the case BEFORE doing calculations** — otherwise, you could cheat by picking the case that gives your desired result.

---

## 6C: Step-by-Step Procedure for Hypothesis Testing (Proportion)

### Example: Heart Attack Rate

**Scenario:** Doctors believe 25% of the population is susceptible to heart attacks. But we suspect the rate might be higher due to modern lifestyle. We test 500 people and find 141 have a high chance of heart attack.

### Step 1: State the Hypotheses

$$H_0: p = 0.25$$
$$H_1: p > 0.25 \quad \text{(Case 1: right-tailed)}$$

### Step 2: Calculate the Sample Proportion

$$\hat{p} = \frac{141}{500} = 0.282 = 28.2\%$$

### Step 3: Calculate the Standard Error

$$SE = \sqrt{\frac{p \times (1-p)}{n}} = \sqrt{\frac{0.25 \times 0.75}{500}} = \sqrt{\frac{0.1875}{500}} = \sqrt{0.000375} = 0.01936$$

> **⚠️ Common mistake:** Use the **null hypothesis value** (p = 0.25), NOT the sample proportion (p̂ = 0.282) when calculating the standard error. This is because hypothesis testing assumes H₀ is true.

### Step 4: Calculate the Test Statistic

$$Z = \frac{\hat{p} - p}{SE} = \frac{0.282 - 0.25}{0.01936} = \frac{0.032}{0.01936} = 1.6525$$

### Step 5: Find the p-value

For Case 1 (right-tailed), the p-value is the **area to the right** of Z = 1.6525.

Using the normal table with linear interpolation:
- Z = 1.65 → main area = 0.4505
- Z = 1.66 → main area = 0.4515
- Interpolated main area = 0.45075
- **Right tail (p-value)** = 0.5 − 0.45075 = **0.04925**

Using Excel (most accurate):
```
=1 - NORM.S.DIST(1.6525, TRUE)
```
Result: **0.04925** (approximately)

### Step 6: Compare p-value to Significance Level

- p-value = 0.04925
- Significance level α = 0.05 (5%)
- **0.04925 < 0.05** → p-value is less than α

### Step 7: Draw Conclusion

**Rule:**
- If p-value < α → **Reject H₀**
- If p-value ≥ α → **Cannot reject H₀**

Since 0.04925 < 0.05, we **reject H₀**.

**Conclusion:** There is sufficient evidence to conclude that the heart attack rate is **higher than 25%**.

---

## 6D: Understanding the p-value 🔑🔑🔑

### What Does the p-value Actually Mean?

The p-value is **the probability of making a mistake** if you reject the null hypothesis.

More precisely:
> **p-value = P(reject H₀ | H₀ is true)**

The "mistake" is: **H₀ is true, but you reject it anyway.**

### Interpreting the p-value

| p-value | Interpretation | Action |
|---------|---------------|--------|
| Very small (< 0.05) | Probability of making a mistake is very small → It's probably NOT a mistake | **Reject H₀** |
| Large (≥ 0.05) | Probability of making a mistake is large → It probably IS a mistake | **Cannot reject H₀** |

### Intuitive Explanation

Think of it this way:
- p-value = 0.04925 means there's only a **4.925% chance** that we'd be wrong if we reject H₀
- That's less than 5%, which we consider "small enough"
- So we say: "The probability of being wrong is so small, let's go ahead and reject H₀"

---

## 6E: All Three Cases Worked Out

Using the same data (n = 500, 141 heart attack susceptible, p̂ = 0.282, Z = 1.6525):

### Case 1: H₁: p > 0.25 (Right-tailed)

- p-value = area to the **right** of Z = 1.6525
- p-value = **0.04925**
- 0.04925 < 0.05 → **Reject H₀**
- **Conclusion:** Heart attack rate is higher than 25%

### Case 2: H₁: p < 0.25 (Left-tailed)

- p-value = area to the **left** of Z = 1.6525
- p-value = 1 − 0.04925 = **0.95075**
- 0.95075 > 0.05 → **Cannot reject H₀**
- **Conclusion:** No evidence that heart attack rate is lower than 25%

### Case 3: H₁: p ≠ 0.25 (Two-tailed)

- p-value = area in **both tails** = 2 × 0.04925 = **0.0985**
- 0.0985 > 0.05 → **Cannot reject H₀**
- **Conclusion:** No evidence that heart attack rate is different from 25%

> **Key insight:** The same data gives three different conclusions! This is why you must choose your alternative hypothesis **before** looking at the data.

---

## 6F: How to "Cheat" in Statistics (And How to Prevent It) 🔑

### The Cheat

If you want a specific conclusion, you can **choose the alternative hypothesis** that gives you the result you want:

| Desired Conclusion | Choose This H₁ |
|-------------------|----------------|
| "Rate is higher" | H₁: p > 0.25 |
| "Rate hasn't changed" | H₁: p < 0.25 or H₁: p ≠ 0.25 |

**Real-world example:** If a government official wants to show that heart attack rates haven't increased (to avoid spending money on prevention), they would choose Case 2 or Case 3, which both lead to "cannot reject H₀."

### The Prevention

To prevent cheating, statistics requires you to:
1. **State your hypotheses BEFORE collecting data**
2. **State your hypotheses BEFORE doing any calculations**
3. Only then proceed with the test

This way, you can't look at the data first and then choose the hypothesis that gives your desired result.

---

## 6G: Binomial Hypothesis Testing (Small Sample) 🔑🔑🔑

### When to Use Binomial Instead of Normal

When the sample size is **small**, the normal approximation may not be accurate. In these cases, we use the **exact binomial calculation**.

### Example: Stock Trader

**Scenario:** A stock trader claims he can beat the market. The null hypothesis is that his predictions are no better than a coin flip (50-50). The alternative is that he's better than 50-50 (say, 80% accuracy).

We observe 10 trades, and he gets 9 correct (90% accuracy).

### Step 1: State the Hypotheses

$$H_0: p = 0.5 \quad \text{(coin flip, no skill)}$$
$$H_1: p > 0.5 \quad \text{(better than coin flip)}$$

More specifically, the trader claims p = 0.8.

### Step 2: Define the Rejection Criterion

We reject H₀ if the sample proportion is **p̂ or more**, where p̂ = 9/10 = 0.9.

That means: reject H₀ if we observe **9 or more winning trades out of 10**.

### Step 3: Calculate the p-value Using Binomial Formula

The p-value is:

$$P(\text{9 or more wins} \mid p = 0.5)$$

$$= P(\text{exactly 9 wins}) + P(\text{exactly 10 wins})$$

Using the binomial formula:

$$P(X = k) = \binom{n}{k} \times p^k \times (1-p)^{n-k}$$

**For exactly 9 wins:**

$$P(X = 9) = \binom{10}{9} \times (0.5)^9 \times (0.5)^1 = 10 \times 0.001953 \times 0.5 = 0.009766$$

**For exactly 10 wins:**

$$P(X = 10) = \binom{10}{10} \times (0.5)^{10} \times (0.5)^0 = 1 \times 0.000977 \times 1 = 0.000977$$

**Total p-value:**

$$p\text{-value} = 0.009766 + 0.000977 = 0.01074 = 1.07\%$$

### Step 4: Conclusion

- p-value = 0.0107 = 1.07%
- α = 0.05 = 5%
- 1.07% < 5% → **Reject H₀**

**Conclusion:** The trader's performance is significantly better than a coin flip. There is evidence that he has genuine prediction skill.

---

## 6H: Type 2 Error (β) and Power 🔑

### Type 2 Error (Beta)

While the p-value measures Type 1 error (rejecting H₀ when it's true), **beta (β)** measures Type 2 error:

> **β = P(fail to reject H₀ | H₁ is true)**

The "mistake" for Type 2 error is: **H₁ is true, but you fail to reject H₀.**

### Calculating Beta

Using the stock trader example:
- H₀: p = 0.5
- H₁: p = 0.8 (the trader's claimed accuracy)
- We reject H₀ if we get 9 or more wins
- We fail to reject H₀ if we get **less than 9 wins** (i.e., 8 or fewer)

$$\beta = P(\text{8 or fewer wins} \mid p = 0.8)$$

$$= 1 - P(\text{9 or more wins} \mid p = 0.8)$$

$$= 1 - [P(X=9 \mid p=0.8) + P(X=10 \mid p=0.8)]$$

$$P(X=9 \mid p=0.8) = \binom{10}{9} \times (0.8)^9 \times (0.2)^1 = 10 \times 0.1342 \times 0.2 = 0.2684$$

$$P(X=10 \mid p=0.8) = \binom{10}{10} \times (0.8)^{10} \times (0.2)^0 = 1 \times 0.1074 \times 1 = 0.1074$$

$$\beta = 1 - (0.2684 + 0.1074) = 1 - 0.3758 = 0.6242 = 62.42\%$$

### Power of the Test

$$\text{Power} = 1 - \beta = 1 - 0.6242 = 0.3758 = 37.58\%$$

**Interpretation:**
- **Type 1 error (α):** 1.07% — very low
- **Type 2 error (β):** 62.42% — very high
- **Power:** 37.58% — quite low

### The Trade-off 🔑

There is always a **trade-off** between Type 1 and Type 2 errors:

| Situation | Type 1 Error (α) | Type 2 Error (β) | Power |
|-----------|-----------------|-----------------|-------|
| Very strict criteria | Low | High | Low |
| Very lenient criteria | High | Low | High |

> **In economics terms:** The **opportunity cost** of a low Type 1 error is a high Type 2 error. You can't minimize both simultaneously.

---

## 6I: Paired Comparison (Paired t-test) 🔑

### Example: Insomnia Medication

**Scenario:** 12 patients are tested with and without a new sleep medication. We want to know if the medication is effective.

| Patient | No Medication (hrs) | With Medication (hrs) | Difference |
|---------|--------------------|--------------------|------------|
| 1 | 1.3 | 2.9 | 1.6 |
| 2 | 1.5 | 3.0 | 1.5 |
| 3 | 1.8 | 2.9 | 1.1 |
| ... | ... | ... | ... |
| 12 | ... | ... | ... |

### Step 1: State the Hypotheses

$$H_0: \mu_d = 0 \quad \text{(no difference — medication has no effect)}$$
$$H_1: \mu_d > 0 \quad \text{(positive difference — medication helps you sleep more)}$$

Where μ_d is the **population mean of the differences**.

> **Why zero in H₀?** In hypothesis testing, the null hypothesis always represents the **skeptical/pessimistic view**: "there's no effect," "there's no improvement," "there's no difference."

### Step 2: Calculate the Sample Mean of Differences

$$\bar{d} = \frac{\sum d_i}{n} = 1.4 \text{ hours (from the data)}$$

### Step 3: Calculate the Standard Error

Given: population standard deviation of differences σ = 1.5

$$SE = \frac{\sigma}{\sqrt{n}} = \frac{1.5}{\sqrt{12}} = \frac{1.5}{3.464} = 0.433$$

### Step 4: Calculate the Test Statistic

$$Z = \frac{\bar{d} - \mu_0}{SE} = \frac{1.4 - 0}{0.433} = 3.23$$

### Step 5: Find the p-value

For Z = 3.23 (right-tailed):

Using the normal table:
- Z = 3.23 → main area ≈ 0.4994
- Right tail = 0.5 − 0.4994 = **0.0006**

### Step 6: Conclusion

- p-value = 0.0006
- α = 0.05
- 0.0006 < 0.05 → **Reject H₀**

**Conclusion:** The medication is effective. There is strong evidence that the medication increases sleep hours.

---

## 6J: The Raven Paradox (Conceptual Question) 🔑

### The Question

**Null hypothesis:** All finance professionals are data science majors. (A → B)

Which observation supports the null hypothesis?

**Answer A:** An English literature major who is a teacher.

### The Logic

By **contrapositive** (a fundamental logic rule):
- If A → B, then **not B → not A**
- "If you're a finance professional, then you're a data science major" is equivalent to "If you're NOT a data science major, then you're NOT a finance professional"

An English literature major who is a teacher:
- Is NOT a data science major (not B) ✓
- Is NOT a finance professional (not A) ✓
- This confirms "not B → not A," which is equivalent to "A → B"

### Why "Teacher" is Relevant

Some students argue: "Is 'teacher' relevant to this question?"

**Answer:** Yes, it's relevant. The alternative hypothesis is "not all finance professionals are data science majors," which means some finance professionals could be something else (like a teacher). So a teacher who is not a data science major is a valid observation.

### Even If You Argue "Teacher is Irrelevant"

Even if you claim the teacher observation is irrelevant:
- In hypothesis testing, you **must maintain H₀** if you don't have strong evidence to reject it
- Irrelevant evidence = not enough evidence = cannot reject H₀
- So you still accept the null hypothesis

> **Key principle:** In hypothesis testing, the null hypothesis has a much stronger standing. You must keep it unless you have strong, relevant evidence to reject it.

---

## Quick Reference: Formulas Summary

| Concept | Formula |
|---------|---------|
| Standard Error (proportion) | SE = √[p(1−p)/n] |
| Test Statistic (proportion) | Z = (p̂ − p) / SE |
| Test Statistic (mean) | Z = (x̄ − μ) / (σ/√n) |
| Standard Error (mean) | SE = σ/√n |
| Binomial probability | P(X=k) = C(n,k) × pᵏ × (1−p)ⁿ⁻ᵏ |
| p-value interpretation | P(reject H₀ \| H₀ is true) |
| Type 2 error | β = P(fail to reject H₀ \| H₁ is true) |
| Power | Power = 1 − β |
| Decision rule | If p-value < α → Reject H₀ |

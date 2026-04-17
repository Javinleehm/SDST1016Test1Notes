# Chapter 7: Regression Analysis (7A + 7B)

> **Test coverage:** This chapter will be covered in Test 2. Expect both conceptual questions (Simpson's Paradox, Anscombe's Quartet) and calculation questions (Logistic Regression, odds ratio).

---

## 7A: Linear Regression — Important Observations

### Simpson's Paradox 🔑🔑🔑

#### What is Simpson's Paradox?

**Simpson's Paradox** occurs when the trend observed in individual subgroups is **completely opposite** to the trend observed when all groups are combined.

#### The Course Study Example

Imagine we're studying the relationship between:
- **X-axis:** Number of hours studied
- **Y-axis:** Exam result (CGPA)

We have data from multiple courses:
- **Physical Education** (pink dots) — easy course
- **Art** (blue dots) — moderate difficulty
- **Social Studies** (green dots) — harder
- **English** (orange dots) — even harder
- **Algebra** (red dots) — hardest course

**What we observe:**

| Level | Trend | Interpretation |
|-------|-------|---------------|
| **Individual courses** | Upward sloping | More study → better results (as expected) |
| **All courses combined** | Downward sloping | More study → worse results (counterintuitive!) |

#### Why Does This Happen?

The answer lies in a **hidden variable** (also called a **confounding variable**):

> **The level of difficulty of the course.**

- Easy courses (like PE): Students get high grades with relatively little study
- Hard courses (like Algebra): Even with lots of study, grades are lower

When you combine all courses:
- Students studying many hours are mostly taking hard courses → lower grades
- Students studying few hours are mostly taking easy courses → higher grades

This creates an **overall downward trend**, even though within each individual course, more study leads to better results.

#### The Lesson

> **Never look at just two variables.** Always consider whether there might be a **confounding variable** (third variable) that affects the relationship between your X and Y.

**Key terms:**
- **Confounding variable** = Hidden variable = Lurking variable
- These are the same concepts we saw in Chapter 1 (Simpson's Paradox in hospital data)

---

### Anscombe's Quartet 🔑🔑🔑

#### What is Anscombe's Quartet?

**Anscombe's Quartet** is a set of **four completely different datasets** that produce **exactly the same linear regression line**.

#### The Four Datasets

| Dataset | Visual Pattern |
|---------|---------------|
| Dataset 1 | Normal linear relationship with some scatter |
| Dataset 2 | Curved (non-linear) relationship |
| Dataset 3 | Perfect linear relationship with one outlier |
| Dataset 4 | One outlier drives the entire regression |

#### The Shocking Result

Despite looking completely different, all four datasets give:
- **Same regression line** (same slope, same intercept)
- **Same R² value**
- **Same correlation coefficient**

#### The Lesson

> **Never just look at the regression line.** Always visualize your data points alongside the regression line.

The regression line alone can be **misleading**. You must check:
1. Are the data points actually linear?
2. Are there outliers distorting the line?
3. Is the relationship actually curved?

---

## 7B: Logistic Regression (Nonlinear Regression) 🔑🔑🔑

### The Problem with Linear Regression for Binary Outcomes

#### The Scenario

We want to predict whether someone has **lung cancer** based on **years of smoking**.

- **X-axis:** Years of smoking
- **Y-axis:** 0 = no cancer, 1 = has cancer (binary outcome)

#### Problem 1: Predicting "0.4 Cancer"

If we fit a linear regression line and someone has smoked for 5 years, the line might predict Y = 0.4.

But what does "0.4 cancer" mean? You either have cancer or you don't!

**Solution:** Interpret 0.4 as the **probability of having cancer**. So 0.4 means a 40% chance of having lung cancer.

#### Problem 2: Negative Probabilities and Probabilities > 1

If someone smoked for only 1 year, the linear regression line might predict Y = −0.1.
- **Probability cannot be negative!**

If someone smoked for 50 years, the line might predict Y = 1.1.
- **Probability cannot exceed 1!**

**No straight line can solve this problem.** No matter how you bend or tilt a straight line, it will always go outside the [0, 1] range at some point.

#### The Solution: Use a Curve (S-shaped / Sigmoid)

We need a **nonlinear regression** — specifically, a **logistic regression** — that produces an **S-shaped curve** that stays between 0 and 1.

---

### The Logistic Regression Formula 🔑

$$P(\text{cancer}) = \frac{e^{\beta_0 + \beta_1 X}}{1 + e^{\beta_0 + \beta_1 X}}$$

Where:
- **X** = number of years of smoking (explanatory variable)
- **β₀** (beta naught / beta 0) = intercept parameter
- **β₁** (beta 1) = slope parameter
- **e** = Euler's number ≈ 2.71828 (base of natural logarithm)
- **EXP** = exponential function = e raised to the power of (...)

> **Note:** β₀ and β₁ are estimated by computer algorithms (Python, R). You cannot calculate them by hand. In tests, these values will be given to you.

#### Example Values

Suppose β₀ = −3.4 and β₁ = 0.0365.

For someone who smoked 50 years:

$$P(\text{cancer}) = \frac{e^{-3.4 + 0.0365 \times 50}}{1 + e^{-3.4 + 0.0365 \times 50}} = \frac{e^{-1.575}}{1 + e^{-1.575}} = \frac{0.207}{1.207} = 0.171$$

So this person has approximately a 17.1% probability of having lung cancer.

---

### Log Odds Ratio 🔑🔑🔑

#### What is the Log Odds Ratio?

The **log odds ratio** compares the odds of cancer between two individuals:

$$\text{Log Odds Ratio} = \beta_1 \times (X_i - X_j)$$

Where:
- **Xᵢ** = years of smoking for individual i
- **Xⱼ** = years of smoking for individual j
- **β₁** = the slope parameter from the logistic regression

#### From Log Odds Ratio to Odds Ratio

To eliminate the log and get the **odds ratio**, take the exponential:

$$\text{Odds Ratio} = e^{\beta_1 \times (X_i - X_j)} = \text{EXP}(\beta_1 \times (X_i - X_j))$$

#### Interpreting the Odds Ratio

The odds ratio tells you the **percentage increase in the probability of cancer** when going from individual j to individual i.

**Formula for percentage increase:**

$$\text{Percentage Increase} = (\text{Odds Ratio} - 1) \times 100\%$$

---

### Worked Examples

#### Example 1: 1 Year vs. 0 Years (Non-smoker)

- Individual i: smoked 1 year (Xᵢ = 1)
- Individual j: non-smoker (Xⱼ = 0)
- β₁ = 0.0365

**Step 1: Calculate log odds ratio**

$$\text{Log Odds Ratio} = 0.0365 \times (1 - 0) = 0.0365$$

**Step 2: Calculate odds ratio**

$$\text{Odds Ratio} = e^{0.0365} = 1.0372$$

**Step 3: Interpret**

$$\text{Percentage Increase} = (1.0372 - 1) \times 100\% = 3.72\%$$

**Conclusion:** Going from 0 years to 1 year of smoking increases the probability of cancer by **3.72%**.

---

#### Example 2: 5 Years vs. 0 Years

- Xᵢ = 5, Xⱼ = 0

$$\text{Log Odds Ratio} = 0.0365 \times (5 - 0) = 0.1825$$

$$\text{Odds Ratio} = e^{0.1825} = 1.2002$$

$$\text{Percentage Increase} = (1.2002 - 1) \times 100\% = 20.02\%$$

**Conclusion:** Going from 0 to 5 years of smoking increases the probability of cancer by **20.02%**.

---

#### Example 3: 50 Years vs. 0 Years (Lifelong Smoker)

- Xᵢ = 50, Xⱼ = 0

$$\text{Log Odds Ratio} = 0.0365 \times (50 - 0) = 1.825$$

$$\text{Odds Ratio} = e^{1.825} = 6.2028$$

$$\text{Percentage Increase} = (6.2028 - 1) \times 100\% = 520.28\%$$

**Conclusion:** A lifelong smoker (50 years) has a **520.28% higher** probability of cancer compared to a non-smoker — that's more than **6 times** the risk.

---

### Summary Table

| Comparison | Log Odds Ratio | Odds Ratio | % Increase in Cancer Probability |
|-----------|---------------|------------|----------------------------------|
| 1 year vs. 0 years | 0.0365 | 1.0372 | +3.72% |
| 5 years vs. 0 years | 0.1825 | 1.2002 | +20.02% |
| 10 years vs. 0 years | 0.3650 | 1.4405 | +44.05% |
| 20 years vs. 0 years | 0.7300 | 2.0751 | +107.51% |
| 50 years vs. 0 years | 1.8250 | 6.2028 | +520.28% |

---

### Key Points for the Test

1. **Given β₀ and β₁**, you can calculate the probability of cancer for any number of years smoked
2. **Given β₁ and two individuals' smoking years**, you can calculate the log odds ratio, odds ratio, and percentage increase
3. **Remember:** EXP means e raised to the power of the value
4. **Interpretation:** Odds ratio of 1.0372 means a 3.72% increase (subtract 1, then multiply by 100%)

---

## Supervised vs. Unsupervised Learning 🔑

### The Key Difference

| Aspect | Supervised Learning | Unsupervised Learning |
|--------|-------------------|----------------------|
| **Equation/Model** | Has an equation (e.g., regression) | No equation |
| **True Labels** | Has true labels (actual observations) | No true labels |
| **Prediction Verification** | Can compare predictions to actual outcomes | Cannot verify predictions |
| **Examples** | Linear regression, logistic regression, decision tree | Clustering, hierarchical clustering |

### What Are "True Labels"?

**True labels** = the actual, observed outcomes in your data.

**Example:** In the lung cancer study:
- You predict whether Eric has cancer (prediction)
- You then check whether Eric actually has cancer (true label)
- If prediction matches true label → accurate prediction

> **Supervised learning** = your learning is "supervised" by the true labels. You can check if you're right or wrong.

> **Unsupervised learning** = no true labels to guide you. You can only group similar things together without knowing if the grouping is "correct."

### Connection to Equations

Having an equation is equivalent to having true labels:
- If you have an equation → you used true labels to estimate it → supervised
- If you have no equation → no true labels were used → unsupervised

---

## Quick Reference: Formulas Summary

| Concept | Formula |
|---------|---------|
| Logistic regression probability | P = e^(β₀ + β₁X) / (1 + e^(β₀ + β₁X)) |
| Log odds ratio | β₁ × (Xᵢ − Xⱼ) |
| Odds ratio | e^(β₁ × (Xᵢ − Xⱼ)) |
| Percentage increase | (Odds Ratio − 1) × 100% |
| Log base 2 calculation | log₂(x) = log₁₀(x) / log₁₀(2) |

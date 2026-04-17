# Chapter 9: Machine Learning Models — Decision Tree

> **Test coverage:** This chapter will be covered in Test 2. Expect calculation questions on entropy and choosing the best split. Conceptual questions on KNN and K-means clustering.

---

## 9A: What is a Decision Tree? 🔑🔑🔑

### The Concept

A **decision tree** is a supervised machine learning model that makes predictions by asking a series of yes/no questions. Each question splits the data into two groups, and we keep splitting until we can make an accurate prediction.

### The Dataset

We have 14 workers with the following information:

| # | Sex | Age | Occupation | Target (1=Happy, 2=Unhappy) |
|---|-----|-----|------------|----------------------------|
| 1 | M | 25 | A | 1 |
| 2 | M | 45 | A | 2 |
| 3 | F | 35 | B | 1 |
| 4 | M | 30 | C | 1 |
| 5 | F | 20 | B | 1 |
| 6 | M | 40 | C | 2 |
| 7 | F | 35 | B | 1 |
| 8 | F | 50 | A | 2 |
| 9 | M | 25 | B | 1 |
| 10 | F | 30 | C | 1 |
| 11 | M | 45 | A | 2 |
| 12 | F | 35 | B | 1 |
| 13 | M | 40 | C | 2 |
| 14 | F | 25 | A | 1 |

**Summary:**
- Target 1 (Happy): 9 people
- Target 2 (Unhappy): 5 people
- Total: 14 people

### The Goal

Given a new person (e.g., Female, age 28, occupation B), predict whether they are happy (1) or unhappy (2).

### Is This Supervised or Unsupervised?

**Supervised learning** — because we have the **true labels** (the Target column). We can compare our predictions against the actual outcomes to see if we're correct.

---

## 9B: How Decision Trees Work

### The Splitting Process

The tree works by asking **binary (yes/no) questions** to split the data:

```
Root: Is Occupation = B?
├── YES → Predict: Happy (1) [100% accurate — all B's are happy!]
└── NO → Need to split further...
    └── Is Sex = Male?
        ├── YES → Predict: Unhappy (2) [majority vote: 3 out of 4 are unhappy]
        └── NO → Predict: Happy (1) [majority vote: 5 out of 6 are happy]
```

### The $1 Million Question: How Do You Choose the Split?

There are many possible splits:
- **Sex:** Male vs. Female (only 1 split needed since it's binary)
- **Age:** ≤20, ≤25, ≤30, ≤35, ≤40, ≤45, ≤50 (many possible splits)
- **Occupation:** =A?, =B?, =C? (3 separate splits needed)

**The answer:** We choose the split that gives the **lowest entropy** (lowest randomness).

---

## 9C: Entropy — Measuring Randomness 🔑🔑🔑

### What is Entropy?

**Entropy** measures the level of randomness/disorder in a system.

- **Maximum entropy = 1:** Total randomness (50-50 split — you know nothing)
- **Minimum entropy = 0:** No randomness (all the same — perfect prediction)

### The Entropy Formula

For a binary target with proportions p₁ and p₂:

$$\text{Entropy} = -p_1 \times \log_2(p_1) - p_2 \times \log_2(p_2)$$

> **⚠️ Don't forget the minus sign!** The log of a proportion is negative, so the minus sign makes the entropy positive.

### How to Calculate log₂ on a Calculator

Most calculators don't have log base 2. Use this formula:

$$\log_2(x) = \frac{\log_{10}(x)}{\log_{10}(2)} = \frac{\log(x)}{\log(2)}$$

You can use any base (base 10 or base e), as long as you're consistent.

### Special Case: 0 × log(0) = 0

When a proportion is 0, you get 0 × log(0), which is technically 0 × (−∞) = undefined.

**Convention:** We define **0 × log(0) = 0**.

---

## 9D: Step-by-Step Entropy Calculation

### Step 1: Calculate Root Entropy (Whole System)

Target distribution:
- Target 1 (Happy): 9 out of 14 → p₁ = 9/14
- Target 2 (Unhappy): 5 out of 14 → p₂ = 5/14

$$\text{Entropy}_{\text{root}} = -\frac{9}{14} \times \log_2\left(\frac{9}{14}\right) - \frac{5}{14} \times \log_2\left(\frac{5}{14}\right)$$

$$= -0.6429 \times \log_2(0.6429) - 0.3571 \times \log_2(0.3571)$$

$$= -0.6429 \times (-0.6374) - 0.3571 \times (-1.4855)$$

$$= 0.4098 + 0.5305 = \mathbf{0.9403}$$

**Interpretation:** The root entropy is 0.9403, very close to 1. This means the whole system is very random — we need splits to reduce this randomness.

---

### Step 2: Calculate Entropy for Each Possible Split

#### Split by Sex (Male vs. Female)

**Frequency table:**

| | Target 1 (Happy) | Target 2 (Unhappy) | Subtotal |
|---|---|---|---|
| **Male** | 3 | 3 | 6 |
| **Female** | 6 | 2 | 8 |
| **Total** | 9 | 5 | 14 |

> **Check:** 6 + 8 = 14 = sample size ✓ (If this doesn't add up, you made a counting error!)

**Proportions:**
- Male: p₁ = 3/6 = 1/2, p₂ = 3/6 = 1/2
- Female: p₁ = 6/8 = 3/4, p₂ = 2/8 = 1/4

**Entropy for Male:**

$$\text{Entropy}_M = -\frac{1}{2} \times \log_2\left(\frac{1}{2}\right) - \frac{1}{2} \times \log_2\left(\frac{1}{2}\right)$$

$$= -0.5 \times (-1) - 0.5 \times (-1) = 0.5 + 0.5 = \mathbf{1.0}$$

> **Key insight:** When proportions are equal (50-50), entropy is maximum (= 1). This means maximum randomness — if you're male, you're equally likely to be happy or unhappy, so you know nothing.

**Entropy for Female:**

$$\text{Entropy}_F = -\frac{3}{4} \times \log_2\left(\frac{3}{4}\right) - \frac{1}{4} \times \log_2\left(\frac{1}{4}\right)$$

$$= -0.75 \times (-0.4150) - 0.25 \times (-2) = 0.3113 + 0.5 = \mathbf{0.8113}$$

**Weighted Average (Total Entropy for Sex Split):**

$$\text{Entropy}_{\text{sex}} = \frac{6}{14} \times 1.0 + \frac{8}{14} \times 0.8113 = 0.4286 + 0.4636 = \mathbf{0.8922}$$

**Improvement:** Root entropy (0.9403) → Sex split entropy (0.8922). Some improvement, but is it the best?

---

#### Split by Age (≤33 vs. >33)

There are many possible age splits. We'll use 33 as a shortcut because it seems to separate most Target 1's (younger) from Target 2's (older).

**Frequency table:**

| | Target 1 (Happy) | Target 2 (Unhappy) | Subtotal |
|---|---|---|---|
| **Age ≤ 33** | 5 | 1 | 6 |
| **Age > 33** | 4 | 4 | 8 |
| **Total** | 9 | 5 | 14 |

**Proportions:**
- Age ≤ 33: p₁ = 5/6, p₂ = 1/6
- Age > 33: p₁ = 4/8 = 1/2, p₂ = 4/8 = 1/2

**Entropy for Age ≤ 33:**

$$\text{Entropy}_{\leq 33} = -\frac{5}{6} \times \log_2\left(\frac{5}{6}\right) - \frac{1}{6} \times \log_2\left(\frac{1}{6}\right)$$

$$= -0.8333 \times (-0.2630) - 0.1667 \times (-2.5850) = 0.2192 + 0.4308 = \mathbf{0.6500}$$

**Entropy for Age > 33:**

$$\text{Entropy}_{> 33} = -\frac{1}{2} \times \log_2\left(\frac{1}{2}\right) - \frac{1}{2} \times \log_2\left(\frac{1}{2}\right) = \mathbf{1.0}$$

(50-50 split → maximum entropy)

**Weighted Average:**

$$\text{Entropy}_{\text{age33}} = \frac{6}{14} \times 0.6500 + \frac{8}{14} \times 1.0 = 0.2786 + 0.5714 = \mathbf{0.8500}$$

**Comparison:** Age 33 split (0.8500) is better than Sex split (0.8922).

---

#### Split by Occupation

We need 3 separate splits: A vs. not-A, B vs. not-B, C vs. not-C.

**Occupation A vs. not-A:**

| | Target 1 | Target 2 | Subtotal |
|---|---|---|---|
| **A** | 2 | 3 | 5 |
| **not-A** | 7 | 2 | 9 |

$$\text{Entropy}_A = -\frac{2}{5}\log_2\left(\frac{2}{5}\right) - \frac{3}{5}\log_2\left(\frac{3}{5}\right) = 0.9710$$

$$\text{Entropy}_{\text{not-A}} = -\frac{7}{9}\log_2\left(\frac{7}{9}\right) - \frac{2}{9}\log_2\left(\frac{2}{9}\right) = 0.7642$$

$$\text{Entropy}_{\text{occA}} = \frac{5}{14} \times 0.9710 + \frac{9}{14} \times 0.7642 = 0.3468 + 0.4913 = \mathbf{0.8381}$$

**Occupation B vs. not-B:**

| | Target 1 | Target 2 | Subtotal |
|---|---|---|---|
| **B** | 5 | 0 | 5 |
| **not-B** | 4 | 5 | 9 |

$$\text{Entropy}_B = -\frac{5}{5}\log_2\left(\frac{5}{5}\right) - \frac{0}{5}\log_2\left(\frac{0}{5}\right) = -1 \times 0 - 0 \times (-\infty) = \mathbf{0}$$

> **Key insight:** When one proportion is 0, entropy = 0. This means zero randomness — perfect prediction! All B's are happy.

$$\text{Entropy}_{\text{not-B}} = -\frac{4}{9}\log_2\left(\frac{4}{9}\right) - \frac{5}{9}\log_2\left(\frac{5}{9}\right) = 0.9911$$

$$\text{Entropy}_{\text{occB}} = \frac{5}{14} \times 0 + \frac{9}{14} \times 0.9911 = 0 + 0.6372 = \mathbf{0.6372}$$

**Occupation C vs. not-C:**

| | Target 1 | Target 2 | Subtotal |
|---|---|---|---|
| **C** | 2 | 2 | 4 |
| **not-C** | 7 | 3 | 10 |

$$\text{Entropy}_C = -\frac{2}{4}\log_2\left(\frac{2}{4}\right) - \frac{2}{4}\log_2\left(\frac{2}{4}\right) = \mathbf{1.0}$$

$$\text{Entropy}_{\text{not-C}} = -\frac{7}{10}\log_2\left(\frac{7}{10}\right) - \frac{3}{10}\log_2\left(\frac{3}{10}\right) = 0.8813$$

$$\text{Entropy}_{\text{occC}} = \frac{4}{14} \times 1.0 + \frac{10}{14} \times 0.8813 = 0.2857 + 0.6295 = \mathbf{0.9152}$$

---

### Step 3: Choose the Best Split

| Split | Entropy |
|-------|---------|
| Root (no split) | 0.9403 |
| Sex | 0.8922 |
| Age ≤ 33 | 0.8500 |
| Occupation A | 0.8381 |
| **Occupation B** | **0.6372** ← LOWEST |
| Occupation C | 0.9152 |

**Answer:** Occupation B gives the lowest entropy (0.6372), so it's the best first split.

**Why?** Because all people with Occupation B are happy (entropy = 0 for the B group). This split perfectly predicts happiness for the B group.

---

## 9E: Making Predictions After the Split

### If Occupation = B

Looking at the data: all 5 people with Occupation B have Target = 1 (Happy).

**Prediction:** Happy (1) — with 100% certainty!

### If Occupation ≠ B

The remaining 9 people have:
- Target 1 (Happy): 4 people
- Target 2 (Unhappy): 5 people

This is ambiguous (nearly 50-50). We can't make a confident prediction, so we need to **split further**.

### Second Split (for Occupation ≠ B)

Now we only consider the reduced dataset (9 people, excluding Occupation B). We repeat the entropy calculation for this reduced set and find the next best split variable.

For example, we might find that splitting by Sex gives the lowest entropy for this reduced set:
- If Male → predict Unhappy (2) [majority vote]
- If Female → predict Happy (1) [majority vote]

---

## 9F: Other Splitting Criteria (Conceptual)

### Gini Impurity

Instead of entropy, some decision tree algorithms use **Gini impurity**:

$$\text{Gini} = 1 - \sum p_i^2$$

For a binary target: Gini = 1 − p₁² − p₂²

The process is the same: calculate Gini for each split, choose the split with the lowest Gini.

### Chi-Square Test

The chi-square test can also be used to determine the best split by measuring how much the observed frequencies differ from expected frequencies.

---

## 9G: KNN (K-Nearest Neighbors) — Conceptual 🔑

### What is KNN?

**KNN** is a supervised learning algorithm that classifies a new data point based on the majority class among its K nearest neighbors.

### How It Works

1. Choose a value for K (e.g., K = 3 or K = 5)
2. Find the K training data points closest to the new point
3. Assign the new point to the majority class among those K neighbors

### Key Properties

| Property | Value |
|----------|-------|
| **Type** | Supervised learning |
| **Can be done by hand?** | No (too many distance calculations) |
| **Key parameter** | K (number of neighbors) |
| **Distance metric** | Usually Euclidean distance |

### Conceptual Test Questions

- KNN is a **supervised** learning method (it uses true labels)
- A small K (e.g., K=1) → more sensitive to noise, overfitting
- A large K (e.g., K=20) → smoother boundaries, but may miss local patterns
- KNN doesn't build a model — it just memorizes the training data ("lazy learning")

---

## 9H: K-Means Clustering — Conceptual 🔑

### What is K-Means?

**K-means clustering** is an unsupervised learning algorithm that groups data into K clusters.

### How It Works

1. Choose K (number of clusters)
2. Randomly place K centroids (cluster centers)
3. Assign each data point to the nearest centroid
4. Recalculate centroids as the mean of all points in each cluster
5. Repeat steps 3-4 until centroids stop moving

### Key Properties

| Property | Value |
|----------|-------|
| **Type** | Unsupervised learning |
| **Can be done by hand?** | No (iterative calculations) |
| **Key parameter** | K (number of clusters) |
| **True labels needed?** | No |

### Conceptual Test Questions

- K-means is an **unsupervised** learning method (no true labels)
- You must specify K in advance
- The algorithm may converge to different results depending on initial centroid placement
- K-means works best with spherical, equally-sized clusters

---

## Quick Reference: Formulas Summary

| Concept | Formula |
|---------|---------|
| Entropy | −p₁ × log₂(p₁) − p₂ × log₂(p₂) |
| log₂ calculation | log₂(x) = log(x) / log(2) |
| 0 × log(0) | = 0 (by convention) |
| Gini Impurity | 1 − p₁² − p₂² |
| Weighted average entropy | (n₁/N) × Entropy₁ + (n₂/N) × Entropy₂ |

# Chapter 8: Machine Learning — Supervised and Unsupervised Examples

> **Test coverage:** This chapter will be covered in Test 2. Expect calculation questions on ROC curve (TPR, FPR) and hierarchical clustering (single, average, complete linkage).

---

## 8A: Supervised Learning — ROC Curve 🔑🔑🔑

### What is the ROC Curve?

**ROC** stands for **Receiver Operating Characteristic**. It's a graph that shows the performance of a classification model at all classification thresholds.

- **X-axis:** False Positive Rate (FPR)
- **Y-axis:** True Positive Rate (TPR)

### Key Definitions

| Term | Definition | Formula |
|------|-----------|---------|
| **True Positive (TP)** | Predicted positive, actually positive | — |
| **False Positive (FP)** | Predicted positive, actually negative | — |
| **True Negative (TN)** | Predicted negative, actually negative | — |
| **False Negative (FN)** | Predicted negative, actually positive | — |
| **True Positive Rate (TPR)** | Percentage of actual positives correctly identified | TP / (TP + FN) |
| **False Positive Rate (FPR)** | Percentage of actual negatives incorrectly identified as positive | FP / (FP + TN) |

### The Threshold (Limit) Concept

In logistic regression, we predict **probability of cancer** (a number between 0 and 1). But ultimately, we need to make a **binary decision**: cancer or no cancer.

To convert probability into a binary decision, we set a **threshold** (also called a **limit**):

- If predicted probability ≥ threshold → predict **positive** (has cancer)
- If predicted probability < threshold → predict **negative** (no cancer)

**The game:** We try different thresholds and see how our predictions match the true labels.

---

### Worked Example: ROC Curve Calculation

#### The Data

We have 10 patients with predicted probabilities of cancer and their true labels:

| Patient | Predicted Probability | True Label |
|---------|----------------------|------------|
| 1 | 0.95 | Cancer (positive) |
| 2 | 0.93 | Cancer (positive) |
| 3 | 0.85 | No cancer (negative) |
| 4 | 0.75 | Cancer (positive) |
| 5 | 0.70 | Cancer (positive) |
| 6 | 0.65 | No cancer (negative) |
| 7 | 0.60 | No cancer (negative) |
| 8 | 0.55 | No cancer (negative) |
| 9 | 0.50 | No cancer (negative) |
| 10 | 0.25 | Cancer (positive) |

**Summary:** 5 actual positives (patients 1, 2, 4, 5, 10), 5 actual negatives (patients 3, 6, 7, 8, 9)

---

#### Threshold 1: ≥ 0.25

**Prediction rule:** If probability ≥ 0.25, predict positive.

Since all 10 patients have probability ≥ 0.25, we predict **everyone as positive**.

| Count | Value | Explanation |
|-------|-------|-------------|
| **TP** | 5 | All 5 actual positives are predicted positive ✓ |
| **FP** | 5 | All 5 actual negatives are predicted positive ✗ |
| **TN** | 0 | Nobody predicted negative |
| **FN** | 0 | Nobody predicted negative |

**TPR** = TP / (TP + FN) = 5 / (5 + 0) = 5/5 = **1.0**

**FPR** = FP / (FP + TN) = 5 / (5 + 0) = 5/5 = **1.0**

**Data point:** (FPR, TPR) = (1.0, 1.0)

---

#### Threshold 2: ≥ 0.43

**Prediction rule:** If probability ≥ 0.43, predict positive.

Patients with probability ≥ 0.43: patients 1–9 (9 patients). Patient 10 (0.25) is predicted negative.

| Count | Value | Explanation |
|-------|-------|-------------|
| **TP** | 4 | Patients 1, 2, 4, 5 are positive and predicted positive |
| **FP** | 5 | Patients 3, 6, 7, 8, 9 are negative but predicted positive |
| **TN** | 0 | Patient 10 is positive, predicted negative → not TN |
| **FN** | 1 | Patient 10 is positive but predicted negative |

**TPR** = TP / (TP + FN) = 4 / (4 + 1) = 4/5 = **0.8**

**FPR** = FP / (FP + TN) = 5 / (5 + 0) = 5/5 = **1.0**

**Data point:** (FPR, TPR) = (1.0, 0.8)

---

#### Threshold 3: ≥ 0.53

**Prediction rule:** If probability ≥ 0.53, predict positive.

Patients with probability ≥ 0.53: patients 1–8 (8 patients). Patients 9, 10 are predicted negative.

| Count | Value | Explanation |
|-------|-------|-------------|
| **TP** | 4 | Patients 1, 2, 4, 5 are positive and predicted positive |
| **FP** | 4 | Patients 3, 6, 7, 8 are negative but predicted positive |
| **TN** | 1 | Patient 9 is negative and predicted negative ✓ |
| **FN** | 1 | Patient 10 is positive but predicted negative |

**TPR** = TP / (TP + FN) = 4 / (4 + 1) = 4/5 = **0.8**

**FPR** = FP / (FP + TN) = 4 / (4 + 1) = 4/5 = **0.8**

**Data point:** (FPR, TPR) = (0.8, 0.8)

---

#### Continuing with Other Thresholds

You repeat this process for each threshold (0.55, 0.60, 0.65, 0.70, 0.75, 0.85, 0.93, 0.95), calculating TP, FP, TN, FN, TPR, and FPR each time.

#### The Final ROC Curve

Plot all the (FPR, TPR) points and connect them. The resulting curve shows the trade-off between true positive rate and false positive rate.

### Interpreting the ROC Curve

| Curve Shape | Meaning |
|-------------|---------|
| **Steep curve (close to top-left corner)** | Excellent classifier — high TPR, low FPR |
| **45-degree diagonal line** | Random guessing — no better than chance |
| **Flat curve (close to bottom-right)** | Terrible classifier — worse than random |

> **Goal:** You want the ROC curve to be as **steep** as possible — reaching high TPR while keeping FPR low.

---

## 8B: Unsupervised Learning — Hierarchical Clustering 🔑🔑🔑

### What is Hierarchical Clustering?

**Hierarchical clustering** groups similar objects together without knowing the true labels. The result is visualized as a **dendrogram** (a tree-like diagram).

### The Problem

We have 5 cells and want to classify them into **cancer cells** and **non-cancer cells**. But we **don't have true labels** — we don't know which cells are actually cancerous.

All we have is a **distance matrix** showing how different each pair of cells is:

| | Cell 1 | Cell 2 | Cell 3 | Cell 4 | Cell 5 |
|---|---|---|---|---|---|
| **Cell 1** | 0 | 9 | 3 | 6 | 11 |
| **Cell 2** | — | 0 | 7 | 5 | 10 |
| **Cell 3** | — | — | 0 | 9 | 2 |
| **Cell 4** | — | — | — | 0 | 8 |
| **Cell 5** | — | — | — | — | 0 |

**Interpretation:** Smaller distance = more similar. For example, Cell 3 and Cell 5 have distance 2 (very similar), while Cell 1 and Cell 5 have distance 11 (very different).

> **Key principle:** The shorter the distance between two cells, the more likely they belong to the same group.

---

### Method 1: Single Linkage (Minimum Principle) 🔑

**Rule:** When calculating the distance between a cell and a group, use the **minimum** distance.

#### Step 1: Find the Shortest Distance

Looking at the matrix, the smallest non-zero distance is **2** (between Cell 3 and Cell 5).

→ **Link Cell 3 and Cell 5 at distance 2.** This is **Level 1** of the first group.

#### Step 2: Recalculate Distances to the New Group (3,5)

Now we need distances from each remaining cell to the combined group (3,5).

**Distance from Cell 1 to group (3,5):**
- Distance(1, 3) = 3
- Distance(1, 5) = 11
- **Minimum** = **3**

**Distance from Cell 2 to group (3,5):**
- Distance(2, 3) = 7
- Distance(2, 5) = 10
- **Minimum** = **7**

**Distance from Cell 4 to group (3,5):**
- Distance(4, 3) = 9
- Distance(4, 5) = 8
- **Minimum** = **8**

Updated matrix:

| | Cell 1 | Cell 2 | Cell 4 | Group (3,5) |
|---|---|---|---|---|
| **Cell 1** | 0 | 9 | 6 | **3** |
| **Cell 2** | — | 0 | 5 | **7** |
| **Cell 4** | — | — | 0 | **8** |
| **Group (3,5)** | — | — | — | — |

#### Step 3: Find the Next Shortest Distance

The smallest distance is **3** (between Cell 1 and group (3,5)).

→ **Link Cell 1 with group (3,5) at distance 3.** This is **Level 2** of the first group.

Now we have group (1, 3, 5).

#### Step 4: Recalculate Distances to Group (1,3,5)

**Distance from Cell 2 to group (1,3,5):**
- Distance(2, 1) = 9
- Distance(2, 3,5) = 7 (already calculated)
- **Minimum** = **7**

**Distance from Cell 4 to group (1,3,5):**
- Distance(4, 1) = 6
- Distance(4, 3,5) = 8 (already calculated)
- **Minimum** = **6**

Updated matrix:

| | Cell 2 | Cell 4 | Group (1,3,5) |
|---|---|---|---|
| **Cell 2** | 0 | 5 | **7** |
| **Cell 4** | — | 0 | **6** |
| **Group (1,3,5)** | — | — | — |

#### Step 5: Find the Next Shortest Distance

The smallest distance is **5** (between Cell 2 and Cell 4).

→ **Link Cell 2 and Cell 4 at distance 5.** This is **Level 1** of a **separate** group.

> **Important:** This is Level 1 of a new group, NOT Level 3 of the first group, because (2,4) is completely separate from (1,3,5).

#### Step 6: Connect the Two Groups

Now we need the distance between group (2,4) and group (1,3,5).

**Distance from group (2,4) to group (1,3,5):**
- Distance(2, 1,3,5) = 7
- Distance(4, 1,3,5) = 6
- **Minimum** = **6**

→ **Link group (2,4) with group (1,3,5) at distance 6.** This is the highest level connection.

#### Final Dendrogram (Single Linkage)

```
Level 3:                    ┌───────────┐
                            │     6     │
Level 2:           ┌────────┴────┐      │
                   │      3      │      │
Level 1:     ┌─────┴─────┐       │   ┌──┴──┐
            Cell 3  Cell 5     Cell 1  Cell 2  Cell 4
           (dist=2)          (dist=3)  (dist=5)
```

**Interpretation:**
- **Group 1:** Cells 3, 5, 1 (similar — possibly cancer cells)
- **Group 2:** Cells 2, 4 (different — possibly non-cancer cells)

---

### Method 2: Average Linkage 🔑

**Rule:** When calculating the distance between a cell and a group, use the **average** of all distances.

The steps are the same as single linkage, but instead of taking the minimum, you take the average.

#### Step 1: Same as Before

Shortest distance is 2 → Link Cell 3 and Cell 5.

#### Step 2: Recalculate Using Average

**Distance from Cell 1 to group (3,5):**
- Distance(1, 3) = 3
- Distance(1, 5) = 11
- **Average** = (3 + 11) / 2 = **7**

**Distance from Cell 2 to group (3,5):**
- Distance(2, 3) = 7
- Distance(2, 5) = 10
- **Average** = (7 + 10) / 2 = **8.5**

**Distance from Cell 4 to group (3,5):**
- Distance(4, 3) = 9
- Distance(4, 5) = 8
- **Average** = (9 + 8) / 2 = **8.5**

#### Step 3: Find the Next Shortest Distance

Looking at all distances, the smallest is **5** (between Cell 2 and Cell 4).

→ **Link Cell 2 and Cell 4 at distance 5.** Level 1 of second group.

#### Step 4: Recalculate

**Distance from Cell 1 to group (3,5):** = 7 (from above)

**Distance from group (2,4) to group (3,5):**
- Distance(2, 3,5) = 8.5
- Distance(4, 3,5) = 8.5
- **Average** = (8.5 + 8.5) / 2 = **8.5**

**Distance from Cell 1 to group (2,4):**
- Distance(1, 2) = 9
- Distance(1, 4) = 6
- **Average** = (9 + 6) / 2 = **7.5**

#### Step 5: Find the Next Shortest

The smallest is **7** (Cell 1 to group (3,5)).

→ **Link Cell 1 with group (3,5) at distance 7.** Level 2 of first group.

#### Step 6: Final Connection

**Distance from group (1,3,5) to group (2,4):**

This is tricky. We need:
- Distance(1, 2,4) = 7.5
- Distance(3,5, 2,4) = 8.5, but since (3,5) has 2 cells, we multiply by 2: 8.5 × 2 = 17

Average = (7.5 + 8.5 + 8.5) / 3 = 24.5 / 3 = **8.17**

→ **Link group (1,3,5) with group (2,4) at distance 8.17.**

---

### Method 3: Complete Linkage (Maximum Principle) 🔑

**Rule:** When calculating the distance between a cell and a group, use the **maximum** distance.

This seems counterintuitive (why use the maximum?), but it works well for separating groups.

#### Step 1: Same as Before

Shortest distance is 2 → Link Cell 3 and Cell 5.

#### Step 2: Recalculate Using Maximum

**Distance from Cell 1 to group (3,5):**
- Distance(1, 3) = 3
- Distance(1, 5) = 11
- **Maximum** = **11**

**Distance from Cell 2 to group (3,5):**
- Distance(2, 3) = 7
- Distance(2, 5) = 10
- **Maximum** = **10**

**Distance from Cell 4 to group (3,5):**
- Distance(4, 3) = 9
- Distance(4, 5) = 8
- **Maximum** = **9**

#### Step 3: Find the Next Shortest Distance

The smallest is **5** (between Cell 2 and Cell 4).

→ **Link Cell 2 and Cell 4 at distance 5.**

#### Step 4: Recalculate

**Distance from Cell 1 to group (2,4):**
- Distance(1, 2) = 9
- Distance(1, 4) = 6
- **Maximum** = **9**

**Distance from group (3,5) to group (2,4):**
- Distance(3, 2,4): max(Distance(3,2), Distance(3,4)) = max(7, 9) = 9
- Distance(5, 2,4): max(Distance(5,2), Distance(5,4)) = max(10, 8) = 10
- **Maximum** = **10**

#### Step 5: Find the Next Shortest

The smallest is **9** (Cell 1 to group (2,4)).

→ **Link Cell 1 with group (2,4) at distance 9.**

#### Step 6: Final Connection

**Distance from group (1,2,4) to group (3,5):**
- Distance(1, 3,5) = 11
- Distance(2,4, 3,5) = 10
- **Maximum** = **11**

→ **Link group (1,2,4) with group (3,5) at distance 11.**

---

### Comparison of Three Methods

| Method | Rule | Grouping Result |
|--------|------|-----------------|
| **Single Linkage** | Minimum | (3,5,1) and (2,4) |
| **Average Linkage** | Average | (3,5,1) and (2,4) |
| **Complete Linkage** | Maximum | (3,5) and (1,2,4) |

> **Note:** Different methods can produce different groupings! The choice depends on your specific application.

---

### Real-World Application: Cancer Classification

In real medical research, hierarchical clustering is used to classify cancer types:

- **Low-level connections** (short distances) → very similar cancers (e.g., ovarian cancer and prostate cancer — both reproductive system cancers)
- **High-level connections** (long distances) → very different cancers (e.g., breast cancer and melanoma/skin cancer)

Even without true labels, researchers can discover meaningful groupings based on similarity measures.

---

## Quick Reference: Formulas Summary

| Concept | Formula |
|---------|---------|
| True Positive Rate | TPR = TP / (TP + FN) |
| False Positive Rate | FPR = FP / (FP + TN) |
| Single Linkage | min(distance to each member) |
| Average Linkage | average(distance to each member) |
| Complete Linkage | max(distance to each member) |

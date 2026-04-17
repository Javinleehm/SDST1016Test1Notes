---
title: SDST1016 Data Science 101 - Complete Notes
layout: default
---

# SDST1016 — Data Science 101 Revision Notes

> **Important:** These notes are based **exclusively on what was taught in lecture** (transcriptions Jan 20 – Apr 17). The lecturer explicitly stated: *"I only test things I said in lesson."*
>
> Test 1 (March 24) covers **Chapters 1–4 only**.  
> Test 2 (Late April) covers **Chapters 5–10**.

---

## 📚 Files in This Folder

### Test 1 Coverage (Chapters 1–4)

| File | Chapter | Topics |
|------|---------|--------|
| [`00_REVIEW_SHEET.md`](00_REVIEW_SHEET.md) | All | Quick review sheet with key formulas and concepts |
| [`01_Data_Science_Introduction.md`](01_Data_Science_Introduction.md) | Ch 1 | What is data science, 6 steps, correlation vs causation, confounding variables |
| [`02_Data_Processing.md`](02_Data_Processing.md) | Ch 2 | Problem definition (OST), data collection (SQE), data cleaning (outliers, normalization, NLP/LSA), vaccine efficacy |
| [`03_Data_Exploration.md`](03_Data_Exploration.md) | Ch 3 | Summary statistics, fancy charts, pivot tables, confusion matrix (accuracy/precision/recall/F1) |
| [`04_Probability.md`](04_Probability.md) | Ch 4A+B | Basic probability, additive law, inclusion-exclusion, conditional probability, Bayes theorem, Monty Hall, birthday problem |

### Test 2 Coverage (Chapters 5–10)

| File | Chapter | Topics |
|------|---------|--------|
| [`05_Normal_Distribution_CI.md`](05_Normal_Distribution_CI.md) | Ch 5 | Normal distribution review, randomized response technique, zero-knowledge proof, linear interpolation |
| [`06_Hypothesis_Testing.md`](06_Hypothesis_Testing.md) | Ch 6 | Z-test for proportions (3 cases), p-value meaning, binomial small-sample test, Type 2 error (β), power, paired comparison, Raven Paradox |
| [`07_Regression.md`](07_Regression.md) | Ch 7A+B | Simpson's Paradox, Anscombe's Quartet, logistic regression formula, log odds ratio, supervised vs unsupervised learning |
| [`08_Machine_Learning.md`](08_Machine_Learning.md) | Ch 8 | ROC curves (TPR, FPR, threshold), hierarchical clustering (single/average/complete linkage), dendrograms |
| [`09_ML_Models.md`](09_ML_Models.md) | Ch 9 | Decision tree (entropy calculation, best split), Gini impurity, KNN (conceptual), K-means clustering (conceptual) |
| [`10_Computational_Thinking.md`](10_Computational_Thinking.md) | Ch 10 | Traditional programming vs ML, transformer architecture, key AI terminology |

---

## ⚡ Key Formulas Quick Reference

### Data Cleaning
- **Standardization (Z-score):** `Z = (X - X̄) / σ`
- **Min-Max Normalization:** `Y = (X - min) / (max - min)`
- **Outlier limits:** Lower = Q1 − 1.5×IQR, Upper = Q3 + 1.5×IQR
- **Quartile position:** Q1 = (n+1)×1/4, Median = (n+1)×2/4, Q3 = (n+1)×3/4
- **Vaccine Efficacy:** `VE = 1 − P(infection|vaccinated) / P(infection|placebo)`

### Probability
- **Addition rule:** `P(A∪B) = P(A) + P(B) − P(A∩B)`
- **Inclusion-exclusion (3 events):** `P(A∪B∪C) = P(A)+P(B)+P(C) − P(A∩B) − P(A∩C) − P(B∩C) + P(A∩B∩C)`
- **Conditional probability:** `P(A|B) = P(A∩B) / P(B)`
- **Multiplicative law:** `P(A∩B) = P(B)·P(A|B)`
- **Bayes' theorem:** `P(A|B) = P(B|A)·P(A) / [P(B|A)·P(A) + P(B|Aᶜ)·P(Aᶜ)]`

### Confusion Matrix
- **Accuracy:** `(TP + TN) / Total`
- **Precision:** `TP / (TP + FP)`
- **Recall (Sensitivity):** `TP / (TP + FN)`
- **Specificity:** `TN / (TN + FP)`
- **F1 Score:** `2 × (Precision × Recall) / (Precision + Recall)`

### Normal Distribution & Confidence Intervals
- **Z-standardization:** `Z = (X − μ) / σ`
- **Sample mean distribution:** `X̄ ~ N(μ, σ²/n)`
- **Sample proportion distribution:** `p̂ ~ N(p, p(1-p)/n)`
- **95% CI for mean:** `X̄ ± 1.96 × σ/√n`
- **95% CI for proportion:** `p̂ ± 1.96 × √(p̂(1−p̂)/n)`
- **Key critical values:** z₀.₁₀ = 1.645, **z₀.₀₅ = 1.96**, z₀.₀₂ = 2.326

### Hypothesis Testing
- **Test statistic (proportion):** `Z = (p̂ − p₀) / √(p₀(1−p₀)/n)`
- **Standard error:** `SE = √(p₀(1−p₀)/n)` — use **null hypothesis p₀**!
- **Test statistic (mean):** `Z = (x̄ − μ) / (σ/√n)`
- **Decision rule:** Reject H₀ if p-value < α (usually 0.05)
- **Binomial probability:** `P(X=k) = C(n,k) × pᵏ × (1−p)ⁿ⁻ᵏ`
- **Power:** `Power = 1 − β`

### Regression
- **Logistic regression:** `P = e^(β₀ + β₁X) / (1 + e^(β₀ + β₁X))`
- **Log odds ratio:** `β₁ × (Xᵢ − Xⱼ)`
- **Odds ratio:** `e^(β₁ × (Xᵢ − Xⱼ))`
- **% Increase:** `(Odds Ratio − 1) × 100%`

### Machine Learning
- **Entropy:** `−p₁ × log₂(p₁) − p₂ × log₂(p₂)`
- **log₂ calculation:** `log₂(x) = log(x) / log(2)`
- **0 × log(0):** `= 0` (by convention)
- **TPR:** `TP / (TP + FN)`
- **FPR:** `FP / (FP + TN)`

---

## 🎯 What the Lecturer Tests

### Test 1 Topics
1. **Calculation of Q1, Q3, IQR, outlier limits** — given a dataset
2. **Standardization and normalization** — calculating z-scores and normalized values
3. **Document/word vectors** — eigenvalue ratio, coordinates from reduced-rank matrix
4. **Vaccine efficacy** — calculate VE from infection rates
5. **Probability calculations** — P(A∪B), P(A|B), inclusion-exclusion with 3 events
6. **Bayes theorem** — using the table method (fill in step-by-step)
7. **Confusion matrix** — accuracy, precision, recall, F1-score

### Test 2 Topics
8. **Randomized response technique** — solve for P_gay given P(yes)
9. **Normal table interpolation** — linear interpolation for more accurate p-values
10. **Hypothesis testing (3 cases)** — calculate test stat, find p-value, make decision for right-tailed, left-tailed, two-tailed
11. **Binomial p-value** — `P(X ≥ k | p = p₀)` for small sample tests
12. **Type 2 error and power** — calculate β and 1−β
13. **Logistic regression** — calculate probability, odds ratio, percentage increase
14. **ROC curve** — calculate TPR, FPR for different thresholds
15. **Hierarchical clustering** — single/average/complete linkage calculations
16. **Decision tree entropy** — calculate entropy for each split, choose best split
17. **Conceptual questions** — KNN vs K-means, supervised vs unsupervised, Simpson's Paradox, Anscombe's Quartet
18. **Transformer terminology** — key terms and logical flow

---

## 📋 Test Coverage

| Test | Date | Coverage |
|------|------|----------|
| Test 1 | March 24 (Tuesday in class) | Chapters 1–4 |
| Test 2 | Late April (Tuesday in class) | Chapters 5–10 |

**Format:** Multiple choice (20–25 questions), 4 choices each (often choice D = "none of the above")  
**Allowed:** Formula sheet (provided on Moodle), rough paper/calculator  
**Location:** In-class, bring your laptop (Moodle test)  

---

## 💡 Study Tips from the Lecturer

1. **Watch the recordings at 2-3x speed** to quickly review what was covered
2. **The sample questions are very similar to the actual test** — just with different numbers
3. **Bring rough paper** for calculations during the test
4. **For hypothesis testing, always use the null hypothesis value** (not sample proportion) for standard error
5. **Don't forget the minus sign** in entropy calculations
6. **Check your frequency subtotals add to sample size** — easy way to catch mistakes
7. **Choose your alternative hypothesis BEFORE looking at data** — otherwise you're cheating!

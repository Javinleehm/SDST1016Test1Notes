---
title: SDST1016 Data Science 101 - Test 1 Notes
layout: default
---

# SDST1016 — Data Science 101 Revision Notes

> **Important:** These notes are based **exclusively on what was taught in lecture** (transcriptions Jan 20 – Mar 20). The lecturer explicitly stated: *"I only test things I said in lesson."*
>
> Test 1 (March 24) covers **Chapters 1–4 only**.  
> Test 2 covers **Chapters 5–6**.

---

## 📚 Files in This Folder

| File | Chapter | Topics |
|------|---------|--------|
| [`00_REVIEW_SHEET.md`](00_REVIEW_SHEET.md) | All | Quick review sheet with key formulas and concepts |
| [`01_Data_Science_Introduction.md`](01_Data_Science_Introduction.md) | Ch 1 | What is data science, 6 steps, correlation vs causation, confounding variables |
| [`02_Data_Processing.md`](02_Data_Processing.md) | Ch 2 | Problem definition (OST), data collection (SQE), data cleaning (outliers, normalization, NLP/LSA), vaccine efficacy |
| [`03_Data_Exploration.md`](03_Data_Exploration.md) | Ch 3 | Summary statistics, fancy charts, pivot tables, confusion matrix (accuracy/precision/recall/F1) |
| [`04_Probability.md`](04_Probability.md) | Ch 4A+B | Basic probability, additive law, inclusion-exclusion, conditional probability, Bayes theorem, Monty Hall, birthday problem |
| [`05_Normal_Distribution_CI.md`](05_Normal_Distribution_CI.md) | Ch 5 | Normal distribution, percentile calculations, CLT, confidence intervals, sample size, randomized response technique |
| [`06_Hypothesis_Testing.md`](06_Hypothesis_Testing.md) | Ch 6 | Z-test for proportions (3 cases), p-value meaning, binomial small-sample test, beta |

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
- **Decision rule:** Reject H₀ if p-value < α (usually 0.05)

---

## 🎯 What the Lecturer Tests

Based on lecture emphasis:
1. **Calculation of Q1, Q3, IQR, outlier limits** — given a dataset
2. **Standardization and normalization** — calculating z-scores and normalized values
3. **Document/word vectors** — eigenvalue ratio, coordinates from reduced-rank matrix
4. **Vaccine efficacy** — calculate VE from infection rates
5. **Probability calculations** — P(A∪B), P(A|B), inclusion-exclusion with 3 events
6. **Bayes theorem** — using the table method (fill in step-by-step)
7. **Confusion matrix** — accuracy, precision, recall, F1-score
8. **Confidence interval** — finding margin of error given sample proportion
9. **Hypothesis testing** — calculate test stat, find p-value, make decision
10. **Binomial p-value** — `P(X ≥ k | p = p₀)` for small sample tests

---

## 📋 Test Coverage

| Test | Date | Coverage |
|------|------|----------|
| Test 1 | March 24 (Tuesday in class) | Chapters 1–4 |
| Test 2 | Late April | Chapters 5–6 |

**Format:** Multiple choice (20–25 questions), 4 choices each (often choice D = "none of the above")  
**Allowed:** Formula sheet (provided on Moodle), rough paper/calculator  
**Location:** In-class, bring your laptop (Moodle test)  

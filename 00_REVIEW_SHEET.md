# SDST1016 — Quick Review Sheet

> Dense review reference. For learning, see the individual chapter files.
>
> **Test 1 (March 24):** Ch1–4 | **Test 2:** Ch5–6

---

## CH1 — DATA SCIENCE CONCEPTS

**Data Science = Statistics + Computer Science + Domain Expertise**

- **Statistics** = hypothesis testing (make assumption → collect data → confirm/refute)
- **Computer Science** = the toolbox
- **Domain Expertise** = the problem area

**6 Steps (every project must have all 6):**
1. Problem Definition → 2. Data Collection → 3. Data Cleaning & Preprocessing → 4. Data Exploration → 5. Model Building → 6. Communication & Visualisation

**Correlation ≠ Causation** — two things happening together doesn't mean one causes the other.

**Confounding variable** — a hidden third variable that explains a spurious correlation.
> e.g. sick patients take vitamins AND have shorter lifespan — sickness is the confounder

**5% significance** — you need very strong evidence (not just 50-50) before you can reject a hypothesis.

---

## CH2 — DATA PROCESSING

### Problem Definition: OST
| O | Objectives | What exactly are you achieving? |
|---|---|---|
| S | Specific | Is it measurable/quantifiable? |
| T | Timeline | How soon? What data time period? |

### Data Collection: SQE
| S | Source | Where from? (e.g. Kaggle) |
|---|---|---|
| Q | Quality | Has it been validated? |
| E | Ethics | Privacy (anonymity) + Consent |

**Data Ethics needs BOTH:** (1) Anonymity + (2) Informed Consent

---

### Vaccine Efficacy
$$VE = 1 - \frac{P(\text{infection} \mid \text{vaccinated})}{P(\text{infection} \mid \text{placebo})}$$

Pfizer example: VE = 1 − 8/162 = **95%** (confirmed cases only)

---

### Outliers — IQR Method

1. Sort data ascending
2. Q1 position = (n+1)×**1**/4 ; Median = (n+1)×**2**/4 ; Q3 = (n+1)×**3**/4
3. **Linear interpolation:** value = lower value + decimal × (upper − lower)
4. IQR = Q3 − Q1
5. Lower limit = Q1 − **1.5**×IQR ; Upper limit = Q3 + **1.5**×IQR
6. Values **outside** [Lower, Upper] = **outliers**

**Larger multiplier (e.g. 2)** → wider range → fewer outliers
**Before discarding:** check the data source — is it a typo?

---

### Key Transformations
| Name | Formula | Result |
|------|---------|--------|
| **Standardisation (Z-score)** | `Z = (X − X̄) / σ` | Mean=0, SD=1 |
| **Min-Max Normalisation** | `Y = (X − min) / (max − min)` | Range [0,1] |

---

### NLP / Latent Semantic Analysis (LSA)

**Goal:** Convert text documents → numerical vectors (so computers can analyse them)

**Steps:**
1. Build **Term-Document Matrix A** (rows=keywords, cols=documents, values=frequencies)
2. **SVD:** A = U × Λ × Vᵀ (U=word eigenvectors, Λ=eigenvalues diagonal, V=document eigenvectors)
3. **Keep top R eigenvalues** for low-rank approximation

**% variance captured (testable):**
$$\frac{\lambda_1^2 + \lambda_2^2 + \ldots + \lambda_R^2}{\lambda_1^2 + \lambda_2^2 + \ldots + \lambda_P^2}$$

**Document vectors** = Λ_R × V_R^T → each column = (X, Y) coordinate of one document

**Word vectors** = U_R × Λ_R → each row = (X, Y) coordinate of one keyword

---

## CH3 — DATA EXPLORATION

### Fancy Charts — Know the Use Case!
| Chart | Used for |
|-------|---------|
| **Gantt** | Project management & scheduling |
| **Sankey/Ribbon** | Flow of resources/money/energy |
| **Radar** | Multi-dimensional performance comparison |
| **Treemap** | Hierarchical data (drill-down rectangles) |
| **Choropleth** | Geographic/spatial data (heat map on a map) |
| **Sunburst** | Hierarchical data (circular rings) |

---

### Hypothesis Testing Concepts (Ch3 Supplement)
| Term | Definition |
|------|-----------|
| **H₀** (null) | The assumption (status quo) |
| **H₁** (alternative) | The opposite of H₀ |
| **Type 1 Error** | H₀ true, but you reject it → **False Positive** → probability = **α** |
| **Type 2 Error** | H₁ true, but you accept H₀ → **False Negative** → probability = **β** |
| **α (significance level)** | Usually 5%; set BEFORE collecting data |
| **Power** | P(correctly reject H₀ when H₁ true) = 1 − β |

---

### Confusion Matrix Formulas

Given table (oriented correctly: TP top-left):

| | **Positive (disease)** | **Negative (healthy)** |
|---|---|---|
| **Test +** | TP | FP |
| **Test −** | FN | TN |

$$\text{Accuracy} = \frac{TP + TN}{TP + TN + FP + FN}$$

$$\text{Precision} = \frac{TP}{TP + FP} \quad \text{(of all predicted positive, how many correct?)}$$

$$\text{Recall} = \frac{TP}{TP + FN} \quad \text{(= Sensitivity; of all actually positive, how many caught?)}$$

$$\text{Specificity} = \frac{TN}{TN + FP} \quad \text{(of all actually negative, how many correct?)}$$

$$F1 = 2 \times \frac{\text{Precision} \times \text{Recall}}{\text{Precision} + \text{Recall}}$$

**F1 is dragged down by whichever of Precision/Recall is smaller.** Imbalanced → punished.

---

## CH4 — PROBABILITY

### Core Rules
| Rule | Formula |
|------|---------|
| Complement | P(Aᶜ) = 1 − P(A) |
| **At least one** | P(≥1) = **1 − P(none)** |
| Addition | P(A∪B) = P(A) + P(B) − P(A∩B) |
| Mutually exclusive | P(A∩B) = 0 → P(A∪B) = P(A) + P(B) |
| Conditional | P(A\|B) = P(A∩B) / P(B) |
| Multiplicative | P(A∩B) = P(B) · P(A\|B) |
| Independent | P(A\|B) = P(A) i.e. knowing B doesn't change A |
| **Inclusion-exclusion (3)** | P(A∪B∪C) = P(A)+P(B)+P(C) − P(AB) − P(AC) − P(BC) + P(ABC) |

---

### Gambler's Problem
- At least one 6 in 4 rolls: 1 − (5/6)⁴ = **0.5177**
- At least one double-6 in 24 rolls: 1 − (35/36)²⁴ = **0.4914**
- **Never add:** 4×(1/6) = wrong. Use the complement!

---

### Standard Card/Dice Results
- 2 dice: 36 outcomes; sum=2 → 1/36; sum=6 → 5/36; same number → 6/36
- 52 cards: diamond=13/52; ace=4/52; face card=12/52

---

### Bayes' Theorem (Confusion of the Inverse)

P(A|B) ≠ P(B|A) — do NOT confuse!

$$P(A|B) = \frac{P(B|A) \cdot P(A)}{P(B|A) \cdot P(A) + P(B|A^c) \cdot P(A^c)}$$

**3 calculation methods:** formula | table (most systematic) | tree diagram (easiest)

**Table method — fill in this order:**
1. N (sample size)
2. N × base rate = disease patients
3. disease × sensitivity = TP
4. disease − TP = FN (by elimination)
5. N − disease = healthy
6. healthy × specificity = TN
7. healthy − TN = FP (by elimination)
8. P(disease | positive test) = TP / (TP + FP) = TP / column total

**Cancer screening example:** base rate=1%, sensitivity=80%, specificity=90%, n=1000
→ P(malignant | positive mammogram) = **8/107 = 7.5%** (NOT 75% — that's the confusion of the inverse!)

**Drug test example:** base rate=5%, accuracy=95% both ways, n=10,000
→ P(drug user | positive) = **475/950 = 50%** (fifty-fifty!)

---

### Monty Hall
You pick door 3. Host opens door 1 (goat). **Always switch to door 2.**
- P(car at door 3 | host opens 1) = 1/3
- P(car at door 2 | host opens 1) = **2/3**

---

### Birthday Problem
- At least one matching pair among n people: P = 1 − (365/365)(364/365)...(366−n)/365)
- **n=23 gives P > 50%**
- "Matches your birthday specifically": P = 1 − (364/365)^(n−1) → lower because more restricted

---

### Family with Two Children
- P(both girls | at least one girl) = **1/3** (sample space: GG, GB, BG — 1 of 3)
- P(both girls | elder is girl) = **1/2** (sample space: GG, GB — 1 of 2)

---

## CH5 — NORMAL DISTRIBUTION & CI

### Normal Distribution Properties
- Bell-shaped, symmetric about μ
- **68-95-100 rule:** μ±1σ=68%, μ±2σ=95%, μ±3σ≈100%
- Smaller σ² → taller, narrower; larger σ² → flatter, wider

**Why normal?** Maximum entropy distribution — contains the most information.

### Z-Transformation
$$Z = \frac{Y - \mu}{\sigma} \sim N(0,1)$$

### Normal Table Usage
- Table gives P(0 < Z < z) = gray area in middle
- P(Z > z) = 0.5 − table value
- P(−z < Z < z) = 2 × table value

### Key Critical Values
| Level | z |
|-------|---|
| 90% | 1.645 |
| **95%** | **1.96** |
| 98% | 2.326 |

> **Only 95% is tested in this course. Use z = 1.96.**

---

### Percentile from Histogram
1. Target = p% × n (e.g. 75th percentile with n=200 → need 150th observation)
2. Cumulate bar frequencies until you bracket the target
3. Linear interpolation:

$$\text{Percentile} = \text{bin start} + \frac{\text{target} - \text{lower cumulative}}{\text{upper cumulative} - \text{lower cumulative}} \times \text{bin width}$$

---

### Percentile from Normal Distribution (Working Backwards)
1. Write: P(Y < C) = 0.75
2. Standardise: P(Z < (C−μ)/σ) = 0.75
3. Table gives 0.75 − 0.5 = **0.25** → find Z where table = 0.25 → Z ≈ **0.6745**
4. Solve: (C − μ)/σ = 0.6745 → C = μ + 0.6745σ

For 25th percentile: Z = −0.6745 (negative, below mean)

---

### Central Limit Theorem (CLT)
For ANY population (doesn't have to be normal), when n is large:
$$\bar{Y} \overset{\cdot}{\sim} N\left(\mu,\ \frac{\sigma^2}{n}\right)$$

**Sample proportion:**
$$\hat{p} \overset{\cdot}{\sim} N\left(p,\ \frac{p(1-p)}{n}\right)$$

---

### Confidence Intervals

**95% CI for proportion:**
$$\hat{p} \pm 1.96 \times \sqrt{\frac{\hat{p}(1-\hat{p})}{n}}$$

**95% CI for mean (σ known):**
$$\bar{Y} \pm 1.96 \times \frac{\sigma}{\sqrt{n}}$$

**Finding margin of error (backward method):**
$$1.96 = \frac{\text{upper limit} - \hat{p}}{SE} \quad \Rightarrow \quad \text{upper limit} = \hat{p} + 1.96 \times SE$$
$$\text{Margin of error} = \text{upper limit} - \hat{p}$$

---

### Sample Size Determination
$$n = \left(\frac{1.96}{ME}\right)^2 \times p(1-p)$$

If p unknown, use p = 0.5. **Always round UP.** (e.g. 1067.1 → 1068)

---

### Randomised Response Technique (Sensitive Questions)
20 cards: 12 say "not gay", 8 say "gay". Student picks card secretly, answers yes/no.

$$P(\text{Yes}) = P(\text{not gay}) \times \frac{12}{20} + P(\text{gay}) \times \frac{8}{20}$$

Solve for P(gay) if you know P(Yes) from the sample.

---

## CH6 — HYPOTHESIS TESTING

### Setup
- **H₀** = traditional belief (status quo)
- **H₁** = new claim (what you suspect)
- Set **α = 0.05 BEFORE** collecting data

### P-value
$$p\text{-value} = P(\text{result this extreme or more} \mid H_0 \text{ true})$$

**Interpretation:** probability of making a Type 1 error given your data.
- Small p-value (< 0.05) → reject H₀ (safe to do so)
- Large p-value (≥ 0.05) → do NOT reject H₀

---

### Z-Test for Proportion (Large Sample)

$$SE = \sqrt{\frac{p_0(1-p_0)}{n}} \quad \leftarrow \text{USE } p_0 \text{, NOT } \hat{p}!$$

$$Z = \frac{\hat{p} - p_0}{SE}$$

| H₁ | P-value |
|----|--------|
| p > p₀ | P(Z > test stat) = 0.5 − table value |
| p < p₀ | P(Z < test stat) = 0.5 + table value |
| p ≠ p₀ | 2 × P(Z > \|test stat\|) |

---

### AMI Example (Worked)
H₀: p = 0.25, H₁: p > 0.25, n = 500, x = 141

- p̂ = 141/500 = 0.282
- SE = √(0.25×0.75/500) = 0.01936
- Z = (0.282 − 0.25)/0.01936 = **1.6525**
- Table: Z=1.65 → 0.4505; P-value = 0.5 − 0.4505 = **0.0495**
- 0.0495 < 0.05 → **Reject H₀** ✓

---

### Linear Interpolation for P-value
Z = 1.6525, between Z=1.65 (area=0.4505) and Z=1.66 (area=0.4515):

$$\text{Area} = 0.4505 + \frac{1.6525 - 1.65}{1.66 - 1.65} \times (0.4515 - 0.4505) = \mathbf{0.4508}$$

P-value (right tail) = 0.5 − 0.4508 = **0.0492**

---

### Binomial Test (Small Sample)

P-value = P(X ≥ observed | H₀ true)

**Stock prediction: n=10, x=9, H₀: p=0.5**

$$P(X \geq 9 \mid p=0.5) = \binom{10}{9}(0.5)^{10} + \binom{10}{10}(0.5)^{10} = \frac{10+1}{1024} = \mathbf{0.0107}$$

0.0107 < 0.05 → **Reject H₀**

Binomial formula:
$$P(X=k) = \binom{n}{k} p^k (1-p)^{n-k}$$

C(n,k) = n! / (k!(n-k)!) → e.g. C(10,9) = C(10,1) = **10**

---

### Beta (Type 2 Error)
$$\beta = P(\hat{p} < \text{observed } \hat{p} \mid H_1 \text{ true})$$

- α↓ → β↑ (trade-off)
- To decrease BOTH simultaneously → **increase n**

---

### CI vs Hypothesis Testing — Critical Difference!

| | Confidence Interval | Hypothesis Test |
|---|---|---|
| SE uses | **p̂** | **p₀** |
| Goal | Estimate parameter | Test a claimed value |
| Output | Range | Reject/Don't reject |

---

## MEMORY AIDS

**OST** = Objectives → Specific → Timeline (problem definition)

**SQE** = Source → Quality → Ethics (data collection)

**Ethics** = Privacy (anonymity) **AND** Consent (both required)

**Confusion of the inverse**: P(A|B) ≠ P(B|A). Always check which direction you need!

**"At least one" trick**: 1 − P(none). Always faster.

**Z for 95%** = **1.96** (only value you need in this course)

**Sample size: always round UP**

**Hypothesis test SE: always use p₀ (null value), not p̂ (sample)**

**F1 punishes imbalance** between precision and recall

**Gantt=scheduling | Sankey=flow | Radar=multi-dim | Treemap=hierarchy | Choropleth=geographic | Sunburst=hierarchy circular**

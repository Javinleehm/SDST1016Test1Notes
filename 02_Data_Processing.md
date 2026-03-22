# Chapter 2: Problem Definition, Data Collection, Data Cleaning & Preprocessing

---

## Step 1: Problem Definition — The OST Framework

A **good problem definition** must satisfy three criteria, remembered as **OST**:

| Letter | Criterion | Meaning |
|--------|-----------|---------|
| **O** | Objectives | What exactly are you trying to achieve? |
| **S** | Specific | Can you measure whether you achieved it? Quantify the target! |
| **T** | Timeline | How soon? (Also: what time period of data are you using?) |

### Bad vs. Good Problem Definitions

| ❌ Bad | ✅ Good |
|--------|--------|
| "We need to do something about customer leaving our service." | "Reduce customer churn by 15% within the next 30 days." |
| "We need to do something with sales data to make it better." | "Forecast sales with at least 90% accuracy to optimise inventory." |

**Why is bad bad?** Lacks objectives (O), not specific (S), no timeline (T).

---

## Vaccine Efficacy Calculation 🔑 (Testable Calculation!)

The lecturer spent significant time on this. You **must** know this formula.

$$VE = 1 - \frac{P(\text{infection} \mid \text{vaccinated})}{P(\text{infection} \mid \text{placebo})}$$$

### Example: Pfizer COVID Vaccine
- 8 confirmed infections in vaccinated group (n subjects)
- 162 confirmed infections in placebo group (n subjects)
- Same sample size → N cancels

$$$\widehat{VE} = 1 - \frac{8/n}{162/n} = 1 - \frac{8}{162} \approx 0.9506 = 95\%$$$

### What happens with unconfirmed cases?
If you include suspected (unconfirmed) cases:
- Vaccinated: 8 confirmed + 1594 suspected = 1602 total
- Placebo: 162 confirmed + 1816 suspected = 1978 total

$$\widehat{VE} = 1 - \frac{1602/n}{1978/n} = 1 - \frac{1602}{1978} \approx 0.19 = 19\%$

**Therefore, the general efficacy formula (Relative Risk Reduction) is:**

$ Efficacy = 1 - \\frac{Risk_{\text{test group}}}{Risk_{\text{baseline}}} $

> The lesson: definition of what counts as a "case" massively changes the result. Be transparent about your data.

---

## Step 2: Data Collection — The SQE Framework

A complete data collection section must address **SQE**:

| Letter | Criterion | Meaning |
|--------|-----------|---------|
| **S** | Source | Where did you get the data? (e.g., Kaggle, government datasets) |
| **Q** | Quality | Is the data reliable? Has it been validated/double-checked? |
| **E** | Ethics | Is the data ethical? |

### Data Ethics — Two Requirements
For data to be **ethical**, you need **BOTH**:

1. **Privacy / Anonymity** — Cannot trace data back to the individual (no names or IDs shown)
2. **Informed Consent** — You asked the person and they said **yes** before you collected

> Getting anonymity alone is not enough — you still need consent!

### Notable Data Sources
- **Kaggle** (kaggle.com) — Large repository of machine-learning-ready datasets, rigorously quality-checked. The lecturer highly recommends this for projects.
- Government datasets, academic databases, APIs, web scraping

---

## Step 3: Data Cleaning & Preprocessing

Five main tasks:
1. **Outliers** — most important
2. **Missing data / Imputation**
3. **Standardisation**
4. **Normalisation**
5. **Categorical data encoding**

---

### 3a. Outliers (Most Important!) 🔑

#### What is an outlier?
An observation that falls **outside the normal sample range**, defined using the **IQR method**.

#### Step-by-step: How to identify outliers

**Step 1:** Sort data in ascending order.

**Step 2:** Calculate the quartile positions using:
$$$Q1 \text{ position} = \frac{(n+1) \times 1}{4}$$$
$$$\text{Median position} = \frac{(n+1) \times 2}{4}$$$
$$$Q3 \text{ position} = \frac{(n+1) \times 3}{4}$$$

**Step 3:** Use **linear interpolation** to find the exact value if position is not an integer.

> Example: If n = 10, Q1 position = 11/4 = 2.75th observation.
> This is between the 2nd and 3rd observations.
> Q1 = 2nd value + 0.75 × (3rd value - 2nd value)

**Step 4:** Calculate IQR:
$$$IQR = Q3 - Q1$$$

**Step 5:** Calculate the limits:
$$$\text{Lower limit} = Q1 - 1.5 \times IQR$$$
$$$\text{Upper limit} = Q3 + 1.5 \times IQR$$$

**Step 6:** Any observation **below the lower limit** or **above the upper limit** is an **outlier**.

---

#### Linear Interpolation — Worked Example

Given n = 10 observations (sorted): 28, 38, 41, 44, 48, 50, 53, 63, 64, 70

**Q1:** position = (10+1)×1/4 = 11/4 = **2.75**
- Between 2nd (38) and 3rd (41) observations
- Q1 = 38 + **0.75** × (41 - 38) = 38 + 2.25 = **40.25**

**Median:** position = (10+1)×2/4 = 11/2 = **5.5**
- Between 5th (48) and 6th (50) observations
- Median = 48 + **0.5** × (50 - 48) = 48 + 1 = **49**

**Q3:** position = (10+1)×3/4 = 33/4 = **8.25**
- Between 8th (63) and 9th (64) observations
- Q3 = 63 + **0.25** × (64 - 63) = 63 + 0.25 = **63.25**

**IQR** = 63.25 - 40.25 = **23**

**Lower limit** = 40.25 - 1.5 × 23 = 40.25 - 34.5 = **5.75**

**Upper limit** = 63.25 + 1.5 × 23 = 63.25 + 34.5 = **97.75**

Check: All observations are within [5.75, 97.75] → no outliers in this dataset.

---

#### The 1.5 multiplier
- 1.5 is the **default** value (most popular choice)
- Increasing it (e.g., to 2) → **larger range → fewer outliers**
- Decreasing it (e.g., to 1) → **smaller range → more outliers**

#### What to do with outliers?
1. **Go back to the data source** first — is it a typing error? (e.g., 74 vs 47 reversed)
2. If it's a **genuine error** → remove it
3. If it's **not an error** → consider keeping it — outliers sometimes contain the most important information (e.g., Yao Ming is an outlier in Chinese height data but he's genuinely Chinese and genuinely tall)

---

### 3b. Missing Data / Imputation

**Imputation** = filling in missing values with estimated values.

Methods:
- **Mean imputation:** Replace missing value with the column mean (most common)
- **Day-specific imputation:** For time-series data, use the average for that day of the week

> Example from lecture: If Tuesday data is missing, use the average of all *other* Tuesdays in the dataset — not the overall average.

---

### 3c. Standardisation (Z-score Normalisation) 🔑

**Purpose:** Scale data so that mean = 0, standard deviation = 1.

$$$Z_i = \frac{X_i - \bar{X}}{\sigma}$$$

Where:
- $X_i$ = the observation
- $\bar{X}$ = sample mean
- $\sigma$ = standard deviation

**Result:** Z-values have mean 0 and SD 1.

---

### 3d. Min-Max Normalisation 🔑

**Purpose:** Scale data into the range [0, 1].

$$$Y_i = \frac{X_i - \min(X)}{\max(X) - \min(X)}$$$

**Result:** Smallest value → 0, Largest value → 1.

---

### 3e. Categorical Data Encoding

Converting text labels (e.g., "apple", "orange") into numbers.

- **Label Encoding:** apple = 0, orange = 1 (simple numbering)
- **One-Hot Encoding (Binary):** Creates a 0/1 column for each category

> One-hot encoding example:
> - "apple" → [1, 0]
> - "orange" → [0, 1]

---

## Natural Language Processing (NLP) / LSA 🔑

This is a **testable topic** — the lecturer explicitly said he can ask calculation questions on this.

### The Problem
Computers can't directly process text documents (PDFs, articles). We need to convert text into **numerical vectors** that computers can analyse.

### Step 1: Build the Term-Document Matrix (A)

Create a matrix where:
- **Rows** = important keywords extracted from documents
- **Columns** = documents
- **Values** = frequency of each keyword in each document

| | Doc 1 | Doc 2 | Doc 3 | Doc 4 | Doc 5 | Doc 6 |
|---|---|---|---|---|---|---|
| ship | 1 | 0 | 1 | 0 | 0 | 0 |
| boat | 0 | 1 | 0 | 0 | 0 | 1 |
| ocean | 1 | 1 | 0 | 1 | 0 | 0 |
| voyage | 0 | 0 | 1 | 0 | 1 | 0 |
| bulk | 0 | 0 | 0 | 1 | 1 | 0 |

### Step 2: Singular Value Decomposition (SVD)

Decompose the matrix A:

$$$A = U \cdot \Lambda \cdot V^T$$$

Where:
- **U** = word eigenvectors matrix (M × P), used for **word vectors**
- **Λ** = diagonal matrix of **eigenvalues** (P × P)
- **V** = document eigenvectors matrix (N × P), used for **document vectors**

Dimensions: M = number of keywords, N = number of documents, P = number of eigenvalues.

### Step 3: How Much Information is Captured?

**Eigenvalues are arranged in descending order.** The formula for the percentage of information captured by the top R eigenvalues:

$$$\text{Variance captured} = \frac{\sum_{i=1}^{R} \lambda_i^2}{\sum_{i=1}^{P} \lambda_i^2}$$$

> Example: If we keep only the top 2 eigenvalues and this ratio = 90%, then we capture 90% of the information while discarding the other 10%.

### Step 4: Low-Rank Approximation (Keep only top R eigenvalues)

To reduce dimensions (e.g., to 2D for plotting), keep only the top R eigenvalues:
- **Λ₂** = 2×2 diagonal matrix (top 2 eigenvalues only)
- **V₂** = first 2 rows of V^T
- **U₂** = first 2 columns of U

**Document vectors** (coordinates of each document in 2D space):
$$$\text{Document vectors} = \Lambda_2 \cdot V_2^T$$$

Result is a 2×N matrix — each column is one document's (X, Y) coordinate.

**Word vectors** (coordinates of each keyword in 2D space):
$$$\text{Word vectors} = U_2 \cdot \Lambda_2$$$

Result is an M×2 matrix — each row is one keyword's (X, Y) coordinate.

### What Can You Do With Vectors?

Once documents and words are represented as vectors, computers can:
- **Classify** documents into clusters (e.g., "travel articles" vs "legal documents")
- **Identify similar documents** (close vectors = similar content)
- **Build large language models** — ChatGPT works by associating word vectors (predict the next most likely word)

---

### 🔑 Testable NLP Calculations

The lecturer said he can ask:

**Q1:** Given eigenvalues λ₁, λ₂, λ₃, λ₄, λ₅ — if I keep the top 2, what % of information is captured?

$$$\text{Answer} = \frac{\lambda_1^2 + \lambda_2^2}{\lambda_1^2 + \lambda_2^2 + \lambda_3^2 + \lambda_4^2 + \lambda_5^2} \times 100\%$$$

**Q2:** Given Λ₂ and V₂^T, what are the (X, Y) coordinates of Document 3?

Answer: Multiply Λ₂ × V₂^T, then read off column 3.

**Q3:** Given U₂ and Λ₂, what are the (X, Y) coordinates of Word 4?

Answer: Multiply U₂ × Λ₂, then read off row 4.

---

## Summary: The 3 Steps for Test 1

Remember the patterns for Steps 1–3:

| Step | Key Framework | Key Calculation |
|------|---------------|-----------------|
| Problem Definition | **OST** (Objective, Specific, Timeline) | Vaccine Efficacy |
| Data Collection | **SQE** (Source, Quality, Ethics = Privacy + Consent) | None |
| Data Cleaning | Outliers (IQR), Standardisation, Normalisation, Imputation, NLP/LSA | All of the above |




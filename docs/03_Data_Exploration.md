# Chapter 3: Data Exploration and Analysis

---

## Overview: What Is Data Exploration?

Data exploration = extracting **summary statistics** + creating **visualisations** to understand your data before modelling.

Two main parts covered in lecture:
1. **Summary statistics** (mean, median, SD, quartiles, etc.)
2. **Graphical methods** (charts and diagrams)
3. **Hypothesis testing concepts** — Type 1/2 errors (covered in Ch3 supplementary — will be tested)
4. **Confusion Matrix** — accuracy, precision, recall, F1 score (testable!)

---

## Part 1: Summary Statistics

### Measures of Central Tendency

| Measure | Formula | Notes |
|---------|---------|-------|
| **Mean** | `Ȳ = Σ Yᵢ / n` | Sum divided by count |
| **Median** | Middle value when sorted | Use (n+1)×2/4 formula |
| **Mode** | Most frequent value | |

> **Important distinction:**
> - Population SD: divide by N
> - Sample SD: divide by **n−1**
>
> If the lecturer gives you data without saying otherwise → **assume sample data**.

### Sample Standard Deviation (given in formula sheet)

$$S = \sqrt{\frac{1}{n-1} \sum_{i=1}^{n} (Y_i - \bar{Y})^2}$$

### Quartiles & Percentiles (reviewed from Ch2 but also in Ch3)

See [`02_Data_Processing.md`](02_Data_Processing.md) for the full quartile calculation method.

**Quick reminder:**
- Q1 = (n+1)/4 th observation
- Q2 = Median = (n+1)×2/4 th observation
- Q3 = (n+1)×3/4 th observation
- Use linear interpolation if position is not a whole number

---

## Part 2: Graphical Methods

### Standard Charts (already know from secondary school — not tested heavily)
- Bar charts, line charts, histograms, pie charts, box plots, scatter plots, heatmaps

### Fancy Charts — You Need to Know These! 🔑

The lecturer said: *"I can ask what each chart is used for."*

#### 1. Gantt Chart
- **Use:** Project management and scheduling
- **Shows:** Tasks, timelines, dependencies between tasks
- **Key feature:** Who is responsible for each task, overlapping time periods

> Example: A tech company's coding project timeline — machine learning phase must finish before LLM phase can start.

---

#### 2. Sankey/Ribbon Diagram
- **Use:** Showing **flow** or distribution of resources, money, energy, data
- **Shows:** How a total quantity splits into categories, and those into sub-categories
- **Key feature:** Width of ribbon = quantity flowing

> Example: Household budget — total income splits into savings and expenses; expenses split into groceries, schooling, health, transport, housing.

---

#### 3. Radar Chart
- **Use:** Comparing **multiple variables** across different items/categories
- **Shows:** Strengths and weaknesses across many dimensions at once
- **Key feature:** Looks like a web/spider web; outer edge = better performance

> Example: Comparing products (laptop, phone, PC) across dimensions like price, usability, quality, appearance, durability, advertising spend.

---

#### 4. Treemap
- **Use:** Displaying **hierarchical data** and proportions
- **Shows:** Categories and sub-categories as nested rectangles; size = proportion
- **Key feature:** Interactive — click to drill down into subcategories

> Example: Restaurant sales → breakfast/lunch → specific menu items (waffles, eggs, pancakes). Clicking "salad" zooms in to show Caesar salad, French salad, etc.

---

#### 5. Choropleth Map
- **Use:** Displaying **geographical data**
- **Shows:** Regional variations using colour (like a heat map on a geographic map)
- **Key feature:** Red = high value, blue/green = low value; also called a geographic heat map

> Example: Average temperature across different regions of Australia.

---

#### 6. Sunburst Chart
- **Use:** Displaying **hierarchical data** (like tree map but circular)
- **Shows:** Multiple levels of hierarchy in concentric rings
- **Key feature:** More visually appealing for hierarchical nested categories

> Example: Smartphone store sales — brand (Xiaomi, Samsung, Apple) → sub-brand (Redmi, Galaxy S, iPhone) displayed in circular rings.

---

### Quick Reference: Which Chart for Which Purpose?

| Chart | Best For |
|-------|---------|
| Gantt | Project management / scheduling |
| Sankey/Ribbon | Flow of resources / money / energy |
| Radar | Multi-dimensional comparison of performance |
| Treemap | Hierarchical data (interactive drill-down) |
| Choropleth | Geographic / spatial patterns |
| Sunburst | Hierarchical nested data (circular view) |

---

## Part 3: Pivot Tables

A **pivot table** converts a long column of raw data into a summary frequency table.

### One-Way Pivot Table
Summarises one variable:

| Seatbelt usage | Count | Percentage |
|----------------|-------|------------|
| Always | 1,686 | 55.4% |
| Most of the time | 743 | 24.4% |
| Sometimes | 347 | 11.4% |
| Rarely | 266 | 8.7% |

### Two-Way Pivot Table
Summarises two variables simultaneously (e.g., seatbelt usage × gender).

> Note: The lecturer said he would NOT ask about Excel functions in the test (e.g., not asking "what function do you use"). But he CAN ask you to interpret a pivot table.

---

## Part 4: Hypothesis Testing Concepts (Ch3 Supplement) 🔑

These definitions are **testable** — "I can ask you what is Type 1 error."

### The Court Analogy

The legal principle "**innocent until proven guilty**" is the model for hypothesis testing:

| Legal Concept | Statistics Concept |
|---------------|-------------------|
| Innocent (assumed) | **Null hypothesis H₀** = the assumption |
| Guilty | **Alternative hypothesis H₁** = the opposite |
| Evidence | Sample data |
| Conviction decision | Rejecting or not rejecting H₀ |

---

### The Truth Table

| | H₀ is TRUE (innocent) | H₁ is TRUE (guilty) |
|---|---|---|
| **Accept H₀** (find innocent) | ✅ Correct decision | ❌ Type 2 Error |
| **Reject H₀** (find guilty) | ❌ Type 1 Error | ✅ Correct decision |

---

### Type 1 vs Type 2 Error

**Type 1 Error:**
- H₀ is TRUE, but you REJECT it → reject something true
- Lock up an innocent person
- Also called: **False Positive**
- Probability = **α** (significance level, usually 5%)

**Type 2 Error:**
- H₁ is TRUE, but you ACCEPT H₀ → miss a real effect
- Release a guilty criminal
- Also called: **False Negative**
- Probability = **β**

---

### Significance Level (α)

- α = probability of committing a **Type 1 Error**
- Usually set at **α = 0.05** (5%)
- Set **BEFORE** collecting data (not after)
- A small α means you need very strong evidence to reject H₀

---

### Power of a Test

- **Power** = probability of correctly rejecting H₀ when H₁ is true
- Power = P(correct rejection) = probability of the bottom-right box in the truth table
- **P(Type 2 Error) = 1 − Power**

---

### P-value vs Significance Level

| | When set? | Meaning |
|---|---|---|
| **Significance level (α)** | **Before** the test | Your tolerance threshold for Type 1 error (usually 5%) |
| **P-value** | **After** the test | The actual probability of making a Type 1 error given your data |

**Decision rule:** If **p-value < α**, reject H₀.

---

## Part 5: Confusion Matrix 🔑 (Testable Calculations!)

The lecturer explicitly covered this as part of Chapter 3/4, with worked examples.

### Setup: 2×2 Table

| | **Infected (Positive)** | **Healthy Control (Negative)** | **Total** |
|---|---|---|---|
| **Test Positive** | TP (True Positive) | FP (False Positive) | |
| **Test Negative** | FN (False Negative) | TN (True Negative) | |
| **Total** | | | |

**Example data:**
- 400 infected, 400 healthy controls tested
- 280 infected tested positive (TP), 120 infected tested negative (FN)
- 80 healthy tested positive (FP), 320 healthy tested negative (TN)

| | Infected | Control | Total |
|---|---|---|---|
| Test Positive | 280 (TP) | 80 (FP) | 360 |
| Test Negative | 120 (FN) | 320 (TN) | 440 |
| Total | 400 | 400 | 800 |

---

### Four Measures 🔑

**Accuracy** — proportion of all correct predictions:
$$\text{Accuracy} = \frac{TP + TN}{TP + TN + FP + FN} = \frac{280 + 320}{800} = 0.75$$

**Precision** — of all positive predictions, how many are correct?
$$\text{Precision} = \frac{TP}{TP + FP} = \frac{280}{360} = 0.7\overline{7}$$

**Recall (= Sensitivity)** — of all actually positive cases, how many did we catch?
$$\text{Recall} = \frac{TP}{TP + FN} = \frac{280}{400} = 0.70$$

**Specificity** — of all actually negative cases, how many did we correctly identify as negative?
$$\text{Specificity} = \frac{TN}{TN + FP} = \frac{320}{400} = 0.80$$

---

### F1 Score 🔑

Combines precision and recall into one balanced metric:

$$F1 = 2 \times \frac{\text{Precision} \times \text{Recall}}{\text{Precision} + \text{Recall}}$$

$$F1 = 2 \times \frac{0.7778 \times 0.70}{0.7778 + 0.70} = 0.7368$$

#### Key property of F1 Score:
**If Precision and Recall are very unbalanced, the F1 score is dragged towards the lower one.**

| Precision | Recall | Arithmetic Mean | F1 Score |
|-----------|--------|-----------------|----------|
| 0.01 | 0.99 | 0.50 | **0.0198** ← punishes imbalance |
| 0.78 | 0.70 | 0.74 | **0.74** ← balanced, F1 ≈ average |

> F1 score requires **both** precision and recall to be high for a high score. Using just one metric can be misleading.

---

### Memory Aid: Where Each Formula Comes From

| Measure | Uses Rows/Cols | Formula denominator |
|---------|---------------|---------------------|
| Accuracy | Both diagonals | All predictions |
| Precision | First **row** (positive predictions) | TP + FP |
| Recall | First **column** (actually positive) | TP + FN |
| Specificity | Second **column** (actually negative) | TN + FP |

> **Important:** Make sure your table is oriented correctly — TP is always top-left, TN bottom-right. If the table is given differently, flip it before calculating.

---

### Alternative names to know

| Term | Used in... | Same as... |
|------|-----------|-----------|
| Recall | Machine learning | Sensitivity |
| Sensitivity | Medical/public health | Recall |
| F1 Score | ML evaluation | Harmonic mean of precision + recall |

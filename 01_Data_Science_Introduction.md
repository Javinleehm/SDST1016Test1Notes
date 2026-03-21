# Chapter 1: Introduction to Data Science

---

## What Is Data Science?

Data science is a **multidisciplinary field** combining three components:

| Component | Meaning |
|-----------|---------|
| **Statistics** | Hypothesis testing — making an assumption and testing it with data |
| **Computer Science** | The tool/toolbox — programming to process and analyse data |
| **Domain Expertise** | The area of application — what problem are you solving? |

> **Lecturer's emphasis:** When you say "I do data science," make sure you actually *do* data science:
> - Use **real, representative data** (not fake/simulated)
> - Do **actual hypothesis testing** — not just programming
> - Don't just do computer programming and call it data science

---

## The 6 Steps of Data Science

These 6 steps define a data science project. **Every project presentation must include all 6.**

```
1. Problem Definition
2. Data Collection
3. Data Cleaning & Preprocessing
4. Data Exploration & Analysis
5. Model Building & Machine Learning
6. Communication & Visualisation
```

All 6 steps can technically be done with computer programming — but the lecturer stresses that real data science also requires scientific rigour (hypothesis testing, representative data).

---

## The Scientific Mindset

**Hypothesis testing** is the core of doing real science:

1. Form a **hypothesis** (an assumption/belief)
2. Collect **representative data**
3. Check whether the data **supports or refutes** the hypothesis
4. Update your belief accordingly

> **Example:** Newton's laws → worked until more accurate measurements → replaced by Einstein's relativity

---

## Correlation ≠ Causation

One of the most important principles in data science:

- **Correlation:** Two things happening at the same time
- **Causation:** One thing *causes* another

> Example: Taking vitamins and shorter lifespan may be *correlated*, but vitamins don't *cause* shorter lifespan. The real explanation is a **confounding variable** — sick patients (terminal cancer) both take vitamins AND have shorter lifespan regardless.

### Confounding Variable
A **hidden third variable** that explains why two unrelated things appear correlated.

> Example: Soda drinking and teen violence — both are caused by the teen already being violent/at-risk, not by the soda itself.

### When Correlation CAN Imply Causation
Using **causal networks** (additional information + process of elimination), you can sometimes narrow down from many possible causal relationships to just one or two. The video shown in lecture (MinutePhysics: "Correlation CAN imply causation") demonstrates this.

---

## Hypothesis Testing: The 5% Significance Level

The lecturer introduced this concept through the "boy band" example:

- **Null hypothesis (H₀):** If you dress like this and play bubblegum music, you'll be successful
- You collect data: 5 out of 10 boy bands succeed

### Key insight:
**50-50 is NOT strong enough evidence to reject H₀.**

> You need *very strong evidence* before you can reject a null hypothesis (e.g., only 10% succeed = strong evidence against the hypothesis).

The **5% level of significance** (α) means: you must have evidence so strong that there's only a 5% chance you're wrong before you can reject H₀.

---

## Sensationalism in the Media

News headlines pick the most sensational data point — not representative data.

**Always ask:**
1. Is the data representative of the whole population?
2. Is there a confounding variable?
3. Can I form a proper hypothesis and test it?

> Examples discussed in lecture:
> - "Vitamins shorten lifespan" (terminal cancer patients confound the result)
> - "Healthy chef dies at 43" (one data point, not representative)
> - "Soda drinking → teen violence" (confounding variable: pre-existing aggression)

---

## Important Terminology

| Term | Meaning |
|------|---------|
| **Hypothesis** | An assumption or belief you want to test |
| **Null hypothesis (H₀)** | The default assumption (status quo) |
| **Alternative hypothesis (H₁)** | The opposite — what you suspect might be true |
| **Significance level (α)** | Usually 5%; the threshold for rejecting H₀ |
| **Representative data** | Data that captures the full population, not a biased sample |
| **Confounding variable** | A hidden variable that explains a spurious correlation |

---

## Infographics & Visualisation (Step 6 Preview)

The lecturer emphasized infographics as a powerful presentation tool:
- Much better than paragraphs of text
- Shows the same information more attractively
- Tools: **Power BI** (highly recommended), Matplotlib, Tableau

> **Exam tip:** The "communication and visualisation" step is one way to distinguish a good project. Use infographics, not walls of text.

---

## Power BI

The lecturer strongly recommended learning **Power BI** (Microsoft Business Intelligence):
- Combines Excel, Python, R in one tool
- Used in industry for presenting results to managers
- Mentioned on job advertisements as "an advantage"
- Can do data analysis AND visualisation in one place

---

## The 3 Roles in a Data Team

| Role | Focus |
|------|-------|
| **Data Scientist** | Full pipeline: collect, clean, analyse, model, visualise |
| **Data Analyst** | Exploring historical data, answering specific questions |
| **ML Engineer** | Building and deploying machine learning models |

> Note: Not tested directly, but gives context for why data science is interdisciplinary.

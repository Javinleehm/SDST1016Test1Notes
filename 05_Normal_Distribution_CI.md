# Chapter 5: Normal Distribution & Randomized Response Technique

> **Test coverage:** This chapter was NOT covered in Test 1. It will be covered in Test 2.

---

## 5A: The Randomized Response Technique 🔑🔑🔑

### The Problem: Asking Sensitive Questions

Imagine you want to find out: **What percentage of HKU students are gay?**

If you ask directly: *"Are you gay?"* — what will happen?

**Nobody will tell the truth.** Even if someone is gay, they won't admit it because it's a sensitive question. If you ask 250 students directly, you'll probably get **0%** saying yes — which is obviously wrong.

So how do we get honest answers to sensitive questions?

---

### The Solution: Randomized Response Technique

This technique allows you to collect truthful data **while protecting the respondent's privacy**. The key idea: **even if someone answers "yes," you still don't know whether they're actually gay or not.**

#### How It Works (Step by Step):

**Step 1: Prepare the cards**

- Prepare **20 blank cards** (the number can be anything — 20, 30, 40 — it doesn't matter)
- On **12 cards**, write: *"I am NOT gay"*
- On **8 cards**, write: *"I am gay"*

> The numbers 12 and 8 are also arbitrary. You could use any split, as long as you know the exact proportions.

**Step 2: Shuffle and distribute**

- Shuffle all 20 cards thoroughly
- Ask each student to randomly pick **one card**
- Tell them: *"Don't show me the card. Don't tell me what it says. Keep it to yourself."*

**Step 3: Ask the matching question**

Ask each student: **"Does the card correctly describe you? Answer YES or NO."**

- If the card says *"I am NOT gay"* and the student is NOT gay → they say **YES** (card is correct)
- If the card says *"I am gay"* and the student IS gay → they say **YES** (card is correct)
- If the card says *"I am NOT gay"* and the student IS gay → they say **NO** (card is wrong)
- If the card says *"I am gay"* and the student is NOT gay → they say **NO** (card is wrong)

**Step 4: Collect the "yes" responses**

- Out of 250 students, suppose **140 say YES**
- The sample proportion of "yes" = 140/250 = 0.56

---

### The Mathematical Formula

Here's the key equation that makes everything work:

$$P(\text{yes}) = P(\text{not gay}) \times P(\text{card says "not gay"}) + P(\text{gay}) \times P(\text{card says "gay"})$$

Let me break this down:

- **P(yes)** = the proportion of students who said "yes" (we observe this from the data)
- **P(not gay)** = 1 − P(gay) — this is what we're trying to find!
- **P(card says "not gay")** = 12/20 = 0.6 (we set this up)
- **P(card says "gay")** = 8/20 = 0.4 (we set this up)

Substituting:

$$P(\text{yes}) = (1 - P_{\text{gay}}) \times \frac{12}{20} + P_{\text{gay}} \times \frac{8}{20}$$

Now plug in what we know:

$$0.56 = (1 - P_{\text{gay}}) \times 0.6 + P_{\text{gay}} \times 0.4$$

Solve for P_gay:

$$0.56 = 0.6 - 0.6 \times P_{\text{gay}} + 0.4 \times P_{\text{gay}}$$
$$0.56 = 0.6 - 0.2 \times P_{\text{gay}}$$
$$0.2 \times P_{\text{gay}} = 0.6 - 0.56 = 0.04$$
$$P_{\text{gay}} = \frac{0.04}{0.2} = 0.2 = 20\%$$

**Answer: Approximately 20% of HKU students are gay** (according to this example).

---

### Why This Works: The Privacy Protection

The brilliance of this technique is that **when a student says "yes," you still don't know if they're gay or not.**

Think about it:
- A "yes" could mean: they're NOT gay AND picked a "not gay" card
- A "yes" could also mean: they ARE gay AND picked a "gay" card

Since you don't know which card they picked, you can't determine their sexual orientation from their answer alone. This is what encourages honest responses.

---

### Connection to Computer Science: Zero-Knowledge Proof 🔑

In computer science (especially cybersecurity), this same concept is called **Zero-Knowledge Proof**.

**Definition:** A zero-knowledge proof is a method where one party can prove they know something (like a password) without revealing what that something is.

**Examples:**
- **Password verification:** You type your password, the system verifies it's correct, but the system administrator never sees your actual password
- **The randomized response technique:** The student tells you "yes" or "no," but you gain zero knowledge about whether they're gay

> **Exam tip:** If you're asked about this in a test, remember:
> - In **statistics**, it's called the **Randomized Response Technique**
> - In **computer science**, it's called **Zero-Knowledge Proof**
> - They are the SAME concept, just different names in different fields

---

## 5B: Normal Distribution Review

### Standard Normal Distribution

The normal distribution is characterized by:
- **Mean (μ)** — the center
- **Standard deviation (σ)** — the spread

The **standard normal distribution** has μ = 0 and σ = 1.

### Standardization Formula

To convert any normal random variable X to a standard normal Z:

$$Z = \frac{X - \mu}{\sigma}$$

This is the same formula used when calculating the **test statistic** in hypothesis testing.

### Using the Normal Table

The normal table gives you the **area under the curve** from 0 to a given Z-value (the "main area").

To find the **tail area** (the p-value):
- **Right tail:** 0.5 − main area
- **Left tail:** 0.5 − main area (same, by symmetry)

### Linear Interpolation for More Accuracy 🔑

The normal table only gives values for 2 decimal places (e.g., Z = 1.65). But your calculated test statistic might be Z = 1.6525.

To get a more accurate answer, use **linear interpolation** (the proportion method):

**Example:** Find the area for Z = 1.6525

From the table:
- Z = 1.65 → main area = 0.4505
- Z = 1.66 → main area = 0.4515

The value 1.6525 is between 1.65 and 1.66. We need to find the corresponding area between 0.4505 and 0.4515.

**Proportion formula:**

$$\text{Area} = 0.4505 + \frac{1.6525 - 1.65}{1.66 - 1.65} \times (0.4515 - 0.4505)$$

$$= 0.4505 + \frac{0.0025}{0.01} \times 0.0010$$

$$= 0.4505 + 0.25 \times 0.0010 = 0.4505 + 0.00025 = 0.45075$$

Then the **right tail area** (p-value) = 0.5 − 0.45075 = **0.04925**

> **Why this matters:** Without interpolation, you'd get 0.0495. With interpolation, you get 0.04925 — much closer to the exact Excel value. This method is significantly more accurate than just rounding to 2 decimal places.

### Excel Formula

For the most accurate result, use Excel's `NORM.S.DIST` function:

```
=NORM.S.DIST(1.6525, TRUE)
```

This gives the cumulative area from −∞ up to Z = 1.6525.

For the **right tail** (p-value):
```
=1 - NORM.S.DIST(1.6525, TRUE)
```

---

## Quick Reference: Key Formulas

| Concept | Formula |
|---------|---------|
| Randomized Response | P(yes) = (1−P_gay) × P(card A) + P_gay × P(card B) |
| Standardization | Z = (X − μ) / σ |
| Right tail area | 0.5 − main area from table |
| Linear interpolation | Lower + [(exact − lower_Z) / (upper_Z − lower_Z)] × (upper_area − lower_area) |
| Excel right tail | 1 − NORM.S.DIST(Z, TRUE) |

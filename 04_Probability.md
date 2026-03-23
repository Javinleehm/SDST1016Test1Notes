# Chapter 4: Probability (Ch4A + Ch4B)

> **Test 1 coverage:** This is the LAST chapter covered in Test 1. Expect the most calculation questions from this chapter.

---

## 4A: Introduction to Probability

### Basic Definitions

| Term | Definition |
|------|-----------|
| **Random experiment** | A process with at least 2 possible outcomes, with uncertainty about which will occur |
| **Sample space (S)** | The set of all possible outcomes |
| **Event** | A subset of the sample space |
| **Basic outcome** | A single element of the sample space |

**Examples of sample spaces:**
- Toss a coin: S = {H, T}
- Roll a die: S = {1, 2, 3, 4, 5, 6}
- Toss a coin twice: S = {HH, HT, TH, TT}

---

### Axioms of Probability

1. For any event A: `0 ≤ P(A) ≤ 1`
2. The probability of the whole sample space: `P(S) = 1`
3. For mutually exclusive events (no overlap): `P(A₁ ∪ A₂ ∪ ... ∪ Aₖ) = P(A₁) + P(A₂) + ... + P(Aₖ)`

---

### Three Conceptual Approaches to Probability

**1. Classical (Equally Likely Outcomes):**
$$P(A) = \frac{\text{number of outcomes in A}}{\text{total number of outcomes}}$$

**2. Relative Frequency:**
$$P(A) = \frac{\text{times A occurred}}{\text{total number of trials}}$$

**3. Subjective Probability:** Based on personal judgment/belief (e.g., horse racing odds)

---

### The "At Least One" Trick 🔑

This technique was emphasised repeatedly:

$$P(\text{at least one}) = 1 - P(\text{none})$$

It is **much easier** to calculate P(none) and subtract from 1.

---

## The Gambler's Problem 🔑

**Historical context:** Chevalier de Méré (1654, France) posed problems to Pascal and Fermat, leading to the founding of probability theory.

### Game 1: At least one 6 in 4 rolls of a die

P(not getting 6 in one roll) = 5/6

P(not getting 6 in ALL 4 rolls) = (5/6)⁴

$$P(\text{at least one 6 in 4 rolls}) = 1 - \left(\frac{5}{6}\right)^4 = 1 - 0.4823 = \mathbf{0.5177}$$

### Game 2: At least one double-6 in 24 rolls of two dice

P(not getting double-6 in one roll) = 35/36

$$P(\text{at least one double-6 in 24 rolls}) = 1 - \left(\frac{35}{36}\right)^{24} = 1 - 0.5086 = \mathbf{0.4914}$$

> **Key insight:** Méré thought both games were 50-50 (his wrong reasoning: 1/6 × 4 = 2/3 and 1/36 × 24 = 2/3). He was wrong because you can't just multiply — use the complement rule!

---

## Standard Examples

### Rolling Two Dice 🔑

Sample space has **36** equally likely outcomes.

| Event | Count | Probability |
|-------|-------|------------|
| Sum = 2 | 1 | 1/36 = 0.0278 |
| Sum = 6 | 5 | 5/36 = 0.1389 |
| Same number (e.g., 1-1, 2-2, ...) | 6 | 6/36 = 1/6 = 0.1667 |

### Drawing Cards 🔑

Standard deck: 52 cards, 4 suits (spades, hearts, clubs, diamonds), 13 cards per suit.

| Event | Count | Probability |
|-------|-------|------------|
| Diamond | 13 | 13/52 = 1/4 = 0.25 |
| Ace | 4 | 4/52 = 1/13 = 0.0769 |
| Face card (J/Q/K) | 12 = 3×4 | 12/52 = 3/13 = 0.2308 |

---

## The Additive Law of Probability (OR rule)

$$P(A \cup B) = P(A) + P(B) - P(A \cap B)$$

> Subtract the intersection because it was counted twice.

### Mutually Exclusive Events

If A and B **cannot happen at the same time**: `P(A ∩ B) = 0`

Therefore: `P(A ∪ B) = P(A) + P(B)`

---

### Example: Disneyland & Ocean Park 🔑

- P(visited Disneyland, A) = 0.75
- P(visited Ocean Park, B) = 0.85
- P(visited both, A ∩ B) = 0.70
- Sample size n = 200 students

**How many students never visited either?**

Step 1: P(A ∪ B) = 0.75 + 0.85 - 0.70 = **0.90**

Step 2: P(neither) = 1 - 0.90 = **0.10**

Step 3: Number = 0.10 × 200 = **20 students**

---

## Inclusion-Exclusion Principle (3 Events) 🔑

For three events A, B, C:

$$P(A \cup B \cup C) = P(A) + P(B) + P(C) - P(A \cap B) - P(A \cap C) - P(B \cap C) + P(A \cap B \cap C)$$

**Why?** When you add A + B + C, the pairwise intersections are double-counted. Subtract them. But then the triple intersection was counted 3 times and subtracted 3 times (ending up at 0), so you must **add it back once**.

---

### Example: Triple Major 🔑

50 students, each intending to major in:
- A (Statistics): 50%
- B (Risk Management): 70%
- C (Actuarial Science): 20%
- Double major A and B: 15/50 = 30%
- Double major B and C: 5/50 = 10%
- Double major A and C: 5/50 = 10%

Since A ∪ B ∪ C = S (everyone must be in at least one), P(A ∪ B ∪ C) = 1:

$$1 = 0.5 + 0.7 + 0.2 - 0.3 - 0.1 - 0.1 + P(A \cap B \cap C)$$

$$P(A \cap B \cap C) = 1 - (0.5 + 0.7 + 0.2 - 0.3 - 0.1 - 0.1) = 1 - 0.9 = \mathbf{0.1}$$

**10% of students intend to do a triple major.**

---

## 4B: Conditional Probability

### Definition

$$P(A|B) = \frac{P(A \cap B)}{P(B)}$$

Read as: "probability of A **given** B has occurred."

**Rearranged (Multiplicative Law):**
$$P(A \cap B) = P(B) \cdot P(A|B) = P(A) \cdot P(B|A)$$

### Independent Events:
Events A and B are **independent** if:
$$P(A|B) = P(A) \quad \text{or equivalently} \quad P(A \cap B) = P(A) \cdot P(B)$$

---

### Drawing Without Replacement 🔑

#### Example: Apple and Banana Sequence

Basket: a apples and b bananas. Draw without replacement.

**P(apple first AND banana second):**

$$P = P(\text{1st apple}) \times P(\text{2nd banana | 1st apple}) = \frac{a}{a+b} \times \frac{b}{a+b-1}$$

**Longer sequences (e.g., apple, banana, banana, banana, apple with a=10, b=15):**

$$P = \frac{10}{25} \times \frac{15}{24} \times \frac{14}{23} \times \frac{13}{22} \times \frac{9}{21} = 0.0385$$

Pattern: **Numerator changes** based on remaining count of each type; **Denominator decreases by 1 each draw**.

---

#### Example: Candy Urn 🔑

Urn: 2 yellow, 3 orange, 3 green, 2 blue = 10 total.

**(a) P(2 blue):**
$$P = \frac{2}{10} \times \frac{1}{9} = \frac{2}{90} = 0.0222$$

**(b) P(yellow or blue only, 2 draws):**
$$P = \frac{4}{10} \times \frac{3}{9} = \frac{12}{90} = 0.12$$

**(c) P(at most 1 orange):** Use complement!
$$P(\text{at most 1 orange}) = 1 - P(\text{2 orange}) = 1 - \frac{3}{10} \times \frac{2}{9} = 1 - \frac{6}{90} = 0.9\overline{3}$$

---

### Family with Two Children 🔑

Sample space: {GG, GB, BG, BB}, each with probability 0.25.

**(a) P(both girls | at least one is a girl):**

$$P(GG | \text{at least one G}) = \frac{P(GG)}{P(GG) + P(GB) + P(BG)} = \frac{0.25}{0.75} = \mathbf{\frac{1}{3}}$$

**(b) P(both girls | elder child is a girl):**

Event "elder is girl" = {GG, GB}

$$P(GG | \text{elder is G}) = \frac{P(GG)}{P(GG) + P(GB)} = \frac{0.25}{0.50} = \mathbf{\frac{1}{2}}$$

> The key difference: "at least one girl" is less specific than "elder is a girl," so it gives you less information and more uncertainty.

---

## Bayes' Theorem 🔑🔑🔑

This is THE most important concept in Chapter 4.

### The Problem: Confusion of the Inverse

`P(A|B) ≠ P(B|A)` — **do not confuse these!**

Example:
- "I have cancer → test positive" ≠ "Test positive → I have cancer"
- "I smoke → lung cancer" ≠ "I have lung cancer → I smoke"

---

### Bayes' Formula

$$P(A|B) = \frac{P(B|A) \cdot P(A)}{P(B|A) \cdot P(A) + P(B|A^c) \cdot P(A^c)}$$

Where:
- **P(A)** = base rate (prior probability)
- **P(B|A)** = sensitivity (how often the test is positive given disease)
- **P(B|Aᶜ)** = false positive rate = 1 − specificity
- **P(A|B)** = what we want: probability of disease given positive test

---

### Three Methods to Calculate Bayes

The lecturer demonstrated all three. **Tree diagram is the easiest.**

---

#### Method 1: Bayes Formula (direct)

Plug into the formula above.

---

#### Method 2: Hypothetical Table (Most Systematic) 🔑

**Step-by-step procedure** (this is what the lecturer taught in detail):

**Given:**
- Base rate = 1% (P(cancer) = 0.01)
- Sensitivity = 80% (P(positive|cancer) = 0.80)
- Specificity = 90% (P(negative|benign) = 0.90)
- Sample size = 1,000

**Fill in the table IN THIS ORDER:**

| | Malignant (cancer) | Benign (no cancer) | Total |
|---|---|---|---|
| Test + | **8** | **99** | **107** |
| Test − | **2** | **891** | **893** |
| **Total** | **10** | **990** | **1,000** |

Order of calculations:
1. Fill in **total** = 1,000 (given)
2. Cancer patients = 1,000 × 1% = **10**
3. True positives (cancer + positive) = 10 × 80% = **8**
4. False negatives (cancer + negative) = 10 − 8 = **2** (by elimination)
5. Non-cancer patients = 1,000 − 10 = **990**
6. True negatives (no cancer + negative) = 990 × 90% = **891**
7. False positives (no cancer + positive) = 990 − 891 = **99** (by elimination)
8. Fill in row totals: 8+99=107, 2+891=893

**Now answer the question:** P(cancer | positive test) = 8/107 = **7.5%**

> Only 7.5%!! Most doctors would say 75% (they confuse sensitivity with the P we want). This is the **confusion of the inverse**.

---

#### Method 3: Tree Diagram (Easiest) 🔑

```
Start
├── Cancer (0.01)
│   ├── Test + (0.80) → branch probability = 0.008
│   └── Test − (0.20) → branch probability = 0.002
│
└── No Cancer (0.99)
    ├── Test + (0.10) → branch probability = 0.099
    └── Test − (0.90) → branch probability = 0.891
```

P(cancer | test+) = P(cancer AND test+) / P(test+)

`= 0.008 / (0.008 + 0.099) = 0.008 / 0.107 = 7.5%`

---

### Drug User Test Example 🔑

**Given:**
- 5% of population uses drugs (base rate)
- Test is 95% accurate for users (sensitivity)
- Test is 95% accurate for non-users (specificity)
- Sample size = 10,000

| | Drug User | Non-User | Total |
|---|---|---|---|
| Test + | 475 | 475 | **950** |
| Test − | 25 | 9,025 | 9,050 |
| Total | **500** | **9,500** | 10,000 |

**P(drug user | positive test) = 475/950 = 0.50 = 50% (fifty-fifty!)**

> Even though the test is 95% accurate, given a positive result, there's only a 50% chance the person is actually a drug user — because most people don't use drugs (low base rate).

---

### Medical Screening Example (Cancer) 🔑

From the lecturer's supplementary notes (Bayes Rule PDF):
- Base rate = 1%, Sensitivity = 80%, Specificity = 90%, n = 1,000

**P(malignant | positive mammogram) = 8/107 = 7.5%**

This is the key number to remember: the answer is **much lower** than most people expect.

---

## The Monty Hall Problem 🔑

**Setup:** 3 doors, one hides a car, two hide goats.
1. You pick door 3.
2. The host (who knows where the car is) opens door 1 revealing a goat.
3. Should you switch to door 2, or stick with door 3?

**Answer: ALWAYS SWITCH. Switching gives you 2/3 probability of winning.**

**Intuition:** Door 3 had 1/3 probability when you picked it. The host opens one goat door, effectively "transferring" the remaining 2/3 probability to door 2.

**Formal calculation using Bayes:**
- P(car at door 3 | host opens door 1) = 1/3
- P(car at door 2 | host opens door 1) = 2/3

---

## The Birthday Problem 🔑

### Part 1: At least one matching pair among n people

P(no match) = (365/365) × (364/365) × ... × ((365−n+1)/365)

P(at least one match) = 1 − P(no match)

**Result: With only n = 23 people, P(at least one match) > 50%!**

### Part 2: Someone else matches YOUR birthday specifically

P(no one else matches you) = (365/365) × (364/365)^(n-1)

P(someone else matches you) = 1 − (364/365)^(n-1)

**Key difference:** Part 1 is ANY matching pair; Part 2 restricts one person to be you. Part 1 has higher probability because it's less restrictive.

---

## Bags of Coins Example 🔑

Three bags:
- Bag A: 2 gold coins
- Bag B: 2 silver coins
- Bag C: 1 gold, 1 silver

You randomly pick a bag and draw one coin. It's gold. What's the probability the remaining coin is also gold?

**= P(you picked Bag A \| drew gold coin)**

Using Bayes:
$$P(A | G) = \frac{P(G|A) \cdot P(A)}{P(G|A) \cdot P(A) + P(G|B) \cdot P(B) + P(G|C) \cdot P(C)}$$

$$= \frac{1 \times \frac{1}{3}}{1 \times \frac{1}{3} + 0 \times \frac{1}{3} + \frac{1}{2} \times \frac{1}{3}} = \frac{\frac{1}{3}}{\frac{1}{2}} = \mathbf{\frac{2}{3}}$$

P(B\|G) = 0 (no gold in Bag B)

P(C\|G) = 1 − 2/3 − 0 = **1/3** (by elimination)

> Interesting: people instinctively say 1/2, but the correct answer is 2/3.

---

## Conditional Probability (Clinical Trial Example) 🔑

Insomnia study — patients received drug or placebo:

| | Treatment | Placebo | Total |
|---|---|---|---|
| Relapse | 33 | 36 | 69 |
| No Relapse | 40 | 31 | 71 |
| Total | 73 | 67 | 140 |

**P(received placebo \| no relapse):**

$$P(A|B) = \frac{P(A \cap B)}{P(B)} = \frac{31/140}{71/140} = \frac{31}{71} = 0.4366$$

> Shortcut: Fix the condition (No Relapse column = 71 total), find the count for event A (Placebo + No Relapse = 31). Answer = 31/71.

---

## Simpson's Paradox (Conceptual)

Hospital I has lower success rate for both Operation A and Operation B individually, but appears BETTER overall due to different patient mix.

> The aggregated data can be misleading when there's a **lurking variable** (type of operation in this case). This is another example of confounding variables from Ch1.

---

## The "None of the Above" Strategy

From the lecturer's multiple-choice joke:

If you have choices A=1, B=2, C=3, D=None of the above:
- "None of the above" (D) contains an **infinite** number of possibilities
- Choices A, B, C each contain only 1 possibility
- Therefore, **without any knowledge, D is statistically most likely to be correct**
- Caveat: The lecturer said now that you know this, he will never make D the answer!

---

## Quick Reference: Formulas Summary

| Formula | Equation |
|---------|---------|
| Addition rule | `P(A∪B) = P(A) + P(B) − P(A∩B)` |
| Complement | `P(Aᶜ) = 1 − P(A)` |
| "At least one" | `P(at least 1) = 1 − P(none)` |
| Multiplicative law | `P(A∩B) = P(A) · P(B\|A)` |
| Conditional | `P(A\|B) = P(A∩B) / P(B)` |
| Independence | `P(A\|B) = P(A)` or `P(A∩B) = P(A)·P(B)` |
| Bayes | `P(A\|B) = [P(B\|A)·P(A)] / [P(B\|A)·P(A) + P(B\|Aᶜ)·P(Aᶜ)]` |
| Inclusion-exclusion | `P(A∪B∪C) = P(A)+P(B)+P(C)−P(AB)−P(AC)−P(BC)+P(ABC)` |

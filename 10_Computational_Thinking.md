# Chapter 10: Computational Thinking & The Transformer Architecture

> **Test coverage:** This chapter will be covered in Test 2. Expect conceptual questions comparing traditional programming vs. machine learning, and terminology questions about the transformer architecture.

---

## 10A: Traditional Programming vs. Machine Learning 🔑🔑🔑

### The Fundamental Difference

The lecturer emphasized that understanding the difference between traditional programming and machine learning is crucial. The decision tree model is the perfect tool to illustrate these differences.

### Six Key Differences

| # | Aspect | Traditional Programming | Machine Learning |
|---|--------|------------------------|------------------|
| 1 | **Input** | Rules + Data | Data + Answers (labels) |
| 2 | **Output** | Answers (results) | Rules (model/equation) |
| 3 | **Logic** | If-then-else statements | Patterns learned from data |
| 4 | **Adaptability** | Fixed rules, doesn't improve | Learns and improves with more data |
| 5 | **Complexity** | Good for simple, well-defined tasks | Good for complex, pattern-recognition tasks |
| 6 | **Maintenance** | Update rules manually | Retrain with new data |

### Illustrated with Decision Tree

**Traditional Programming Approach:**
```python
if occupation == "B":
    return "Happy"
elif sex == "Male":
    return "Unhappy"
else:
    return "Happy"
```
- A human programmer writes the rules
- Rules are fixed and don't change unless manually updated

**Machine Learning Approach:**
- The computer looks at the data
- It discovers the rules itself (the decision tree structure)
- If given more data, it can update and improve the rules

### Why Machine Learning?

Some problems are too complex for humans to write explicit rules:
- **Image recognition:** How do you write rules to identify a cat in a photo?
- **Natural language processing:** How do you write rules to understand sentiment in text?
- **Medical diagnosis:** How do you write rules to predict disease from symptoms?

Machine learning lets the computer discover patterns that humans might miss.

---

## 10B: The Transformer Architecture 🔑🔑🔑

### Why Learn About Transformers?

The lecturer emphasized this heavily:

> "The transformer architecture is the basis for all LLMs (Large Language Models). If you want to work in AI or IT after graduation, you MUST know the terminology and logical flow of transformers."

Even though you can't do transformer calculations by hand (they're far too complex), understanding the concepts and terminology is essential for your career.

### What is a Transformer?

A **transformer** is a neural network architecture designed to process sequential data (like text) using a mechanism called **self-attention**. It was introduced in the 2017 paper "Attention Is All You Need" by Vaswani et al.

All modern AI models (ChatGPT, Claude, Gemini, etc.) are based on the transformer architecture.

---

### Key Terminology 🔑

| Term | Definition |
|------|-----------|
| **Token** | A piece of text (word, sub-word, or character) that the model processes |
| **Embedding** | A numerical vector representation of a token that captures its meaning |
| **Self-Attention** | A mechanism that lets each token "pay attention" to all other tokens in the sequence |
| **Encoder** | The part of the transformer that processes the input sequence |
| **Decoder** | The part of the transformer that generates the output sequence |
| **Positional Encoding** | Information added to embeddings to preserve the order of tokens |
| **Multi-Head Attention** | Running the attention mechanism multiple times in parallel to capture different types of relationships |
| **Feed-Forward Network** | A simple neural network layer applied after attention |
| **Layer Normalization** | A technique to stabilize training by normalizing activations |
| **Residual Connection** | Adding the input to the output of a layer to help gradients flow |

---

### The Logical Flow of a Transformer

#### Step 1: Input Processing

1. **Tokenization:** The input text is split into tokens
   - Example: "I love data science" → ["I", "love", "data", "science"]

2. **Embedding:** Each token is converted to a numerical vector
   - Each word becomes a vector of numbers (e.g., 512 dimensions)
   - Similar words have similar vectors

3. **Positional Encoding:** Position information is added to embeddings
   - Since transformers process all tokens simultaneously (unlike RNNs), they need explicit position information
   - "I love data" is different from "data love I"

#### Step 2: Encoder Stack

The encoder processes the input through multiple identical layers. Each layer has:

1. **Multi-Head Self-Attention:**
   - Each token looks at every other token
   - Determines how much "attention" to pay to each other token
   - Example: In "The bank of the river," "bank" pays attention to "river" to understand it means a riverbank, not a financial bank

2. **Feed-Forward Network:**
   - Processes the attention-weighted representations
   - Applies non-linear transformations

3. **Residual Connections + Layer Normalization:**
   - Added after each sub-layer to stabilize training

#### Step 3: Decoder Stack

The decoder generates the output one token at a time. Each layer has:

1. **Masked Multi-Head Self-Attention:**
   - Similar to encoder attention, but "masked" so tokens can only attend to previous tokens (not future ones)
   - This prevents the model from "cheating" by looking at the answer

2. **Multi-Head Cross-Attention:**
   - The decoder attends to the encoder's output
   - This connects the input understanding to the output generation

3. **Feed-Forward Network:**
   - Same as encoder

4. **Residual Connections + Layer Normalization:**
   - Same as encoder

#### Step 4: Output Generation

1. **Linear Layer:** Projects the decoder output to vocabulary size
2. **Softmax:** Converts scores to probabilities for each possible next token
3. **Sampling:** The token with the highest probability is chosen (or sampled)
4. **Repeat:** The process repeats, feeding the generated token back into the decoder

---

### Visual Summary

```
Input Text
    ↓
Tokenization
    ↓
Embedding + Positional Encoding
    ↓
┌─────────────────────────┐
│     ENCODER STACK       │
│  ┌───────────────────┐  │
│  │ Multi-Head Self-  │  │
│  │ Attention         │  │
│  ├───────────────────┤  │
│  │ Feed-Forward Net  │  │
│  └───────────────────┘  │
│  (repeated N times)     │
└─────────────────────────┘
    ↓
┌─────────────────────────┐
│     DECODER STACK       │
│  ┌───────────────────┐  │
│  │ Masked Self-      │  │
│  │ Attention         │  │
│  ├───────────────────┤  │
│  │ Cross-Attention   │  │
│  ├───────────────────┤  │
│  │ Feed-Forward Net  │  │
│  └───────────────────┘  │
│  (repeated N times)     │
└─────────────────────────┘
    ↓
Linear + Softmax
    ↓
Output Text (token by token)
```

---

### Why Transformers Are Revolutionary

1. **Parallel Processing:** Unlike RNNs, transformers process all tokens simultaneously, making them much faster to train
2. **Long-Range Dependencies:** Self-attention can connect any two tokens regardless of distance
3. **Scalability:** Transformers scale well with more data and compute power
4. **Transfer Learning:** Pre-trained transformers can be fine-tuned for many different tasks

### Real-World Applications

| Application | How Transformers Help |
|-------------|----------------------|
| **ChatGPT** | Generates human-like text responses |
| **Translation** | Translates between languages with context awareness |
| **Summarization** | Condenses long documents into key points |
| **Code Generation** | Writes programming code from natural language descriptions |
| **Image Generation** | Variants (Vision Transformers) generate and understand images |

---

## Quick Reference: Key Concepts

| Concept | Description |
|---------|-------------|
| Traditional Programming | Human writes rules → rules process data → produce answers |
| Machine Learning | Data + answers → computer learns rules → applies to new data |
| Transformer | Neural network using self-attention for sequence processing |
| Token | Smallest unit of text processed by the model |
| Embedding | Numerical representation of a token's meaning |
| Self-Attention | Mechanism for tokens to relate to each other |
| Encoder | Processes input understanding |
| Decoder | Generates output |

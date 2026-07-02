# Inference

## Overview

Inference is the process of using a trained Large Language Model (LLM) to generate predictions or responses for new input.

Unlike training, where the model learns by updating its weights, inference uses the trained model to generate output without modifying its parameters.

Every time you interact with an LLM, you are performing inference.

---

## Training vs Inference

| Training | Inference |
|----------|-----------|
| Learns from data | Uses learned knowledge |
| Updates model weights | Model weights remain fixed |
| Requires backpropagation | Only forward pass |
| Computationally expensive | Optimized for low latency |

---

## How Inference Works

```mermaid
flowchart LR

A[User Prompt]
B[Tokenizer]
C[Token IDs]
D[Embeddings]
E[Transformer]
F[Logits]
G[Sampling]
H[Next Token]
I[Repeat Until Complete]

A --> B --> C --> D --> E --> F --> G --> H --> I
I --> E
```

---

## Step 1: Tokenization

The input text is converted into tokens.

Example:

```text
Explain how AI works.

↓

[1256, 8421, 991, 430]
```

---

## Step 2: Embeddings

Each token ID is converted into a dense vector representation.

These embeddings capture semantic information and become the input to the Transformer.

---

## Step 3: Transformer Forward Pass

The Transformer processes all input tokens using:

- Self-attention
- Feed-forward layers
- Residual connections
- Layer normalization

The result is a contextual representation for every token.

---

## Step 4: Logits

The model predicts a score (called a **logit**) for every token in its vocabulary.

Example:

| Token | Logit |
|--------|------:|
| AI | 8.2 |
| ML | 5.9 |
| Computer | 3.4 |
| Pizza | -1.2 |

Logits are raw scores, not probabilities.

---

## Step 5: Convert Logits to Probabilities

A **softmax** function converts logits into probabilities.

Example:

| Token | Probability |
|--------|------------:|
| AI | 72% |
| ML | 18% |
| Computer | 8% |
| Pizza | 2% |

---

## Step 6: Token Selection (Sampling)

The model selects the next token.

Common strategies include:

- Greedy decoding
- Temperature sampling
- Top-k sampling
- Top-p (nucleus) sampling

The selected token is appended to the sequence.

---

## Step 7: Repeat

The newly generated token becomes part of the input.

The model repeats the process until:

- An end-of-sequence token is generated
- The maximum token limit is reached
- A stop sequence is encountered

This is called **autoregressive generation**.

---

## Example

Prompt:

```text
The capital of France is
```

Generation:

```text
The
↓

capital
↓

of
↓

France
↓

is
↓

Paris
↓

.
```

Each token is generated one at a time.

---

## Streaming Responses

Many AI applications stream tokens as they are generated instead of waiting for the full response.

Benefits:

- Faster perceived response time
- Better user experience
- Supports real-time chat interfaces

---

## Production Considerations

Inference performance depends on several factors:

- Model size
- Context window length
- Hardware (CPU vs GPU)
- Batch size
- KV Cache
- Quantization

Production systems often optimize inference using:

- KV Cache
- FP16/BF16 precision
- Quantization
- Request batching
- Efficient serving frameworks

---

## Python Example

Using the OpenAI Python SDK:

```python
from openai import OpenAI

client = OpenAI()

response = client.responses.create(
    model="gpt-5",
    input="Explain inference in LLMs."
)

print(response.output_text)
```

---

## Interview Answer (30 sec)

> Inference is the process of using a trained LLM to generate predictions for new input. During inference, the model performs only a forward pass, computes logits for the next token, converts them into probabilities, selects the next token using a decoding strategy, and repeats this process until the response is complete.

---

## Interview Answer (2 min)

Inference begins by tokenizing the user's prompt and converting the token IDs into embeddings. These embeddings pass through the Transformer, which uses self-attention and feed-forward layers to produce contextual representations. The model then computes logits for every token in its vocabulary, converts them into probabilities using softmax, and selects the next token using a decoding strategy such as greedy decoding or top-p sampling.

The generated token is appended to the input, and the process repeats one token at a time until the response is complete. Unlike training, inference does not update model weights. Production systems optimize inference using techniques like KV cache, quantization, batching, and GPU acceleration to reduce latency and cost.

---

## Common Follow-up Questions

### Why is inference slower than reading a sentence?

Because the model generates one token at a time, and each token requires a forward pass through the Transformer.

---

### Does the model generate an entire paragraph at once?

No.

It generates one token at a time in an autoregressive manner.

---

### What are logits?

Logits are the raw prediction scores for every token in the vocabulary before they are converted into probabilities.

---

### What determines which token is generated?

The decoding strategy, such as greedy decoding, temperature sampling, top-k, or top-p sampling.

---

### Does inference change the model?

No.

Inference uses the learned weights but does not update them.

---

## References

- Attention Is All You Need (2017)
- The Illustrated Transformer
- Hugging Face – Text Generation
- OpenAI API Documentation

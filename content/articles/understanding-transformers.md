---
title: "Understanding Transformers: Two Approaches"
date: "2025-11-06"
---

I've spent the last week or so building two educational projects to understand how transformer models work. It started as an overview, but after I got the high level, I wanted to dig deeper and see all the math.So now you can too...every calculation, every design choice, every gradient flowing backward through the network.

The first project is a [complete transformer implementation](https://www.zhubert.com/transformer) in PyTorch. The second is a [step-by-step walkthrough](https://www.zhubert.com/attention-to-detail) of every single calculation in training a tiny transformer model by hand. They're companions to each other - one shows you how to build a working model, the other shows you exactly what's happening under the hood.

## Why Build This?

Large language models like GPT, Claude, and others have become essential tools for developers and researchers. But understanding how they actually work requires getting your hands dirty with the mathematics and code.

I wanted to move beyond treating transformers as black boxes. So Claude, ironically, built them from scratch for me, documented every component, and calculated every derivative with its digital hand.

## The Transformer Project

The [transformer project](https://github.com/zhubert/transformer) is a complete decoder-only transformer (GPT architecture) built in PyTorch. It includes everything you need to train and understand a real language model:

**Core Architecture**

- Multi-head self-attention with KV-cache optimization
- Positional embeddings (learned, not sinusoidal)
- Feed-forward networks with GELU activation
- Pre-layer normalization architecture
- Residual connections throughout

**Training Pipeline**

- Streams from HuggingFace's FineWeb dataset (10 billion tokens)
- Gradient accumulation for stable training
- Learning rate scheduling with warmup and cosine decay
- Train/val split for monitoring progress

**Text Generation**

- Advanced sampling strategies (greedy, top-k, top-p, combined)
- KV-cache optimization that speeds up generation by 2-50x
- Interactive CLI for easy experimentation

**Interpretability Tools**

- Logit lens: visualize how predictions evolve through layers
- Attention analysis: understand what each head focuses on
- Induction head detection: find pattern-matching circuits
- Activation patching: test which components are causally responsible for behaviors

Every component includes extensive documentation explaining not just what it does, but why it's designed that way. The code prioritizes clarity over performance - this is for learning, not production. I've tested my patience trying to finish a full run on my AMD GPU, but have restarted multiple times. Soon I'll probably have a checkpoint to share.

## Attention to Detail

The [attention-to-detail project](https://github.com/zhubert/attention-to-detail) takes a different approach. Instead of building a full model, it walks through every single calculation in training a tiny transformer:

**What "by hand" means:**

- 16-dimensional embeddings (vs GPT-3's 12,288)
- 2 attention heads (vs GPT-3's 96)
- 1 transformer layer (vs GPT-3's 96)
- Training text: "I love transformers"

The project shows all calculations step-by-step:

- Forward pass: tokenization, embeddings, attention, feed-forward, loss
- Backward pass: gradients for every parameter using backpropagation and chain rule
- Optimization: AdamW updates with momentum and adaptive learning rates

This isn't about memorizing formulas. It's about building intuition by seeing the actual numbers flow through the network. Every matrix multiplication is shown in full. Every Jacobian is derived. Every gradient is calculated explicitly.

The documentation includes interactive math rendering, color-coded matrices, and Python scripts you can run to verify every calculation yourself. No PyTorch, no NumPy.

## What I Learned

**From the transformer implementation:**

- How attention mechanisms actually compute relevance between tokens
- Why KV-caching makes such a dramatic difference in generation speed
- What induction heads are and why they're crucial for in-context learning
- How activation patching reveals causal structure in neural networks

**From the manual calculations:**

- Why softmax gradients involve Jacobian matrices
- How layer normalization affects gradient flow
- Why AdamW uses both first and second moment estimates
- The actual shapes and values flowing through a transformer at each step

## Two Paths to Understanding

These projects represent two complementary approaches to learning:

The transformer implementation lets you build something real. You can train it on actual data, generate text, and use interpretability tools to understand what it learned. It's practical and complete, albeit extremely rudimentary and not very effective.

The manual calculations force you to understand the mathematics deeply. You can't hand-wave away a Jacobian matrix when you're calculating every element by hand. It's rigorous and foundational and quite a lot of decimals.

Together, they provide both breadth and depth. The transformer shows you what's possible. The manual calculations show you why it works.

## Getting Started

Both projects are on GitHub but the documentation is more readable:

- [Transformer](https://www.zhubert.com/transformer) - Full PyTorch implementation with training, generation, and interpretability
- [Attention to Detail](https://www.zhubert.com/attention-to-detail) - Step-by-step manual calculations

If you're interested in understanding how modern LLMs work, I'd suggest starting with the transformer project. Read through the core components in order: attention, embeddings, feedforward, blocks, model. Then try the manual calculations to see exactly what's happening at each step.

These are learning resources, built to prioritize understanding over everything else. Hopefully you find them useful too!

---
title: "How Text Becomes an Image"
date: "2025-12-03"
---

After building [transformer implementations](https://www.zhubert.com/articles/understanding-transformers/) to understand how LLMs work, I got curious about image generation. How does a model turn "a cat wearing a tiny hat" into an actual picture of a cat wearing a tiny hat? It's an area with a lot of ongoing research, and I wanted to understand the fundamentals.

So Claude and I built [text-to-image](https://github.com/zhubert/text-to-image), an educational project that constructs a complete text-to-image system from scratch in five progressive phases. Each phase adds one key concept, building from pure noise all the way to natural language control.

## Why Flow Matching?

Most tutorials on image generation start with diffusion models and their complex noise schedules. But there's a cleaner formulation called flow matching that makes the math far more intuitive.

The core idea is simple: you have noise (x₀) and you have a real image (x₁). Flow matching learns the velocity field that moves you from one to the other. The model predicts `v = x₁ - x₀` (literally just the direction from data toward noise). To generate, you start with random noise and integrate backward along that learned velocity field.

No Markov chains, no complicated variance schedules. Just straight lines in latent space.

## The Five Phases

The project works through image generation incrementally, with each phase introducing one new concept:

**Phase 1: Unconditional Flow Matching**

Start with the absolute basics. Train a simple CNN on MNIST to predict velocity fields. The model learns to generate digits, but has no control over which digit appears. This phase establishes the training loop and sampling algorithm.

**Phase 2: Diffusion Transformer (DiT)**

Replace the CNN with a transformer. Images get split into patches and treated as tokens, just like words in an LLM. This is the architecture behind modern systems like DALL-E 3 and Stable Diffusion 3.

The shift to transformers gives you global attention (every patch can attend to every other patch) which dramatically improves coherence over convolutional approaches.

**Phase 3: Class-Conditional Generation**

Now we add control. The model learns embeddings for each digit class (0-9), and we can specify which digit to generate. This phase introduces Classifier-Free Guidance (CFG), the technique that lets you amplify how strongly the model follows your conditioning.

The trick is elegant: train with 10% random label dropping, then at inference time blend the conditional and unconditional predictions. Crank up the guidance scale and the model follows your instructions more faithfully.

**Phase 4: Text Conditioning with CLIP**

Discrete labels are limiting. Phase 4 swaps them for natural language using a pretrained CLIP encoder. Now instead of "generate digit 7" you can say "the number seven" or "a lucky number" and get coherent results.

Cross-attention connects image patches to text tokens, letting the model learn which parts of the image should correspond to which words. The same CFG trick works here (just drop the text 10% of the time during training).

**Phase 5: Latent Diffusion**

Finally, efficiency. Working in pixel space is expensive. A 256×256 image has nearly 200,000 dimensions. Latent diffusion compresses images through a VAE first, reducing dimensionality by 48×.

This is how Stable Diffusion works in practice. Train the generative model in latent space, then decode to pixels at the end. Same quality, fraction of the compute.

## Getting Started

The project lives on [GitHub](https://github.com/zhubert/text-to-image), and the Jupyter notebooks showing all the work are posted at [zhubert.com/text-to-image](https://www.zhubert.com/text-to-image).

Each notebook is self-contained with training code, sampling utilities, and explanations of the underlying math. The codebase runs on Apple Silicon, CUDA, or CPU (though I recommend GPU for anything past Phase 2).

If you want to understand how modern image generation works, start with Phase 1 and work through sequentially. Each phase builds directly on the last.

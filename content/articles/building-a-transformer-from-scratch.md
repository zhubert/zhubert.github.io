---
title: "Building a Transformer from Scratch"
date: "2025-11-06"
---

Here's the thing about modern AI: we use it every day, but most of us (myself included, until recently) have only the vaguest idea how it actually works under the hood.

Sure, I knew the buzzwords. Attention mechanisms. Self-attention. Multi-head attention. Embeddings. The whole "Attention is All You Need" paper everyone references but few have actually read.

But knowing the vocabulary isn't the same as understanding the thing.

## The Black Box Problem

I've been writing code for decades now. Built pricing algorithms at Amazon. Founded a social network that scaled to nearly a million users. Published a novel about AI gone rogue. (The irony is not lost on me.)

And yet, when ChatGPT dropped and everyone started building with LLMs, I realized I was working with a technology I didn't truly understand. I was treating transformers like a black box — prompts go in, tokens come out, something something magic happens in between.

That bugged me.

I don't like not understanding my tools. So I did what I always do when I want to learn something: I built it from scratch.

## From First Principles

The project was straightforward in concept: implement a decoder-only transformer in PyTorch. No shortcuts. No importing someone else's attention layer and calling it good.

Embeddings? Built from scratch.

Positional encodings? From scratch.

Multi-head self-attention? You guessed it.

And here's what I learned: transformers aren't actually that complicated once you build one yourself. They're elegant, really. The attention mechanism is just a way of letting each token "look at" every other token and decide which ones are important for the task at hand.

(It's linear algebra all the way down, of course, but the concept is surprisingly intuitive once you see it in action.)

## Interpretability Tools

The best part about building your own transformer? You can poke around inside it while it's running. I added interpretability tools so I could actually see what the model was paying attention to at each layer.

Turns out, attention patterns are fascinating. Early layers tend to focus on syntax and nearby words. Deeper layers start picking up semantic relationships — things that are related in meaning even if they're far apart in the sentence.

You don't see that when you're just calling an API.

## Why Bother?

Someone will ask: why build this yourself when there are perfectly good implementations already out there?

Two reasons.

First, because reading code isn't the same as writing it. You can stare at the PyTorch source for hours and still not have the intuition that comes from implementing it yourself.

Second, because I'm not satisfied being a user of tools I don't understand. I don't need to be an expert in everything, but for the technologies that matter? I want to know how they work.

Not at a surface level. At the level where I could rebuild it if I had to.

## The Slope Continues

This project reminded me of something I've written about before: the power of incremental work. I didn't build this transformer in a weekend. It was an hour here, a Saturday morning there, slowly chipping away at the mountain.

But eventually, the pieces came together. And now when I read papers about the latest architecture improvements or talk to colleagues about model optimization, I'm not just nodding along.

I actually know what they're talking about.

That's worth the investment.

---

If you're curious to see the implementation, the code is up on GitHub: [transformer](https://www.zhubert.com/transformer). Fair warning: it's not production code. It's learning code. Messy in places, over-commented in others, exactly what you'd expect from someone working through first principles.

But it works. And more importantly, I understand it.

That's the whole point.

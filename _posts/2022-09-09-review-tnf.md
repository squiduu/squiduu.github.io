---
title:  "[논문 리뷰] Taking Notes on the Fly Helps Language Pre-Training (TNF)"
tags:
  - Language Modeling
use_math: true
---

### Information
> Task: Language modeling \
> Publisher: ICLR \
> Year: 2021 \
> [Paper Link](https://openreview.net/pdf?id=lU5Rs_wCweN)

### Abstract
1. Creating a note dict for rare words in training corpus makes the pre-training faster and stable
2. Introducing note embedding to update and maintain the note dict

### Method
1. Contruction of note dictionary\
![0](https://squiduu.github.io/assets/images/review/tnf/0.png)
The left box shows the forward pass with the help of the note dictionary. In the input word sequence, $w_2$ is a rare word. Then for tokens 4 and 5 originated from $w_2$, we query the value of $w_2$ in the note dictionary and weighted average it with token/position embeddings. The right box demonstrates how we maintain the note dictionary. After the forward pass of the model, we can get the contextual representations of the word near $w_2$ and use mean pooling over those representations as the note of $w_2$ in the current sentence. Then, we update $w_2$’s value in the note dictionary by a weighted average of the current note and its previous value.

2. Maintaining of note dictionary\
For a rare word $w$ that appears both in the input token sequence $x = \{x_1, ..., x_i, ..., x_n\}$ and note dict, denoting the span boundary of $w$ in $x$ as $(s,t)$, where $s$ and $t$ are the starting and ending position. The note of $w$ for $x$ as
    
    $$Note(w,x) = \frac{1}{2k + t - s} \sum_{j=s-k}^{t+k}\bold{c}_j$$
    
    where $\bold{c}_j \in \mathbb{R}^d$ si the output of the encoder on position $j$ and served as the contextual representation of $x_j$, $k$ is half of the window size that controls how many surrounding tokens we want to take as notes and save their semantics.
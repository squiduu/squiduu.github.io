---
title:  "[논문 리뷰] Exploiting Cloze Questions for Few Shot Text Classification and Natural Language Inference (PET)"
tags:
  - Language Modeling
use_math: true
---

### Information
> Task: Language modeling \
> Publisher: EACL \
> Year: 2021 \
> [Paper Link](https://arxiv.org/pdf/2001.07676.pdf)

## Main
### Architecture
![0](https://squiduu.github.io/assets/img/review/pet/0.png)
An example of PET for sentiment classification
1. A pre-trained language model is fine-tuned with patterns from labeled training data $\mathcal{T}$
2. Ensemble of fine-tuned models annotates unlabeled data $\mathcal{D}$
3. A classifier is trained on the resulting soft-labeled original and additional dataset
![1](https://squiduu.github.io/assets/img/review/pet/1.png)
Schematic representation of PET and iPET
1. Initial training set $\mathcal{T}$ is used to finetune an ensemble of pre-trained models $\mathcal{M}_n$
2. For each model, a random subset of other models generates a new training set by labeling examples from unlabeled data $\mathcal{D}$
3. A new set of PET models is trained using the larger, model-specific datasets $\mathcal{T}_n^k$
4. Previous two steps are repeated $k$ times, each time increasing the size of the generated training sets
5. The final set of models is used to create a soft-labeled dataset $\mathcal{T}_C$
6. A classifier $C$ is trained on this dataset $\mathcal{T}_C$

### Patterns
Defined patterns for an input text in Yelp dataset are
![2](https://squiduu.github.io/assets/img/review/pet/2.png)
Defined verbalizer $v$ for all patterns are
![3](https://squiduu.github.io/assets/img/review/pet/3.png)

### Discussion
Introduced PET to learn with unlabeled data with labels created by ensemble of pre-trained LMs\
It proved that generated labels with pre-trained LMs can be helpful for few-shot learning\
Using knowledge distillation from an ensemble of pre-trained LMs and augmented unlabeled data
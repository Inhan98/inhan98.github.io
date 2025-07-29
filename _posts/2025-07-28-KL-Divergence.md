---
layout: default 
title: KL Divergence
date: 2025-07-28 21:20 +0100
categories: [Machine Learning, Loss Function]
tags: [Machine Learning]
author: <author_id>
toc: true
comments: true
---


# What is KL Divergence?

KL Divergence (Kullback–Leibler Divergence) is a measure of how one probability distribution $Q$ diverges from a reference probability distribution $P$. 

In simple terms, KL Divergence quantifies the **extra amount of information** required to represent samples from $P$ using the distribution $Q$.

## Formula

For **discrete** probability distributions, KL Divergence is defined as:

$$
D_{\text{KL}}(P \parallel Q) = \sum_{x} P(x) \log \frac{P(x)}{Q(x)}
$$

For **continuous** distributions, it is defined as:

$$
D_{\text{KL}}(P \parallel Q) = \int P(x) \log \frac{P(x)}{Q(x)} \, dx
$$

Where:

* $P(x)$: True distribution
* $Q(x)$: Approximated or model distribution
* $\log$: Typically the natural logarithm ($\ln$)

## Properties

* **Asymmetry**: $D_{\text{KL}}(P \parallel Q) \ne D_{\text{KL}}(Q \parallel P)$
* **Non-negative**: $D_{\text{KL}}(P \parallel Q) \ge 0$ (Gibbs' inequality)
* $D_{\text{KL}}(P \parallel Q) = 0$ if and only if $P = Q$ (almost everywhere)

### Proof of Non-negativeness of KLD

We start by rewriting the KL divergence in a form that invites Jensen’s inequality. Observe:

$$
\begin{aligned}
D_{\mathrm{KL}}(P \parallel Q)
&= \sum_x P(x)\,\log\frac{P(x)}{Q(x)}
= -\sum_x P(x)\,\log\frac{Q(x)}{P(x)}. \\
\end{aligned}
$$

Define the random variable

$$
  Z = \frac{Q(X)}{P(X)},
$$

where $X$ is drawn according to distribution $P$. Then

$$
  D_{\mathrm{KL}}(P \parallel Q)
  = -\mathbb{E}_{X\sim P}\bigl[\log Z\bigr].
$$

Since $f(t) = -\log t$ is convex, Jensen’s inequality gives:

$$
\begin{aligned}
-\mathbb{E}[\log Z]
&= \mathbb{E}\bigl[\,f(Z)\bigr]
\;\ge\; f\bigl(\mathbb{E}[Z]\bigr)
= -\log\bigl(\mathbb{E}[Z]\bigr).
\end{aligned}
$$

But

$$
\mathbb{E}[Z]
= \sum_x P(x)\,\frac{Q(x)}{P(x)}
= \sum_x Q(x)
= 1.
$$

Hence

$$
  D_{\mathrm{KL}}(P \parallel Q)
  = -\mathbb{E}[\log Z]
  \;\ge\; -\log(1)
  = 0.
$$

This completes the proof.


## Intuition

KL Divergence can be interpreted as the **information loss** when $Q$ is used to approximate $P$. In other words, it measures how different $Q$ is from $P$.

* A smaller value means $Q$ is a good approximation of $P$
* A larger value means $Q$ is far from $P$

## Example Use Case

Suppose $P$ is the distribution of real data, and $Q$ is the distribution given by a model. KL Divergence tells us how well the model captures the true data distribution. It is often used in training probabilistic models, such as in variational inference.

---
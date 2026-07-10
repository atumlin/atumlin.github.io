---
layout: page
title: Fairness Verification of Neural Networks
description: FairNNV — certifying individual and counterfactual fairness of neural networks with reachability analysis, quantified by a Verified Fairness score and evaluated across bias-mitigation techniques.
img:
importance: 2
category: research
related_publications: true
---

As machine learning models are increasingly used in socially critical financial decisions — credit scoring, loan approval, fraud detection — providing *formal* guarantees of fairness matters as much as guaranteeing accuracy. **FairNNV** brings fairness into formal verification: it certifies fairness properties of neural networks using reachability analysis, built on the [Neural Network Verification (NNV)](https://github.com/verivital/nnv) framework. This work was published at **ICAIF '24** {% cite 10.1145/3677052.3698677 %}, where I led the design and development of the tool and gave the oral presentation.

### The approach

FairNNV extends NNV's reachability machinery to reason about two fairness notions directly:

- **Individual fairness** — similar individuals should receive similar outcomes.
- **Counterfactual fairness** — an individual's prediction should be unchanged when a protected attribute is counterfactually altered.

Rather than estimating fairness empirically from a test set, FairNNV constructs the reachable output set over the relevant input variations and checks the fairness property against it, yielding a formal certificate. To make the result interpretable and comparable across models, it introduces the **Verified Fairness (VF) score**, a quantitative measure of certified fairness.

### Bias mitigation, put to the test

A central question in the paper is whether popular bias-mitigation methods actually deliver the fairness they appear to. FairNNV compares models **before and after adversarial debiasing** and measures both the empirical fairness improvement and the verified fairness score. Across benchmark datasets — **Adult Census, German Credit, and Bank Marketing**, with a focused analysis on Adult Census classifiers — the results reveal a gap: empirical fairness gains from adversarial debiasing do not always align with formally verified fairness. This argues for integrating formal verification into the model-evaluation pipeline to guide model selection, rather than relying on empirical fairness metrics alone.

### Continuing work

FairNNV grounds my ongoing contributions of fairness specifications to the NNV tool, and the fairness-verification perspective it introduces is the basis for guest lectures I've given on fairness in machine learning at Vanderbilt.

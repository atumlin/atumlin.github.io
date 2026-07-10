---
layout: page
title: Formal Verification of Graph Neural Networks
description: GNNV — reachability-based formal verification of graph neural networks with node and edge features, delivering provable robustness guarantees for power-system surrogates and graph-classification models.
img:
importance: 1
category: research
github: https://github.com/atumlin/gnnv-saiv26
related_publications: true
---

Graph neural networks (GNNs) are increasingly used as fast, topology-aware surrogates in electric power systems — for power flow (PF) analysis, optimal power flow (OPF) estimation, and cascading failure analysis (CFA). Because these models inform safety-critical decisions, their predictions need formal guarantees. **GNNV** is the first reachability-based framework for formally verifying GNNs with *both* node and edge features. It is released as a new module of the [Neural Network Verification (NNV)](https://github.com/verivital/nnv) tool, and this work was accepted to **SAIV 2026** {% cite tumlin2026gnnedge %}.

### The idea: GraphStar sets

Classical neural network verification propagates a **Star set** — an affine image of a bounded polytope — through a network to soundly over-approximate all reachable outputs. GNNs break this abstraction: perturbations propagate through message passing, coupling computations across neighboring nodes and, for edge-aware architectures, across node and edge feature spaces at once.

GNNV introduces **GraphStar sets**, a generalization of Star sets that maintains the matrix structure of node- and edge-feature tensors so graph operations (neighbor aggregation, source gathering, target scattering) apply directly to the center and generator matrices. A `NodeGraphStar` captures uncertainty over the node-feature matrix and an `EdgeGraphStar` over the edge-feature matrix; together they represent joint node–edge uncertainty.

### What it supports

- **GCN and GINE layers.** Affine message-passing operations are propagated exactly; ReLU nonlinearities are soundly over-approximated with the approx-star relaxation. GINE integrates edge features into each message-passing step — to my knowledge, GNNV is the first tool to formally verify GINE-based architectures.
- **Sound reachability.** A soundness theorem (with separate proofs for GCN and GINE) guarantees the computed reachable set over-approximates all outputs under bounded node and edge perturbations.
- **Subgraph verification.** Exploiting the locality of message passing, node-level queries are restricted to a target node's $K$-hop neighborhood, sharply reducing the number of ReLU units and keeping verification tractable on large grids.
- **Formal safety specifications** for voltage-magnitude safety in node regression and local robustness in graph classification.

### Evaluation

GNNV is evaluated on three power-system tasks (PF, OPF, CFA) across the **IEEE-24, IEEE-39, and IEEE-118** networks, plus two standard graph-classification benchmarks (**ENZYMES, PROTEINS**). Highlights:

- GINE models achieve consistently high verification rates under both node-only and joint node–edge perturbations, with edge-feature uncertainty adding minimal cost — the **first edge-aware robustness guarantees** for GINE-based PF and OPF models.
- Against CORA (the only other reachability-based GNN verifier), GraphStar sets produce **tighter enclosures**, verifying up to 21.6% more graphs and maintaining verification at perturbation levels where CORA fails.
- Subgraph verification scales across all system sizes, with most cases completing in under a second and larger systems within tens of seconds.

Code and trained models for reproducing all experiments are available on [GitHub](https://github.com/atumlin/gnnv-saiv26).

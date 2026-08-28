# CAMFT: Conflict-Aware Mergeable Fine-Tuning for Large Language Models

<p align="center">
  Jingang Zhou &nbsp;·&nbsp; Haiyang Guo &nbsp;·&nbsp; Yuan Ma &nbsp;·&nbsp; Han Zhu &nbsp;·&nbsp; Xu-Yao Zhang
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Findings%20of%20EMNLP-2026-4C8BF5" alt="Findings of EMNLP 2026">
</p>

<p align="center">
  <a href="#overview">Overview</a> ·
  <a href="#main-results">Main Results</a> ·
  <a href="#release-status">Release Status</a> ·
  <a href="#citation">Citation</a>
</p>

> **Accepted to Findings of the Association for Computational Linguistics: EMNLP 2026.**

> CAMFT makes mergeability a property shaped during fine-tuning, rather than only a problem repaired after fine-tuning.

This repository will host the official implementation and reproducibility artifacts for **CAMFT: Conflict-Aware Mergeable Fine-Tuning for Large Language Models**. The training and evaluation code is currently being prepared for public release.

## Overview

Most model-merging methods attempt to resolve conflicts after independently fine-tuned task experts have already diverged. CAMFT acts earlier by controlling **where** each task is allowed to update the base model.

CAMFT consists of four stages:

1. **Shared SVD coordinates:** construct a frozen spectral coordinate system from the pretrained weights.
2. **Gradient probing:** estimate coordinate importance and cross-task directional conflict using small probing sets.
3. **Conflict-aware allocation:** assign sparse trainable coordinates according to task importance, specificity, and conflict.
4. **Fine-tune and merge:** train task experts independently and combine their updates using standard model-merging algorithms.

<p align="center">
  <img src="assets/camft_overview.png" width="100%" alt="Overview of CAMFT">
</p>

## Highlights

- **Conflict prevention before merging:** CAMFT uses cross-task conflict as a training-time signal instead of relying only on post-hoc repair.
- **Coordinate-level allocation:** task updates are learned in a shared SVD basis with sparse, conflict-aware masks.
- **Merger-agnostic updates:** among Full FT, MergOPT, and CAMFT, CAMFT achieves the highest merged average with Average, Task Arithmetic, DARE, and TIES.
- **Parameter-efficient adaptation:** CAMFT trains 34.4M parameters per task on Llama-3.2-1B at a coordinate ratio of $\rho=0.10$.

## Main Results

Results on the seven-task TRACE benchmark with Llama-3.2-1B and TIES merging:

| Method | Trainable parameters per task | Single-task average | Merged average | Mergeability |
|:--|--:|--:|--:|--:|
| Full FT | Full | 0.569 ± 0.002 | 0.418 ± 0.006 | 73.5% |
| MergOPT | Full | 0.555 ± 0.008 | 0.442 ± 0.002 | 79.7% |
| **CAMFT** | **34.4M** | **0.557 ± 0.003** | **0.464 ± 0.002** | **83.3%** |

Values are macro-averages over three random seeds. CAMFT achieves the strongest merged performance and mergeability while retaining competitive single-task performance.

## Release Status

- [x] Accepted to Findings of EMNLP 2026
- [x] Method overview and main results
- [ ] Paper link and official BibTeX
- [ ] Training and evaluation code
- [ ] Experiment configurations
- [ ] Per-seed results and plotting scripts
- [ ] Reproduction instructions
- [ ] Task adapters and conflict-aware masks

## Citation

The official BibTeX entry and paper link will be added when the paper becomes publicly available.

## License

The source-code license will be announced with the code release. Model weights and datasets remain subject to their respective upstream licenses.

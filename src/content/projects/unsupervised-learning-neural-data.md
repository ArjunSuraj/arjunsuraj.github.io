---
title: "Unsupervised Learning on Neural Data"
description: "Fitting Hidden Markov Models and Winner-Take-All neural clustering to retinal population recordings — unsupervised analysis without stimulus labels."
tags: ["Python", "Jupyter", "Machine Learning", "Neuroscience", "Data Science"]
github: "https://github.com/ArjunSuraj/UnsupervisedLearningNeuralData"
order: 6
---

## Overview

A research project fitting unsupervised models to neural population recordings from the retina. The goal: discover structure in how neurons fire together, without using any information about the visual stimuli that drove those responses.

## Research Context

Collaboration contributing to computational neuroscience methods, building on two published models:

1. **TreeHMM** (Prentice et al., 2016) — captures temporal (HMM) and spatial (tree) correlations in neural firing patterns
2. **Winner-Take-All clustering** (Loback & Berry, 2018) — biologically plausible neural clustering algorithm

## Datasets

The models were fitted to three types of neural data:

1. **Retinal recordings** from Prentice et al. (2016) — responses to natural movie stimuli
2. **Large-scale retinal data** from Tkačik et al. (2014) — 297 repeats of a 19s movie across ~120 neurons
3. **Synthetic data** — parametrically controlled spatial correlations (alpha = 0 to 1.9) with matched individual firing rates

## Analysis Pipeline

- Fit models across different numbers of latent modes (1 to 146)
- Cross-validated mode selection via test log-likelihood
- Dimensionality reduction (MDS, PCA, LDA) for cluster visualization
- Adjusted Random Index for comparing clustering methods
- Batch processing via SLURM for cluster computing

## Technical Stack

- Python with C++ bindings (Boost.Python)
- Jupyter notebooks for analysis
- Shelve for fitted parameter storage
- Matplotlib for visualization
- SLURM batch processing for compute clusters

## Key Scripts

- `EMBasins_sbatch.py` — main fitting script (TreeHMM / EMBasins)
- `WTAcluster_sbatch.py` — Winner-Take-All model fitting
- `EMBasins_sbatch_plot.py` — post-fitting analysis and visualization
- `data_generation/` — synthetic data generation with controlled correlations

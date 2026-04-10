---
title: "TreeHMM — Neural Data Modeling"
description: "Python bindings for Hidden Markov Models with tree-structured spatial correlations, applied to retinal neural population data."
tags: ["C++", "Python", "Machine Learning", "Neuroscience", "HMM"]
github: "https://github.com/ArjunSuraj/TreeHMM"
order: 5
---

## Overview

Extended the TreeHMM codebase from Prentice et al. (2016) with Python bindings for both HMM and EMBasins models — enabling temporal and spatial correlation analysis in neural population recordings without recompiling C++ code.

## Research Context

This project builds on the paper:

> Prentice, Jason S., et al. 2016. "Error-Robust Modes of the Retinal Population Code." *PLOS Computational Biology* 12 (11): e1005148.

The model identifies recurring patterns (modes) in how populations of neurons fire together, capturing both temporal dynamics (via Hidden Markov Models) and spatial correlations (via tree-structured Ising models).

## Contributions

1. **Python bindings** for both HMM and EMBasins (temporal/no-temporal) — no C++ recompilation needed to switch between models
2. **Modified Matlab bindings** with HMM/TreeBasins switching via preprocessor directive
3. **Additional outputs** — test log-likelihood and other diagnostics exposed through bindings
4. **Numerical stability fixes** — handling NaN/Inf in log-likelihood computations
5. **Code documentation** — comments clarifying implementation details

## Models

- **pyHMM** — Hidden Markov Model capturing temporal correlations between neural firing patterns
- **pyEMBasins** — Temporally independent model for spatial correlation analysis
- **TreeBasin vs IndependentBasin** — Toggle spatial correlations via typedef (requires recompile)

## Technical Stack

- C++ core with Boost.Python bindings
- Matlab MEX interface
- Tested on Debian 9.11 / macOS with Python 2.7
- Compatible with retinal spiking data from [Dryad](https://datadryad.org/stash/dataset/doi:10.5061/dryad.1f1rc)

## Academic Work

Part of my MSc Advanced Computer Science research at the University of Sheffield, contributing to computational neuroscience methods for understanding population coding in the retina.

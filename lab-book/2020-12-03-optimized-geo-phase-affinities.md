---
layout: post
title: Robust speed-optimized composition/affinity determinations for geo-phases
active: lab-book
author: Aaron S. Wolf
date: 2020-12-03
prev:
  post: 2020-11-19-MEXQAL-rapid-geo-benchmark
  title: Least-squares-optimized MEXQAL calculations for geo-phases
next:
motivation: Rapid and robust determination of equilibrium is critical for thermodyanmic simulations. Their ability to usefully predict the evolving state of the system hinges entirely on the speed and trustworthiness of the underlying algorithm responsible for finding the equilibrium states of each phase. Given the large abundance and variety of phases relevant to geological and planetary simulations, this demands a general technique that is sure to rapidly converge to the optimal answer, regardless of the details of the particular phase. This challenge is especially difficult for complex phases involving multi-site substitution, cation ordering, and composition-induced structural changes, all of which frustrate the search for equilibrium as they embed wrinkles and complex-features features in the Gibbs energy surface of the solution phase. This work proposes a generalized solution to this problem, which is guaranteed to converge despite compositional idiosyncrasies common to geological mineral phases (like pyroxenes and spinels).
future-work:
key-points:
  - Local regular solution approximation is derived from calculated chemical potentials and Gibbs curvature at a reference composition; excess mixing parameters are inferred extending accurate extrapolation regime.
---

# Key role of compositional perturbation models
- establish why perturbation models aid convergence
- mention compositional variability in phases needed to cover
- outline existing (linear) baseline models for approximating chemical potentials (linear in composition, or linear in log-transformed composition)
- set metrics for compositional extrapolation accuracy

# Local regular solution approximation overview
<!-- # [[202011300948]] Local regular solution approximation overview -->

While regular solution models [[202011290633]] scan be quite useful, their simplicity limits their applicability to complex ordered phases.
Nevertheless, the ability of the regular solution to capture ideal mixing and roughly represent (in many situations) non-ideal excess interactions makes it attractive for calculations considering local perturbations.
We therefore construct the local regular solution approximation, which relies on evaluating the chemical potentials and Gibbs curvature matrix at a reference state.
Excess solution properties are extracted from this matrix by subtracting off for expected contributions from an ideal solution [[202012010818]].
The chemical potential and Gibbs curvature contributions of the regular solution are fortunately linear in the excess mixing parameters $W_{ij}$, enabling linear least-squares inference of their appropriate values [[*TK*]].
This approach yields a well-behaved perturbation model whose composition-dependence captures the dominant logarithmic and linear terms.
When applied to complex multi-site solution phases, this approximation must be carried out in the augmented dependent-species space (rather than simple independent components) to retain meaningful ideal mixing terms [[*TK*]].

# Classic Regular Solution
- provide expressions for Gibbs energy and derivs
- emphasize computational simplicity of expressions, allowing rapid calcuations

# Inferring local regular solution parameters

# Accuracy benchmark for local regular solution
- Compositional perturbation test for local regular solution vs simple linear model of chemical potential variation

# Accuracy

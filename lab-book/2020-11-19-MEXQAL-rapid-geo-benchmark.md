---
layout: post
title: Least-squares-optimized MEXQAL calculations for geo-phases
active: lab-book
author: Aaron S. Wolf
date: 2020-11-19
prev:
  post: 2020-11-12-MEXQAL-geo-application
  title: Benchmarking MEXQAL method for geologically-relevant phases
next:
key-points:
  - Exchange equilibrium solution can be found approximately by transforming to log-composition space; this yields a set of coupled linear equations, with $\Delta \log X_i$ and $A$ as unknowns, that can be solved using least squares.
---

## Dependent Species & least squares intro


## Linearized least squares affinity solution w/ MEXQAL
<!-- # [[202011061439]] Linearized least squares affinity solution w/ MEXQAL -->

An alternative approximate solution for the coupled composition and affinity of a solution phase can be calculated by linearizing the chemical potential exchange equilibrium condition.
Note that once the curvature matrix has been translated to log-space, all compositional dependence depends only linearly on the log-compostion terms $(logX_i)$.
The approximate metastable equilibrium equation holds simultaneously of each component of the solution phase, providing a system of equations with N constraints:

$$A + \sum_j \frac{\partial \mu_i}{\partial \log X_j} \Delta \log X_j  =  \hat{\mu}_i - \mu_i^\textrm{ref}$$

But there is a single additional unknown, the affinity of the phase A, which itself requires one more constraint.
This constraint is the normalized composition equation (or closure condition), which requires that the sum of all components equals 1.
It is not possible, of course, to perfectly express this in log-space, but it can be represented approximately as:

$$\sum_i X_i^\textrm{ref} \Delta \log X_i = 0$$

where the reference composition vector is given by $X_i^\textrm{ref}$, and we consider logarithmic changes from the reference state, approximately equal to fractional changes as long as they are small.
Since the original reference composition is normalized, these changes must all sum to zero to ensure that the final result is also normalized.
Combined, the two expressions above provide a system of N+1 linear equations constraining the value of N+1 unknowns ($\Delta \log X_i$ and $A$).
They can thus be rapidly solved using any standard linear solver.

The inherent assumption that logarithmic composition adjustments are small will hold true near the end of the convergence iteration loop, but may not at the beginning, depending on the quality of the initial guess.


## Re-mapping chemical potentials & Gibbs curvature to dependent species
<!-- [[202011131534]] Mapping chempot & Gibbs curvature to dependent species -->

Transformation to dependent species space raises additional mathematical challenges associated with deriving properties of the dependent species from those of the endmember components.
This transformation rests directly on the species stoichiometry matrix:
$$\tilde{\nu}_{ij} = \partial n_j / \partial \tilde{n}_i$$
which describes how the number of moles of the $j^\textrm{th}$ endmember component ($n_j$) changes in response to changes in the amount of the $i^\textrm{th}$ species ($\tilde{n}_i$).
The chemical potentials of the species are then given simply by the stoichiometrically-weigthed average of the endmember chemical potentials:

$$
\tilde{\mu}_i = \sum_j \tilde{\nu}_{ij} \mu_j
$$

Likewise, we must also find a transformation for the Gibbs curvature matrix, which describes the linear dependence of chemical potentials on changes in molar composition, but it does so in endmember component space.
When solving problems in the larger degenerate compositional space of dependent species, we must mathematically inflate this matrix to describe how the chemical potentials of these species change as their quantity is altered.

$$
\frac{\partial \tilde{\mu}_i}{\partial \tilde{n}_l} = \sum_k \sum_j \tilde{\nu}_{ij} \frac{\partial \tilde{\mu}_j}{\partial \tilde{n}_k} \tilde{\nu}^T_{kl}\\
\frac{\partial \tilde{\mu}}{\partial \tilde{n}} = \tilde{\nu}  \cdot \frac{\partial \tilde{\mu}}{\partial \tilde{n}} \cdot \tilde{\nu}^T
$$

where $\nu^T$ is the transpose of the stoichiometry matrix (oriented with species as columns rather than rows).
This transformation is derived by applying the stoichiometry matrix once to calculate the linear dependence of species on the molar endmember composition, and then a second time to calculate their dependence on the molar abundance of the species themselves.
Since the stoichiometry matrix is unchanging and fixed by the composition of each species, this new Gibbs curvature matrix for dependent species retains all the linearity of the original in endmember component space, thereby allowing an identical least squares approach to solve for dependent species abundances.

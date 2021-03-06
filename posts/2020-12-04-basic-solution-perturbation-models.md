---
layout: post
title: Basic composition-perturbation models for solution phases
active: lab-book
author: Aaron S. Wolf
date: 2020-12-04
prev:
  post: 2020-11-19-MEXQAL-rapid-geo-benchmark
  title: Least-squares-optimized MEXQAL calculations for geo-phases
next:
  post: 2020-12-11-equilibrium-paper-outlines
  title: 'Urgently seeking equilibrium: Manuscript outlines for equilibrium algorithms'
motivation: |
  Rapid and robust determination of equilibrium is critical for thermodynamic simulations. Predicting the evolving state of the system hinges entirely on the speed and trustworthiness of the underlying algorithms responsible for finding the equilibrium states of each phase. Given the large abundance and variety of phases relevant to geological and planetary simulations, this demands a general technique that is sure to rapidly converge to the optimal answer, regardless of the details of the particular phase.
  In this post, I focus on describing the foundations of the two simplest local approximations available for solution mixing models. The ideal and linear solution approximations form the foundation of the local regular solution approximation, to be presented in next week's post.
future-work: Most of what I prepared for this post had to be removed due to a missing term in my derivation of the regular solution model. In next week's post, we will thus explore the mathematical and performance details of the local regular solution approximation.
key-points:
  - Ideal solution model assumes non-interacting components in the mixture, leading to a weighted average Gibbs energy modified only by the entropy of mixing.
  - Linear solution model provides a basic linear description for solution phases which has greater accuracy for small compositional perturbations, but lacks any awareness of entropic mixing.
  - The best aspects of each of these models can be combined to form the local regular solution approximation, which builds a complete regular solution based on phase properties evaluated at the reference composition, allowing greater extrapolation in composition space.
---

<!-- # Key points -->
  <!-- - Local regular solution approximation is derived from calculated chemical potentials and Gibbs curvature at a reference composition; excess mixing parameters are inferred extending accurate extrapolation regime. -->
  <!-- - Gibbs curvature for ideal solutions has large positive composition-dependent values on the diagonal and small fixed negative values off it, reflecting how increasing any component fractionally dilutes all others. -->
  <!-- - The regular solution model is the simplest extension of the ideal solution model, accounting for non-negligible mixing energy; its quadratic compositional form leads to linearly-dependent chemical potential terms. -->
  <!-- - Local regular solution is determined using least squares by constructing a linear constraint matrix that encodes the linear dependence of excess Gibbs curvature values $(d \mu_i/d n_j)^{xs}$ on the $W_{ij}$ parameters. -->

<!-- # Justify motivation for efficient & robust equilibrium algorithms -->
<!-- Rapid and robust determination of equilibrium is critical for thermodynamic simulations. Their ability to usefully predict the evolving state of the system hinges entirely on the speed and trustworthiness of the underlying algorithm responsible for finding the equilibrium states of each phase. Given the large abundance and variety of phases relevant to geological and planetary simulations, this demands a general technique that is sure to rapidly converge to the optimal answer, regardless of the details of the particular phase. This challenge is especially difficult for complex phases involving multi-site substitution, cation ordering, and composition-induced structural changes, all of which frustrate the search for equilibrium as they embed wrinkles and complex features in the Gibbs energy surface of the solution phase. This work proposes a generalized solution to this problem, which is guaranteed to converge despite compositional idiosyncrasies common to geological mineral phases (like pyroxenes and spinels). Most of what I prepared for this post had to be removed due to a missing term in my derivation of the regular solution model. This will be fixed and addressed in next week's post. -->

## Computational role of compositional-perturbation models

Chemical thermodynamic simulations, especially those involving compositional evolution or model calibration require many repeated calculations of the chemical potentials for each phase, typically dominating simulation computing time.
Despite generally modest adjustments in composition from one iteration to the next, the computational burden for each of these calculations is fully realized in every function call, dramatically and unnecessarily increasing overall computing times.
<!-- Discussion of limited compositional variability in natural systems might be helpful here. -->
We are thus highly motivated to seek out simple local approximations that can achieve dramatically faster runtimes while retaining accuracy over reasonable ranges in composition.
In this section, we quantify the accuracy of the ideal and linear solution models, which represent the baseline computational models of chemical thermodyanmics.
We also outline the basic framework for a potentially more accurate model, the local regular solution approximation, discussed in detail in the next section.

## Ideal and Linear Solution Models

The simplest local approximations for chemical solutions are the physically-motivated ideal solution and the purely mathematical linear solution models.
Because the ideal solution is based on the assumption of ideal mixing, it completely ignores any chemical interaction energies and thus generally performs rather poorly for most real-world solutions.
In stark contrast, the linear solution model is a purely mathematical representation that has no physical basis, but shows much improved performance as it empirically accounts for (linear) compositional variation in the chemical potentials.
Together, these two rather basic yet important models provide the foundation for a much more accurate approximation, the local regular solution, which we will later explore in detail.
<!-- # [[202012010818]] Ideal Solution model intro -->

The ideal solution model represents a thermodynamic baseline (or null hypothesis) for mixed phases; though it is rarely used directly, it forms the foundation of nearly all more complicated models.
The fundamental assumption underlying the ideal solution is that the components of the solution behave as energetically independent entities.
The resulting mixture thus has an energy given by the weighted average of the components, modified only by the additional entropy of mixing, yielding the simple molar Gibbs energy expression:

$$
\bar{G}^{ideal} = \sum_i X_i \mu_i^0 + RTm\sum_i X_i \log X_i
$$

where $\mu_i^0$ are the chemical potentials for each pure endmember component, $X_i$ is the mol-fraction of each component, $RT$ is the thermal energy scale, and $m$ is the site multiplicity.
The chemical potentials are given by the compositional derivative:

$$
\mu_k = \mu_k^0 + RTm \ln X_k
$$

which emphasizes how the chemical potential of the pure endmember component is only modified by ideal entropy mixing.
Based on this form, the ideal solution can be transformed into a local perturbation model:

$$
\Delta \mu_k^{ideal} = \mu_k-\mu_k^{ref} \approx RTm \cdot \ln \left(X_k / X_k^{ref}\right)
$$

where changes in the chemical potentials are attributed entirely to the expected behavior for the entropy of mixing terms.

Conceptually much simpler is the linear solution model, which is simply a first-order Taylor expansion of the chemical potentials with respect the the molar composition of the phase.
Unlike the ideal solution, the linear solution thus requires that both the chemical potentials and their compositional derivatives (the Gibbs curvature matrix) be calculated at the reference composition:

$$
\Delta \mu_k^{linear} = \mu_k-\mu_k^{ref} \approx \sum_l \frac{d \mu_k}{d n_l} \cdot (X_l - X_l^{ref})
$$

where changes in the chemical potentials are assumed to have linear dependence, regardless of the magnitude of the compositional extrapolation.
For small perturbations, this assumption is perfectly reasonable, and the linear solution model thus greatly outperforms the ideal solution in this regime.
But the lack of logarithmic mixing terms comes to dominate for larger extrapolations, urging us to seek a more accurate model that can capture both empirically observed chemical potential variations and the appropriate form for entropic mixing.




<!-- # Compositional Extrapolation Benchmark (linear solution)
- compare local ideal solution and local linear solution -->

## Local regular solution approximation overview
<!-- # [[202011300948]] Local regular solution approximation overview -->

Regular solution models represent the next step in improving accuracy for chemical mixing models, and while they can be quite useful, their simplicity limits their applicability to complex ordered phases.
Nevertheless, the ability of the regular solution to capture ideal mixing and roughly represent (in many situations) non-ideal excess interactions makes it attractive for calculations considering local perturbations.
We therefore construct the local regular solution approximation, which relies on evaluating the chemical potentials and Gibbs curvature matrix at a reference state.
Excess solution properties are extracted from this matrix by subtracting off for expected contributions from an ideal solution.
The chemical potential and Gibbs curvature contributions of the regular solution are fortunately linear in the excess mixing parameters $W_{ij}$, enabling linear least-squares inference of their appropriate values.
This approach yields a well-behaved perturbation model whose composition-dependence captures the dominant logarithmic and linear terms.
When applied to complex multi-site solution phases, this approximation must be carried out in the augmented dependent-species space (rather than simple independent components) to retain meaningful ideal mixing terms.


<!-- # Gibbs Curvature for Ideal Solution -->
<!-- # [[202012010810]] Gibbs Curvature for Ideal Solution -->

<!-- The Gibbs curvature matrix for an ideal solution is:
$$
\left(\frac{d \mu_i}{d n_j}\right)^{ideal}  = \frac{RTm} {X_i} (\delta_{ij} - X_i)
$$
where $\delta_{ij}$ is the kronecker delta, reflecting the diagonal stucture of the matrix.
For diagonal elements, the expression simplifies to:
$$
\left(\frac{d \mu_i}{d n_i}\right)^{ideal}  = \frac{RTm} {X_i} (1 - X_i), \;\;\; \textrm{for diagonal elements}
$$
which is generally large and positive, and modified by the reference composition, while off-diagonal elements have the fixed value of:
$$
\left(\frac{d \mu_i}{d n_j}\right)^{ideal}  = -RTm, \;\;\; \textrm{for} \;\;\; i \ne j
$$
which is negative, reflecting the closure condition for normalized fractional compositions (i.e. increasing a single component fractionally dilutes all other components).
This diagonal structure arises directly from the molar derivative of fractional composition ($d X_i/ dn_j$) [[*TK*]]. -->

<!-- # Classic Regular Solution
# [[202011290633]] Regular Solution Model Intro

On of the simplest non-ideal solution models is the regular solution, which supplements ideal entropic mixing contributions [[202012010818]] with a non-ideal quadratic excess $\bar{G}^{xs}$:
$$
\bar{G} = \bar{G}^{ideal} + \bar{G}^{xs}\\
\bar{G}^{xs} = \frac12 \sum_i \sum_j W_{ij} X_i X_j
$$
where $W_{ij}$ is the symmetric energy of mixing parameter, and $X_i$ is the fractional composition of the solution.
In some applications, this excess is allowed to vary with temperature and pressure and is thus represented as:
$$
W^G = W^H - W^ST  + W^V P
$$
breaking it down into excess enthalpy ($W^H$), entropy ($W^S$), and volume ($W^V$) contributions.
The chemical potentials for this model are derived from the compositional derivative of the Gibbs energy, yielding:
$$
\mu_k = \mu_k^{ideal} + \mu_k^{xs}\\
\mu_k^{xs} = \sum_i X_i W_{ik}
$$
where the quadratic form of the excess introduces a simple linear composition-dependent term to the chemical potentials (higher order derivatives are also computationally useful [[202011290649]]).
This symmetric non-ideal model is simple but often quite powerful in describing solution thermodynamics, especially in cases with limited data where even a highly approximate model is useful.


# Inferring local regular solution params by least-squares
# [[202012030549]] Inferring local regular solution params by least-squares

A local regular solution [[202011300948]] provides a valuable approximation tool for computational applications.
Training its parameter values is both easy and computationally efficient using standard least-squares inference.
The first step is simply to calculate the excess Gibbs curvature matrix for the reference composition ($X_k$):
$$
\left(\frac{d \mu_i}{d n_j}\right)^{xs} \equiv \frac{d \mu_i}{d n_j} - \left(\frac{d \mu_i}{d n_j}\right)^{ideal}
$$
where $d \mu_i/d n_j$ and $(d \mu_i/d n_j)^{ideal}$ are the local Gibbs curvature and its ideal contribution [[202012010810]].
This curvature excess is linearly related to the unknown regular solution parameters ($W_{ij}$):
$$
\left(\frac{d \mu_i}{d n_j}\right)^{xs} = (W_{ij} + W_{ji})/2 - \sum_k X_k (W_{ik}+W_{ki})/2
$$
where this expression has been modified from its standard form to enforce the required symmetry of the quadratic energy excess properties of the regular solution.

![**Constraint matrix for local regular solution parameters $W_{ij}$.** Excess energy parameters are determined by least-squares using the constraint (or design) matrix visualized here. Weighting coefficients range from -1 (dark blue) to 0 (white) to +1 (dark red).](images/202012030654-local-reg-soln-constr-matrix.png){#fig:Wij-constr width=50%}

The unknown energy excess parameters can now be determined using least-squares methods by unraveling the constraint and unknown parameter matrices to fit the standard least-squares form ($A x = b$).
The result is a block diagonal constraint (or design) matrix (visualized in the figure) which imposes the direct dependence of each curvature value on its corresponding W parameter (dark red values on main diagonal and in tilted lattice), modified by weighted compositional adjustments (light blue values just off main diagonal and in stripes).
Combining this matrix with the list of excess curvature values determined above, enables direct inference of the unknown parameter values by least squares, which is trivially fast for geological applications and guaranteed to yield a result accurate to within machine precision. -->

<!-- # Accuracy benchmark for local regular solution
- Compositional perturbation test for local regular solution vs simple linear model of chemical potential variation
- monte carlo variation in fractional composition (log changes in mol values)
- evaluate chemical potentials for local regular soln and linear approx models and true variation
- plot growing approximation errors with increasing compositional extrapolation
  - quantify improved accuracy
- carry out for geologically relevant compositions
  - explore dependence on dependent species -->

---
layout:  default
title: Buckingham Potential
date:   2015-05-28 
active: notes
categories: [notes]
tags: [md,potentials,atom-sim]
---

The Buckingham potential is a common choice, capable of representing a wide variety of materials:
<div>$$
     \phi_{ij}(r_{ij}) =  A_{ij}\exp\left[-\frac{r_{ij}}{\rho_{ij}}\right] - \frac{C_{ij}}{r_{ij}^6}
     \label{eq:stdbuck}
$$</div>
where `$A_{ij}$` and `$\rho_{ij}$` define the short-range repulsive interaction and `$C_ij$` describes the long-range Van der Waals interaction between atoms i and j.
This is the common form found in most textbooks and simulation codes (including LAMMPS).

## Modified Buckingham-well Potential
To make physical sense of this expression, we can define a modified Buckingham-well potential which is cast in terms of physically intuitive parameters:
<div>$$
     \phi_{ij}(r_{ij}) =  
    \frac{E^0_{ij}}{1-\sigma_{ij}} \left\{ \sigma_{ij}\exp\left[-\frac{6}{\sigma_{ij}} \left(r_{ij}/r^0_{ij}-1\right)\right] - \left[\frac{r_{ij}}{r^0_{ij}} \right]^{-6} \right\} \\
  \label{eq:buckwell}
$$</div>
where `$r^0_{ij}$`, `$E^0_{ij}$`, and `$\sigma_{ij}$` are the position, depth, and relative width of the potential energy well between atoms of type `$i$` and `$j$`.
The relative width parameter is bounded to the range `$0 < \sigma_{ij} < 1$`, tending toward intermediate values of `$\sigma_{ij} \sim 1/2$`.
This form of the potential can be directly related to the standard Buckingham potential form 
<div>$$
     A_{ij} = E^0_{ij}\frac{\sigma_{ij}}{(1-\sigma_{ij})} \exp\left[\frac{6}{\sigma_{ij}}\right] \;,\;\;
    \rho_{ij} = r^0_{ij} \frac{\sigma_{ij}}{6} \;,\;\;
    C_{ij} = \frac{E^0_{ij}{r^0_{ij}}^{\,6} }{(1-\sigma_{ij})}
$$</div>
Though the standard form (see Eq. \ref{eq:stdbuck} above) is slightly more compact, its parameters cannot be directly interpreted as in the modified form.
*(It should be noted that this transformation is trancendental, and thus we must determine the equivalent modified parameter values iteratively given the standard buckingham parameters.)*


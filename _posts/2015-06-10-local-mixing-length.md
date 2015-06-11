---
layout:  default
title: Local Conductive Mixing Length
date:   2015-06-10 
active: notes
categories: [notes,magma-ocean]
tags: [geodyn,magma-ocean]
---
##Standard Approach
As discussed in the general notes on [Mixing Length Theory](mixing-length.html), the complex theory of convection can be reasonably well approximated within a simple 1D theory by casting convection as an equivalent 1D conductive problem.
The key to this approach is to define a mixing length `$l$`, which is the typical length-scale of the system.
**The mixing length thus represents both the average size of convective parcels and the average distance each parcel travels before dissipating.**
It has been empirically determined (need citation) that assuming the mixing length corresponds to the distance to the nearest boundary is a reasonable approximation, yielding thermal profiles that agree with 3D convective simulations.
We can make sense of this standard model assumption:
<div>$$
l_{\rm std} = {\rm min}(R_{\rm max}-r, r-R_{\rm min})
$$</div>
by recognizing that at any given time, equal numbers of convective parcels are going up as going down.
Thus the convective parcels will continue rising or falling until they "hit" the thermal boundary layers at the top and bottom.
Due to the symmetry of the problem, we expect that rising and falling parcels travel a similar distance/are of similar size, and thus the distance to the nearest boundary must be reasonably close to the typical length scale of the convective parcels.
Using this standard formulation, we obtain effective convective diffusivities for viscous systems that scale like:
<div>$$
\kappa_{\rm conv} \propto \frac{l^4}{\nu}
$$</div>
Since convection is a more efficient heat transport mechanism than conduction alone, `$\kappa_{\rm conv} > \kappa$` throughout the bulk of the convecting system.
From this scaling expression, it is clear that the two major ways to reduce the efficiency of convection (and thus develop the high thermal gradients associated with boundary layers is to have very small mixing-lengths, as occurs at the system boundaries, or to dramatically increase the viscosity.

##Boundary Layer Length Scale
The behavior within the boundary layer is distinct from the rest of the system.
Within the boundary layers, the material is completely within the conductive regime, as it is incapable of generating the buoyant instabilities (which grow into convective parcels) so close to the system boundaries.
This is typically thought of using local Rayleigh numbers to determine the minimum length scale of the boundary layer needed to attain super-critical Rayleigh numbers that signify convection.

**Give derivation of T.B.L. length-scale derivation here**

## Mixing length within boundary layers
In many cases, the standard mixing length formulation is perfectly sufficient to describe convecting systems/ we must be careful, however whenever we are particularly concerned about the development of new boundary layers  within the systems interior.
Once a thermal boundary layer has developed, the standard method would dictate that the system should suddenly break into two subsystems separated by a thermal boundary layer.
It is unclear, however, how this might be naturally simulated without first prescribing the location and time of the boundary layer appearance... clearly not an ideal situation.
Instead, we seek an alternative approach that provides the same behavior for simple systems, but that can still generalize to the spontaneous development of internal boundary layers.

**Incomplete section, giving only equations**
Condition for the edge of a TBL:
<div>$$
\kappa_{\rm conv} = \kappa
$$</div>
By rearranging the expression for the convective diffusivity of a viscous system, we find that:
<div>$$
l = (18)^{1/4} \left[\frac{\nu}{\alpha |g| \Delta (\delta_z T)_S} \right]^{1/4}
$$</div>
As shown above, this is consistent with the critical Rayleigh number argument, having the identical functional dependence on material properties, and differing only in the proportionality constant.

Thus we have altered the expression for the convective diffusivity, to accurately reflect the transition from conductive to convective behavior:
<div>$$
\kappa_{\rm conv} = {\rm max}\left\{\kappa_h, \kappa\right\}
$$</div>

and
<div>$$
  J_q = +\rho C_p \kappa \left.\frac{\partial T}{\partial z}\right|_S + \rho C_p \kappa_{\rm conv}\Delta (\delta_z T)_S
$$</div>

**Condition for a TBL**
<div>$$
\begin{array}{ll}
\Delta (\delta_z T)_S &> 0 \\
\kappa_{\rm conv} &= \kappa
\end{array}
$$</div>
Thus we can now extend the definition of the mixing length to include distance to the core of *ANY* TBL, be it at the margins OR at the center of the system.

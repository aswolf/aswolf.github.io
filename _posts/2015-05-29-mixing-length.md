---
layout:  default
title: Mixing Length Theory
date:   2015-05-28 
active: notes
categories: [notes,magma-ocean]
tags: [geodyn,magma-ocean]
---

1-D thermal evolution can be effectively modeled using mixing length theory to approximate the radially averaged results of full 3-D convective simulations.
The physical picture is that convective heat transport at a distance $l$ from the nearest boundary is dominated by fluid parcels of size $l$, which transport heat vertically over a distance equal to their size before the dissipate, spanning the current position (from $r-l/2$ below to $r+l/2$).
The sensible heat flux is expressed as a sum of conductive and convective terms:
<div>$$
  J_q = +\rho C_p \kappa \frac{\partial T}{\partial z} + \rho C_p \kappa_{\rm conv}\Delta (\delta_z T)_S
$$</div>
where $z=R-r$ is the depth below the surface, $\kappa$ is the thermal diffusivity, $\kappa_{\rm conv}$ is the effective convective diffusivity, and the thermal gradient relative to the adiabat is given by:
<div>$$
\label{eqn:thermgrad}
\Delta (\delta_z T)_S = \frac{\partial T}{\partial z} - \left(\frac{\partial T}{\partial z} \right)_S= -\Delta (\delta_r T)_S = -\frac{\partial T}{\partial r} + \left(\frac{\partial T}{\partial r} \right)_S
$$</div>
Similarly:
<div>$$
\Delta (\delta_{zz} T)_S = \frac{\partial^2 T}{\partial z^2} - \left(\frac{\partial^2 T}{\partial z^2}\right)_S = \Delta (\delta_{rr} T)_S = \frac{\partial^2 T}{\partial r^2} - \left(\frac{\partial^2 T}{\partial r^2}\right)_S
$$</div>
(Note that the -1 terms from `$\partial z = -\partial r$` cancel in the case of the second derivative such that the curvature of the surfaces is actually the same.)
The effective convective diffusivity is expressed in a form identical to Fourier's law (formerly called the eddy diffusivity according to Abe 1993), is determined from the mean free path by `$\kappa \sim v l$`:
<div>$$
\kappa_h = \left\{
\begin{array}{ll}
0 &  \Delta(\delta_z T)_S \leq 0 \\ 
v_{\rm vis}l & 0 < {Re}_{\rm loc} < 9/8 \\
v_{\rm invis}l & 9/8 \leq {Re}_{\rm loc} 
\end{array} 
\right.
$$</div>
where stable stratification prevents convection when the temperature gradient is not as steep as the adiabat ($\Delta(\delta_z T)_S \leq 0$), and otherwise the local Reynolds number `$Re_{\rm loc} = {v_{\rm vis} l} \big/ {  \nu}$` determines the importance of viscosity to the resulting convection.
The convective velocities are given by a balance of the buoyancy force on each fluid parcel against the viscous drag or pressure drag forces, in the viscous and inviscid cases, respectively:
<div>$$
  v_{\rm vis} = \frac{\alpha |g| l^3}{18\nu}  \Delta(\delta_z T)_S \\
$$</div>
<div>$$
  v_{\rm invis} = \sqrt{\frac{\alpha |g| l^2}{16}  \Delta(\delta_z T)_S} \\
$$</div>
For viscous convection, the parcel velocity is given by Stokes settling for a sphere of diameter $l$. The inviscid case can be determined up to a constant by equating the dynamic pressure force $\sim$$\rho v^2$ with the buoyancy force (though the exact source of the proportionality constant is unknown).

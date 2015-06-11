---
layout:  default
title: Mie-Grüneisen Equation of State
date:   2015-05-29 
active: notes
categories: [notes]
tags: [eos]
---

In order to represent the complete equation of state of a material, we must be able to model its properties (density, bulk modulus, heat capacity, thermal expansion, etc.) as a function of *both* pressure and temperature.
The Mie-Grüneisen equation of state provides a simple and useful solution to this problem, by given a function for the thermal pressure contribution in term of the thermal energy:
<div>$$
\Delta P_{\rm therm}(V,T) = \frac{\gamma(V)}{V} \Delta E_{\rm therm}(V,T)
\label{eq:mie-grun-eos}
$$</div>
where `$\Delta P_{\rm therm} = P(V,T) - P(V,T_0)$`and `$\Delta E_{\rm therm} = E(V,T) - E(V,T_0)$` are the thermal pressure and energy contributions, and the Grüneisen parameter `$\gamma = \gamma(V)$` is assumed to be a function only of volume.
This expression is extremely useful due to its simplicity and accuracy for solids, where the temperature-dependence of the Grüneisen parameter is negligible, however it is also often applied very approximately to melts, where the thermal effect on $\gamma$ is sufficiently small over a limited P-T ranges.

##Derivation 
To derive equation \eqref{eq:mie-grun-eos} above, we begin with thermodynamic definition of the Grüneisen parameter:
<div>$$
\gamma = -\left.\frac{\partial \log T}{\partial \log V}\right|_S = - \left.\frac{V}{T}\frac{\partial T}{\partial V}\right|_S
$$</div>
Using a Maxwell relation, we can replace the derivative with `$\partial T \big/ \partial V \big|_S = - \partial P \big/ \partial S \big|_V$`.
Finally, we note from the 1st law of Thermodynamics that for reversible processes `${dE}_V = T {dS}_V$`, where the `$V$` subscript indicates that volume is held constant.
Thus we obtain
<div>$$
\gamma = V \left.\frac{\partial P}{\partial E}\right|_V
$$</div>
We can rearrange this expression and integrate to obtain absolute pressures and energies
<div>$$
\int_{P_0}^{P}{dP}_V = \frac{1}{V}\int_{E_0}^{E}\gamma{dE}_V
\label{eq:mie-grun-integ}
$$</div>
This is an important expression, as thusfar we have made no specialized assumptions about the form of the equation of state, and thus Equation \eqref{eq:mie-grun-integ} is generally applicable to any material.

Now we can make an extremely useful simplifying assumption, which is that the Grüneisen parameter is a function of **only** volume, having no appreciable temperature dependence.
This assumption holds approximately true for most crystalline solids up to reasonably high temperatures (typically up to a decent fraction like `$\sim 1 \big/ 2$` the melting temperature, owing to their quasi-harmonic vibrational properties.
Since these integrations are made along isochoric (constant-volume) pathways, we can move `$\gamma(V)$` outside the integral, yielding
<div>$$
P - P_0 = \frac{\gamma(V)}{V} (E - E_0)
$$</div>
Noting the volume and temperature dependence of the pressure and energy, we arrive at the final form of the Mie-Grüneisen equation of state, given in Equation \eqref{eq:mie-grun-eos}.

## Using the Mie-Grüneisen EOS
At this point we are free to make use of this handy expression by plugging in a model for the internal energy.
Depending on circumstances, we have multiple options available:

* **Debye Model** - This is the most popular and is a reasonable approximation for simple solids
* **Hugoniot** - If the data being modeled are from shock wave experiments, we can use the Rankine-Hugoniot equations to get measured P,V,E values.
* **Power-law Heat Capacity** - This simple form can be used to roughly model melts provided the temperature dependence of `$\gamma$` is small enough over the P-T range of interest 


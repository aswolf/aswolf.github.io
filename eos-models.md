---
layout:  default
title: Eos-Models
active: resources
---

## General Thermodyanmic Properties

### Pressure and Energy
The thermodynamic definition of pressure, relates it to the volume-dependence of the energy. This expression can be rearranged in order to derive an expression for the energy.
\$$ 
P(V)= - \frac{dE}{dV}
\$$
\$$ 
E(V)= E_0 - \int_{V_0}^{V} P(V) dV
\$$

### Bulk Modulus 
The bulk modulus reflects a further volume derivative of the pressure.
\$$ 
K(V)= - V \frac{dP}{dV}
\$$
By rearranging this expression, and approximating differentials with small differences, we can see that the bulk modulus can be seen as a pressure scale
for the material, defining the required pressure change \\( \Delta P \\), needed to induce a large fractional change in the material volume
\$$ 
\frac{\Delta V}{V} \sim - \frac{\Delta P}{K}
\$$

### Bulk Modulus Derivative
\\(K'\\) defines the pressure dependence of the bulk modulus
\$$ 
K'(V)= \frac{dK}{dP}
\$$
For most solid materials, \\(K'\\) remains very roughly constant decreasing slightly with compression, and takes on typical values near 4.

##Vinet Equation of State
The "Universal" equation of state is derived from a direct representation of typical inter-atomic forces. It has been shown to have generally favorable extrapolation behavior to very high pressure. It provides a useful description of either an adiabatic or isothermal reference compression curve.
\$$ 
P(V)=  K_0\cdot 3(1-x)x^{-2} \exp[\eta (1-x)]
\$$
\$$ 
E(V) - E_0= K_0 V_0\cdot (9/\eta^2) \\{ 1+ [\eta(1-x) -1]\exp[\eta (1-x)]\\}
\$$
where
\$$
x = (V/V_0)^{1/3}
\$$
\$$
\eta = 3/2 (K_0' - 1)
\$$

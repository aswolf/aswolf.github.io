---
layout: default
title: Research
active: research
---

My research interests span a broad range of topics including planetary science, geochemistry, geophysics, and statistical analysis.
In particular, the bulk of my work is focused on understanding the chemistry and thermodynamics of the Earth’s lower mantle.
I approach this topic with a variety of techniques, including diamond anvil cell experiments, thermodynamic modeling of first principles calculations, and simplified planetary evolution modeling.
I have also done work on determining the interior properties of extrasolar planets through their orbital evolution, as well as understanding near-shore bathymetry of lakes on Titan through careful statistical analysis of radar images.
You can see a list of my publications [here](publications.html).
Currently, I am working on three projects that I describe below in more detail.

{% include box.html %}

{% include markdown.html %}
###Open Projects found at [github.com/aswolf]()
In support of the goals of Open Science, to make research more accessible and reproducible (i.e. more scientific), I have begun posting many of my projects on my github site.

####I encourage you to take a look and think about what you can do to make your science more open!
{% include divclose.html %}
{% include divclose.html %}

##Modeling Silicate Liquids at Mantle Conditions 
Determining the evolution of the Earth's mantle since formation is a crucial topic to understanding its present state.
This is particularly true given that temperature and composition are often highly degenerate in seismic observations of the mantle.
It has long been thought that the Earth likely went through one or more periods in which the mantle was predominantly or entirely molten.
This magma ocean scenario is a simple consequence of the extremely large energies involved in terrestrial planet accretion.
Recent experimental and theoretical work have shown that the properties of high pressure silicates are rather different from what was previously supposed, implying that crystallization of a magma ocean proceeds from the center outward rather than from the bottom up.
This behavior is a consequence of both the depths of crystallization and neutral crystal buoyancy.
Since these parameters are defined by composition-dependent equilibrium conditions, it is important to develop a simple model of silicate liquids that allows rapid determination of equations of state in a large chemically relevant system.
For this project, I have developed the Coordinated Hard Sphere Mixture (CHaSM), which can rapidly predict the behavior of complex silicate liquids over wide ranges in Temperature, Pressure, and Composition.
I am currently applying this general model to a simplified chemical representation of the Earth's mantle with an eye toward later using it to determine the chemical and thermal evolution of a planetary magma ocean.

##High P-T Diamond Anvil Cell Experiments (Advisor: Jennifer
Iron-bearing magnesium silicate perovskite is thought to be the dominant mineral in the Earth's lower mantle, occupying ~80% by volume.
This makes it one of the most crucial phases to understanding the structure and long-term evolution of the Earth.
In this work, I set out to characterize the composition-dependent compression behavior of perovskite at realistic mantle conditions using laser-heated diamond anvil cell experiments.
Synchrotron X-ray diffraction experiments were carried out at the Advanced Photon Source, measuring the high temperature compression curves for (Mg,Fe)SiO_3 perovskite in a quasi-hydrostatic neon pressure medium for a range of iron compositions.
The resulting powder diffraction profiles are then fit to obtain perovskite volumes as a function of pressure and temperature.
From the extracted volumes, I construct high temperature equations of state for each composition.
These results can be compared to previous experimental studies that used less hydrostatic pressure media and focused on either pure MgSiO3 perovskite or did not explore the thermal effect in iron bearing samples.

##Thermodynamics Model of 1st Principles Calculations
High quality experimental data is ideally the best standard for determining the thermodynamic properties of earth materials, however it is often difficult and costly to perform experiments at the relevant extreme conditions.
Furthermore, experiments provide a relatively sparse sampling of Pressure-Temperature-Composition space, and so theoretical calculations will always be useful in constructing a detailed overall picture of the thermodynamics of complex systems.
In this work with Paul Asimow and Razvan Caracas, we use density functional theory (DFT) to calculate the energies and volumes of iron-bearing silicate perovskite at mantle pressures.
I construct a full thermodynamic model of perovskite at mantle conditions by combining static DFT data together with perturbation calculations that explore the vibrational behavior of the crystal structures.
In particular, we are interested in characterizing the spin state of iron in mantle perovskites, which can have a large observable effect on material properties, and in determining the location and form of the spin transition in perovskites at high temperature.
Eventually, we aim to combine this model with a similar model for ferropericlase, the other major phase in the lower mantle, to obtain a complete thermodynamic model for a simplified lower mantle system.

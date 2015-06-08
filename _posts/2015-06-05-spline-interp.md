---
layout:  default
title: Cubic Spline Interpolation
date:   2015-08-05 
active: notes
categories: [notes,math]
tags: [math,numerics]
---
We all like continuity. 
It turns out, so does our code.

Most numerical methods are susceptible to minor (or major) freak outs whenever discontinuities are present in the data being handled.
This includes jumps not only in the actual value, but also jumps in its derivatives, which appear as kinks or cusps in the function.
For computational simplicity/stability, it is sometimes beneficial to smooth over these jumps or kinks before handing the data over to whatever algorithm we are using.

In order to represent arbitrarily shaped smooth curves, we need functional forms that are flexible and can easily scale to match increasingly complex data.
Polynomial ***splines*** provide us exactly these services, by splitting up the functional domain into many segments and then representing the function as simple cubic (or higher order) polynomials, which are constrained to have continuous values and higher order derivatives at the domain boundaries, called "knots".
Thus, we can create arbitrarily complex functions simply by defining a sufficient number of domains.

Though splines are implemented out of the box in many numerical analysis packages, like scipy (for Python), MATLAB, and IDL, sometimes these pre-packaged tools can be overly complex for a simple application.
There are many details that arise with splines, including boundary conditions, creating basis functions, uneven knot positions, and extrapolation behavior.
Each of these topics are important and can play a large role in sophisticated spline applications, but they can also be overwhelming for some of the simplest cases where splines can be useful.

It is therefore useful to consider the equations for a single-domain cubic spline, which smoothly connects to endpoints with known values and slopes.
These equations are well known, and I have ported them here from wikipidea.
Consider representing a smooth function `$f(x)$` on the bounded interval `$x_0 \leq x \leq x_1$`, where we know the functions slope and value at the endpoints:
<div>$$
\begin{array}{ll}
f(x_0) &= y_0\\
f(x_1) &= y_1\\
f'(x_0) &= k_0\\
f'(x_1) &= k_1
\label{eq:constraints}
\end{array}
$$</div>
Since a cubic polynomial has only four parameters, these functional constraints uniquely define a single cubic polynomial that smoothly connects the domain boundaries.
We can simply write the resulting polynomial as:
<div>$$
f(x) = (1-t) y_0 + t y_1 + t(1-t)[a(1-t) + b t]
\label{eq:splinefunc}
$$</div>
where 
<div>$$
\begin{array}{ll}
t & = \frac{x-x_0}{x_1-x_0} \\
a & = +k_0 (x_1-x_0) - (y_1-y_0) \\
b & = -k_1 (x_1-x_0) + (y_1-y_0) \\
\end{array}
$$</div>
By evaluating Equation \eqref{eq:splinefunc} at the boundaries, we can easily verify that all of the constraints given in Equation \eqref{eq:constraints} are obeyed.
As alluded to in the intro, there are many applications for such a simple use case.
Personally, I have just used this method to smooth the heat transfer behavior at the onset of convection in the magma ocean modeling project I am working on.

Though smoothing techniques are crucial to many numerical investigations, I must end with a word of caution.
When smoothing data or functions, we need to be **VERY** careful, recognizing that we are artificially altering the inputs, with the hope that this will *improve* the result.
It can also introduce artificial behavior or numerical artifacts, which may mask the *true* behavior.
So before you smooth, think about the problem and make sure that it is physically justified.
Secondly, you should perform resolution tests to find the optimal amount of smoothing to use.
In the equations above, the smoothing length-scale corresponds to the width of the domain `$\Delta x = x_1-x_0$`.
Thus if we wish to smooth out a kink in our data located at `$x_r$`, we can use a cubic spline in the domain `$x_r - \Delta x \big/ 2 \leq x \leq x_r + \Delta x \big/ 2$`.
We must try out a range of `$\Delta x$` values to ensure that we smooth enough to get nice results, but not so much that we change the behavior of the system by introducing numerical artifacts.


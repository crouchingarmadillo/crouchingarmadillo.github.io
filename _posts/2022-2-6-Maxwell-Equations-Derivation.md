---
layout: post
title: Deriving Maxwell's Equations
mathjax: true
excerpt: "Maxwell's equations, together with the Lorentz Force Law tell us everything there is to know about classical Electrodynamics. They're usually motivated with experimental considerations. However, in this post we will explore pure theory, how Coulomb's Law, together with conservation of charge, and respecting special relativity, leads us inevitably to Maxwell's equations."
---
Maxwell's equations, together with the Lorentz Force Law tell us everything there is to know about classical Electrodynamics. They're usually motivated with experimental considerations. However, in this post we will explore pure theory, how Coulomb's Law, together with conservation of charge, and respecting special relativity, leads us inevitably to Maxwell's equations.

We will be assuming the reader is familiar with electrostatics, [special relativity](/Special-Relativity-Locality), and tensors. The metric signature we will use is (-,+,+,+). [Natural Units](/Natural-Units-Constants/) will be used for simplicity, specifically setting $c = \epsilon_0 = 1$. We will work in cartesian coordinates to make life a bit easier, but these results can easily be extended to any coordinate system by replacing each partial derivative with a covariant derivative.

## Conservation of Charge
The first thing we will consider is conservation of charge.
\\[ \partial_t \rho + \partial_i j^i = 0 \\]
Here, $\rho$ is the charge density, and $j^i$ is the current density. This equation nicely tells us that $j^\mu = (\rho, j^i)$ must form a four vector, in order to be Lorentz invariant, else this would not be 0 in all reference frames. This is an important fact we will use to identify four-potential.

## Four-Potential
Coulomb's law in its modern form is just the static version of Gauss's law along with Poisson's equation. We denote the electric field by $E^i$ and the electric potential by $V$.
\\[ \partial_i E^i = -\partial_i \partial^i V = \rho \\]
The most straightforward change we can make to move towards Lorentz invariance is to replace the divergence $\partial_i$ with the four divergence $\partial_\mu$ and laplacian $\partial_i\partial^i$ with the four-laplacian $\partial_\mu\partial^\mu$
\\[ \partial_\mu E^\mu = -\partial_\mu \partial^\mu V = \rho \\]
As we noticed from conservation of charge though, $\rho$ is the time component of a four-vector. Thus, $V$ must also be the time component of some four-potential, $A^\mu$. The electric field $E^\mu$ must be the time component $F^{0\mu}$ for some tensor $F^{\alpha\mu}$. This is all required by Lorentz invariance. Once we identify $A^\mu$ it will obey $-\partial_\nu\partial^\nu A^\mu = j^\mu$. 
We can express the electric field in terms of the potential along with some vector that has appropriate divergence.
\\[ E^i = -\partial^i V + Q^i \\]
This is consistent as long as we require $\partial_i Q^i + \partial_t\partial^t V = 0$. From this equation, and requiring Lorentz invariance we identify $Q^i = \partial^t A^i$.
So now we have a general expression for the electric field in terms of potential.
\\[ E^i = \partial^0 A^i - \partial^i A^0 \\]
This is immediately suggestive and tells us what the tensor $F^{\mu\nu}$ is from earlier. We define the electromagnetic tensor.
\\[ F^{\mu\nu} := \partial^\mu A^\nu - \partial^\nu A^\mu \\]
This tensor is anti-symmetric, and hence its diagonal is 0. We know $E^i = F^{0i} = -F^{i0}$. So the only mystery left is $F^{ij}$. This is the magnetic field, and we recognize that in this form, $F^{ij}$ is just the curl of $A^i$. So we make the following definition for the magnetic field $B_i$. Here $\epsilon_{ijk}$ is the Levi-Civita tensor.
\\[ B_i := \epsilon_{ijk}\partial^j A^k \\]

## Maxwell's Equations
Alright, now that we've got that background, we're ready to start deriving Maxwell's Equations. They all come from the structure of the Electric and Magnetic fields expressed in terms of potential. And we can get all the equations just by differentiation. Gauss's law stays the same.
\\[ \partial_i E^i = \rho \\]
Now we take the curl of the electric field to give Faraday's Law.
\\[ \epsilon_{ijk}\partial^j E^k = \epsilon_{ijk}\partial^j \partial^0 A^k = -\partial_t B_i \\]
Next we turn our attention to the magnetic field. Any divergence of a curl gives us 0. So this is Gauss's law.
\\[ \partial_i B^i = 0 \\]
For the final equation, we will use the double curl identity curlcurl$a^i$ = $\partial^i \partial_j a^j - \partial_j \partial^j a^i$. <center>
$$\begin{align*}
\epsilon^{ijk}\partial_j B_k &= \partial^i \partial_j A^j - \partial_j \partial^j A^i  \\
&= \partial^i(-\partial_t V) -\partial_j \partial^j A^i \\
&= \partial_t E^i - \partial_t \partial^t A^i - \partial_j \partial^j A^i \\
\end{align*}$$ </center> \\
On the second line we used the condition on divergence of $A^i$ and on the final line we used the identity of the electric field in terms of potential. This yields the final maxwell equation, the Maxwell-Ampere law.
\\[ \epsilon^{ijk}\partial_j B_k = j^i + \partial_t E^i \\]

## Lorentz Force Law
We now have everything, except for the Lorentz Force Law, let's finish the job. To make things easier using relativistic invariance, we shall work with the four-force $f^\mu = \gamma \frac{dp^\mu}{dt}$ instead. In ordinary electrostatics, the definition of the electric field acting on a charge $q$ is as follows.
\\[ f^i = q\gamma E^i = q\gamma F^{0i} = -q\gamma F^{i0} \\]
In order to be relativistically invariant, there's only one way to rewrite this in the general case, some four-vector $u_\mu$ contracts with $F^{i\mu}$, and $u_0 = -\gamma$. Do we know a four-vector that satisfies these properties? Yes, the proper-velocity $u^\mu = \gamma \frac{dx^\mu}{dt}$. Thus, now we know. 
\\[ f^i = q u_{\mu}F^{i\mu} \\]
Let's move back to the force $F^i$ and velocity $\dot x^\mu = \frac{dx^\mu}{dt}$
\\[ F^i = q \dot x_\mu F^{i\mu} \\]
Let's expand this and re-express in terms of electric and magnetic fields.
\\[ F^i = q(\dot x_0 F^{i0} + \dot x_j F^{ij}) = q(E^i + \dot x_j F^{ij}) \\]
Alright so what is this $x_j F^{ij}$ term? Well it's going to involve the magnetic field because it only has the spatial components of the electromagnetic tensor. Let's expand it out.
\\[ \dot x_j F^{xj} = \dot y B_z - \dot z B_y = \epsilon^{xjk}\dot x_j B_k \\]
Alright it's pretty clear we're going to get the same thing with the y, z components, in general this is the cross product of the velocity with the magnetic field. So finally we have the Lorentz Force Law in its usual form.
\\[ F^i = q(E^i + \epsilon^{ijk}\dot x_j B_k) \\]

And that's it! We've done it, all of Maxwell's Equations and the Lorentz Force Law, all with theoretical arguments. It is clear that conservation of charge along with special relativity put very strong constraints on what the electric and magnetic fields can do. I find this absolutely incredible, because conservation of charge, and special relativity are pretty reasonable things to want and expect out of a theory.
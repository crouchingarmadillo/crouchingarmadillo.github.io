---
layout: post
title: Special Relativity from Locality
mathjax: true
excerpt: "Special Relativity (SR) is an area of physics that is often motivated using electrodynamics. Historically, that's how it was developed in the first place. However, SR is something that makes sense even without involving electrodynamics. This post will explore how we can expect the results of SR just using the principle of locality. "
---
Special Relativity (SR) is an area of physics that is often motivated using electrodynamics. Historically, that's how it was developed in the first place. However, SR is something that makes sense even without involving electrodynamics. This post will explore how we can expect the results of SR just using the principle of locality.

## Inertial Reference Frames
First we would like to focus on the idea behind Newton's First Law, because this idea is oh so important in physics, the idea of an inertial reference frame. An inertial reference frame has a simple definition, it is a reference frame that is not accelerating. This does leave us a bit of freedom, it allows us to consider any reference frame traveling at a constant velocity relative to some other reference frame. The most barebones example in classical mechanics is to consider some fixed point such as a point on the ground, declare this to the origin of our coordinate system, and measure someone's velocity relative to this fixed point. Let's consider some particle moving relative to some fixed frame $\boxed S$ with speed $v$ along the +x-axis of $\boxed S$.
\\[ \boxed{S} \bullet \overset{v}{\to}  \\]
Something we wonder is, in the particle's frame $\boxed{S'}$, what are its coordinates in terms of the coordinates of $\boxed S$? Basic common sense tells us that the two frames should be the exact same, except $\boxed{S'}$ should see everything else move along the -x'-axis with speed $v$ compared to $\boxed S$. This idea yields the following differential equations.
\\[ \dot x' = \dot x - v \\]
\\[ \dot y' = \dot y \\]
\\[ \dot z' = \dot z \\]
And the starting origins coincide, and we assume time is absolute so the solutions yield the *Galilean Transformations*.
\\[ t' = t \\]
\\[ x' = x - vt \\]
\\[ y' = y \\]
\\[ z' = z \\]
So is this the final answer for what $\boxed{S'}$ sees? Funnily enough, no, our common sense assumption that velocities in different reference frames just add simply is wrong. In fact, the idea of locality will tell us right away this is wrong, at least for very large $v$. The Galilean Transformation is so accurate for low speeds, the realm of non-relativistic physics, that we cannot measure any difference really. But this is not true in general as we shall see.

## Locality
Intuitively, we expect that if two particles are separated in space, they can't interact instantaneously, because well this wouldn't make any sense, also it'd be very pathological. If anything could affect anything else in the universe instantly, how could we make sense of anything? If you find someone rudely broke your window, where would we expect to find that person? Not on the other side of the planet, we'd expect them to be in some neighborhood near us, in the same town/city probably, experience tells us this. But ok, how can we capture this idea of locality precisely? Well, it just means there's a speed limit in the universe, which we call $c$. This is necessary, because if the speed something could move at was unbounded, i.e. could move infinitely fast, then locality would not be possible, some particle could instantly move anywhere else and affect it instantly from anywhere in space. Is there something else we should expect about $c$? Yes, we should expect it's the same in any inertial reference frame, because no inertial reference frame is special, they should all produce the same laws of physics, as we discussed in the last paragraph. Notice that if we have a particle traveling at speed $c$ in say frame $\boxed{S'}$, the gallilean transformation violates this principle of locality, because it tells us the particle will travel faster than $c$ relative to $\boxed{S}$. What is the resolution to this? There's only one consistent way out of this, we require that if something is traveling at $c$ in one reference frame, it travels at speed $c$ in all reference frames. This might seem a bit of a leap, and do we have any experimental evidence for such a thing? Yes, the Michelson Morley experiment demonstrated that photons (particles of light) travel at the same speed $c =$ 299, 792, 458 m/s in every reference frame. Because of this, $c$ is often called the speed of light, but it should more accurately be called the speed of causality, because this is the speed any piece of information travels at, such as fields. Alright so the Gallilean transformation is wrong, both from a theoretical standpoint of violating locality, as well as experimental, where we have light demonstrating exactly what we should expect from locality. How can we fix the transformations?

## Scalars
The way we figure things out is how physicists always love figuring things out, appealing to symmetry, in fact, that's what we've been doing all along, arguing no inertial reference frame is special. What we need to do, is identify some scalar, i.e. a quantity that is the same for all reference frames, and figure out how to compute it in general. $c$ is a scalar, but unfortunately it's a constant too, we need to find some variable or parameter to keep track of. In non-relativistic physics, we used $t$ as a parameter and took it as absolutely the same in all reference frames. What happens if we try to use that? Well unfortunately, it just won't work. This will be illustrated with the following classic argument. Consider some fixed frame $\boxed{S}$ and we call its coordinates $t, x$. We will have a train, call it frame $\boxed{S'}$ with coordinates $t', x'$ it will move to the right with speed $v$ relative to $\boxed S$.
![Alt Text](/images/Train_Moving_on_x-axis.jpg)
We're going to fix some mirror to the top of the train, and send a pulse of light from the bottom of the train to the top. We will use the constantcy of the speed of light to show $t' \neq t$. Alright, so suppose all this happens over some time interval $\Delta t$ in $\boxed S$ and $\Delta t'$ in $\boxed{S'}$. Here we illustrate what each frame sees. The $\boxed S$ frame is a mess, because we have to draw successive frames to really see what's happening, but light will travel in a straight line with horizontal and vertical components because the train is moving.
![Alt Text](/images/Special_Relativity_Train_Frames.jpg)
We will label the height of the train as $h$. In frame $\boxed{S'}$ the light travels at speed $c$ in time $\Delta t'$ and hence the total distance $h = c\Delta t'$, solving for $c$ we have $c = \frac{h}{\Delta t'}$. For $\boxed S$, we have to apply the pythagorean theorem, and light travels distance $c\Delta t = \sqrt{h^2 + v^2 \Delta t^2}$, because the train travels a distance $v\Delta t$. So interestingly, we've also shown that lengths and distances don't stay the same across reference frames. Anyway, now we solve for $c$ and set both sides equal we have.
\\[ \sqrt{\frac{h^2}{\Delta t^2} + v^2 } = \frac{h}{\Delta t'} \\]
Now we confess that $h$ is really just an artificial vehicle here, but we don't really care about it because the height of our reference frame is arbitrary, so we're gonna substitue in $h = c\Delta t'$ and solve for $\Delta t$. We end up finding so called time dilation. 
\\[ \Delta t = \frac{\Delta t'}{\sqrt{1- \frac{v^2}{c^2}}} \\]
So we see that in general, time between different reference frames will not be the same, unless we take the limit as $v/c$ goes to 0. This factor of $\frac{1}{\sqrt{1- \frac{v^2}{c^2}}}$ is so important that it gets a special name and is written as just $\gamma$. There is something else pretty awesome about the particular thought experiment we picked. The time interval $\Delta t'$ is very special, because it is the time interval between two events, that happen at the **same place**. In any other reference frame, light being sent, and coming back would happen in two different places. So this is a special frame of reference for this particular event, and it is agreed upon by every other frame, and hence its time is special. We call this time where an event occurs in the same place in space, proper time $\pi$. Well most people use $\tau$ for proper time, but I'm using that for the circle constant haha. So we now know for any reference frame $\boxed S$, $\Delta t = \gamma \Delta\pi$. This is a very powerful relation, and it tells us we have a scalar time to consider, proper time, and we can use this to parameterize things as we please. 

## Four-Vectors
In what is coming, we will use the notation of tensors freely because it's pretty sweet and is the appropriate language for relativity. For any who wish to learn it, I strongly recommend chapter 12 of James Nearing's excellent [Math Tools for Physics](http://www.physics.miami.edu/~nearing/mathmethods/). Alright so, we now know that time is no longer absolute, we must consider it as a part of our physics that depends on the reference frame. The most natural way is to begin considering time and space on equal footing, we call this spacetime. We collect our position into a four-vector $x^\mu = (ct, \vec x)$. By convention, greek indices are used for four-vectors, whereas latin indices are used for ordinary three-vectors, and 0 is used to mean the time component. What are the four-vectors for all our other physical quantities? Well to figure that out we need to figure out how four-vectors transform. Since proper time is a scalar, the easiest way to do it is to require the *Lorentz Transformations* leave proper time invariant. If we're going to do this though, we need an actual way to compute proper time, since we kinda left it implicit in the time dilation formula. Let's rectify that! So first of all, the formula we derived in terms of speed holds true for an arbitrary reference frame with any velocity, because it's arbitrary what we decided to call the x-axis, and we could just as well chosen any other axis. Now suppose we have an object moving with, an arbitrary constant velocity $\dot{\vec{x}} = \frac{\Delta\vec{x}}{\Delta t}$. Time dilation gives us the following formula.
\\[ \Delta t = \frac{\Delta \pi}{\sqrt{1 - \frac{|\dot{\vec{x}}|^2}{c^2}}} \\]
Now we solve for the proper time, squared and scaled by c for simplicity.
\\[ c^2\Delta\pi^2 = c^2\Delta t^2 - \Delta x^2 - \Delta y^2 - \Delta z^2 \\]
We require that this be invariant, and many sources will call this the spacetime interval. We're going to make a slight tweak though and attach a minus sign and define the spacetime interval $\Delta s^2 = -c^2\Delta\pi^2$. Why? Well, since the sign choice is arbitrary, as what's important is this thing isn't changed, we may as well pick the sign choice that yields an interval closely mimicking the distance for 3-vectors, and has less minus signs. This immediately yields the following choice of metric $\eta_{\mu\nu}$. \\
$$ \eta_{\mu\nu} = \begin{pmatrix}
-1 & 0 & 0 & 0 \\
0 & 1 & 0 & 0 \\
0 & 0 & 1 & 0 \\
0 & 0 & 0 & 1 
\end{pmatrix} $$
Since $\Delta x^\mu$ forms a four-vector, we can construct a four-velocity, by just dividing by the proper time. $u^\mu := \frac{\Delta x^\mu}{\Delta\pi}$
We can keep going, forming the four-momentum $p^\mu = mu^\mu$. But I think you guys get the idea. So that's it! We've now found all the ideas of special relativity. We will end this off by constructing a lorentz transformation $\Lambda^\mu_{\ \nu}$ analogous to the galilean transformation. We will assume frames $\boxed S, \boxed{S'}$ with $\boxed{S'}$ moving with speed $v$ along the +x-axis relative to $\boxed S$. By symmetry, we agree on the $y,z$ values, so let's figure out what the $t,x$ values are.
\\[ x^2 - c^2 t^2 = x'^2 - c^2 t'^2 \\]
First we construct a more general lorentz transformation $t,x$. Consider the following rotation matrix with parameter $\phi$. \\
$$ R^\mu_{\ \nu} = \begin{pmatrix} 
\cos\phi & -\sin\phi & 0 & 0 \\
\sin\phi & \cos\phi & 0 & 0 \\
0 & 0 & 1 & 0 \\
0 & 0 & 0 & 1
\end{pmatrix} $$ \\
This is one of the most general transformations that preserves $x^2 + c^2 t^2$. We're using the circle trignometric functions. However, $x^2 - c^2 t^2$ is a hyperbolic geometry, so we must replace the trig functions with hyperbolic functions. Thus, it is reasonable to guess the following matrix is a general lorentz transformation. Let's check. \\
$$ L^\mu_{\ \nu} = \begin{pmatrix} 
\cosh\phi & -\sinh\phi & 0 & 0 \\
\sinh\phi & \cosh\phi & 0 & 0 \\
0 & 0 & 1 & 0 \\
0 & 0 & 0 & 1
\end{pmatrix}$$ \\
When we expand this out however, we get.
\\[ (\sinh\phi ct + \cosh\phi x) - (\cosh\phi ct - \sinh\phi x)^2 = x^2 - c^2 t^2 + 2\cosh\phi\sinh\phi  \\]
This sadly is not what we wanted. Where did we go wrong? Well, the cross terms didn't cancel, and that's because we had the sign wrong on our $\sinh\phi$ in the 10 entry, it needs to be negative, and this fixes it. So now we can write down with confidence that the following is a general Lorentz boost along the +x-axis. This is really good to know, because it places serious restrictions on what can be a Lorentz boost, we only have two entries to figure out.\\
$$ \Lambda^\mu_{\ \nu} = \begin{pmatrix} 
\cosh\phi & -\sinh\phi & 0 & 0 \\
-\sinh\phi & \cosh\phi & 0 & 0 \\
0 & 0 & 1 & 0 \\
0 & 0 & 0 & 1
\end{pmatrix}$$ \\
So what would the new version of the galilean transformation be? Once again we're going to guess and fix it up. The Galilean transformation moves $ct$ to $-\frac{v}{c} ct$ and $x$ to $x$ for $x'$. Let's then try this matrix. \\
$$ L^\mu_{\ \nu} = \begin{pmatrix} 
1 & -\frac{v}{c} & 0 & 0 \\
-\frac{v}{c} & 1 & 0 & 0 \\
0 & 0 & 1 & 0 \\
0 & 0 & 0 & 1
\end{pmatrix}$$
\\[ (-\frac{v}{c}ct + x)^2 - (ct - \frac{v}{c}x)^2 = \frac{1}{\gamma}(x^2 - c^2 t^2) \\]
So our guess was almost right, and Galilean transformation is close, we just need this gamma factor. So the Lorentz transformation analogous to the Galilean transformation is the following. \\
$$ \Lambda^\mu_{\ \nu} = \begin{pmatrix} 
\gamma & -\gamma\frac{v}{c} & 0 & 0 \\
-\gamma\frac{v}{c} & \gamma & 0 & 0 \\
0 & 0 & 1 & 0 \\
0 & 0 & 0 & 1
\end{pmatrix}$$



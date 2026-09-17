---
layout: page
title: The sound of spacetime
eyebrow: Rabbit Holes
permalink: /rabbit-holes/gravitational-waves/
back_url: /rabbit-holes/
back_label: Rabbit Holes
---

Classical gravitational theory served science very well for many centuries, as we had a hint of in the [The Three Body Problem]({{ "/rabbit-holes/three-body-problem/" | relative_url }}) card. It is now worldwide known how the work of Nobel-Prize winner Albert Einstein brought groundbreaking innovation to many areas of physics, including gravitation. Although he is mostly known for what people call *the world's most famous equation*

$$
E=mc^2
$$

already published in 1905 in one of his four milestone papers, it's his later work on general relativity (1915) that we're interested in for this card. With him, the word "spacetime" went from science-fiction jargon to being the way we actually have to understand reality. His theories were so visionary that it took decades — in some cases the better part of a century — to confirm experimentally what his equations predicted.

The question now is: how do numerical methods enter this picture?

*Numerical relativity* is the field of computational science dedicated to the simulation of Einstein's field equations. This recent (~15 years), active research strand turned out to be crucial not only for simulating but also for validating the discoveries stemming from the notion that space and time are intrinsically coupled. For those interested in getting acquainted with such a cool topic without being a pure physicist, my starting point was Baumgarte & Shapiro's *Numerical Relativity: Starting from Scratch*, which builds the whole machinery up from a 1+1 toy problem before tackling real binary inspirals — I'm borrowing from its first chapter here.

## Newton and Einstein side-by-side

In order to fully understand the intricacies of Einstein's theory one would need many university-level courses such as Differential Geometry, Gravitational Physics, and so on. We'll take a shortcut here and hyper-simplify things, while still trying to keep the core modeling ideas intact. It's useful to put what we're used to from Newton's theory side-by-side with what Einstein used instead. We'll repeat here a table presented in Chapter 1 of *Numerical Relativity: Starting from Scratch* and slowly go through it with dedicated explanations.

| Relation to fundamental quantity   |      Newton      |  Einstein |
|--------------------------|:-------------------------:|--------------------------------------:|
| Fundamental quantity     | $$\phi$$                  | $$g_{ab}$$                            |
| Equation of motion       | $$\nabla\phi$$            | $$\Gamma_{bc}^{a}$$                   |
| Geodesic deviation       | $$\nabla^2\phi$$          | $$R^{a}_{bcd}$$                       |
| Field equation l.h.s.    | $$\Delta\phi$$            | $$G_{ab}$$                            |
| Field equation           | $$\Delta\phi=4\pi G\rho$$ | $$G_{ab}=\frac{8\pi G}{c^4}T_{ab}$$   |

### Fundamental quantity
This is what objects react to. In Newton's theory this was a potential, i.e. a scalar function whose value was dictated by the mass distribution in space. In Einstein's case, this is substituted with a rank-$$2$$ tensor (you can visualize it as a matrix). The innovation is that this tensor is the spacetime *metric*, i.e. the measure of the *geometry* of spacetime. It has indices that span $$4$$ coordinates, time and the three spatial components. Note two changes in paradigm:
1. Time and space are dealt with in a unified way, i.e. time is just another coordinate, coupled to the space ones through the metric (the off-diagonal terms express the coupling).
2. Objects do not react to a certain potential but to the *shape* of spacetime itself. So free-falling objects try to go as straight as possible, but they need to follow the spacetime curvature, and that is why their trajectories may be curved.

### Equation of motion
This term describes how the object moves. From Newton's laws of motion and gravitation we had

$$
m_I\b{a} = \b{F} = -m_G\nabla\phi
$$

where $$\b{g}=-\nabla\phi$$ was the gravitational acceleration. This meant that the *inertial* acceleration of a body was dictated by the changes in gravitational potential times a constant, the gravitational mass $$m_G$$. Now note that we used two different subscripts and names for the mass term. This is because, in principle, nothing tells us that those two masses should be equal, but in classical mechanics they are assumed to be. In Newton's law of gravity, the so-called *equivalence principle* is treated as an empirical observation — a hypothesis motivated by experiment, not a consequence of the theory itself. In Einstein's model of gravity, the equivalence principle is a consequence of physics itself: matter tells spacetime how to curve, and spacetime tells matter how to move.

Passing to Einstein's side, we need to "take derivatives" of the fundamental quantity. Now, once we talk about non-Euclidean spaces, such as the $$4$$-dimensional manifold that is spacetime, there are different, special ways of taking the analogue of the *directional derivative*. One of them, closely linked to the Euclidean gradient, is the so-called *covariant derivative*. We won't go into details here, but it is enough to know that this derivative is completely determined by its so-called *Christoffel symbols* $$\Gamma_{bc}^{a}$$, which describe how the metric changes from point to point and can be used to take derivatives on manifolds. In particular, given a certain basis, they can be expressed in terms of first derivatives of the metric (read "first derivatives of the fundamental quantity")

$$
\Gamma^{a}_{bc} = \frac{1}{2}g^{ad}(\partial_{c}g_{db}+\partial_{b}g_{dc}-\partial_{d}g_{bc})
$$

where $$g^{ab}$$ is the inverse of $$g_{ab}$$.

### Geodesic deviation

The problem with the above — and this was true in the Newtonian case too — is that it is frame-dependent. In fact, one can always choose coordinates so that the Christoffel symbols mentioned above vanish and the spacetime is locally flat (Minkowski spacetime). To understand, in a frame-independent way, how spacetime changes, we need to take yet another derivative. If in the Newtonian case the result is the *tidal tensor* $$\nabla^2\phi$$, in the general relativity case we obtain the *spacetime curvature* $$R^{a}_{bcd}$$. The spacetime curvature is a frame-independent measure of the gravitational field.

### Field equations

We are ready now to close the loop and reconnect the motion with what caused it. In the Newtonian case, the two were related by the *trace* of the tidal tensor

$$
\mathrm{Tr}(\nabla^2\phi) = \Delta \phi = 4\pi G \rho
$$

The same happens in Einstein's case, and, by contracting (a.k.a. taking the trace) two indices in the rank-$$4$$ spacetime curvature tensor, we obtain the *Ricci tensor*

$$
R_{ab}\equiv R^c_{acb}
$$

where we used the *Einstein summation convention* — repeated indices ($$c$$ above) are summed over. One can also go further and take the trace of the remaining indices to obtain the *Ricci scalar* $$R=g^{ab}R_{ba}$$. The need to use $$g^{ab}$$ is linked to tensor algebra matters (raising an index with the inverse metric) that we skipped for the sake of simplicity.

We thus have that the metric $$g_{ab}$$, the Ricci tensor $$R_{ab}$$ and the Ricci scalar $$R$$ can all take part in the left-hand side of the field equations. Due to energy and momentum conservation arguments, the successful combination of these terms is the *Einstein tensor*

$$
G_{ab}\equiv R_{ab}-\frac{1}{2}Rg_{ab}
$$

The final step: what goes in place of the mass density $$\rho$$ in Einstein's case? The stress-energy tensor $$T^{ab}$$, which encodes different sources of mass-energy (recall that mass and energy are interchangeable in Einstein's theory). Requiring the relation between $$G_{ab}$$ and $$T_{ab}$$ to reduce to the Newtonian field equation in the non-relativistic limit leaves us with the relation

$$
G_{ab} + \Lambda g_{ab} = 8\pi T_{ab}
$$

(in units where $$G=c=1$$). These are the infamous *Einstein's field equations of general relativity*.

## Gravitational Waves

As one can imagine, Einstein's field equations are a very complex set of equations to solve. They show up as a system of 10 highly nonlinear, coupled PDEs. Even worse, they are not a classical evolution problem: there is no built-in notion of "time" to march forward in. A lot of effort has been put into actually taming their complexity and reducing them to a more familiar initial-value PDE system. A very interesting simplification is considering a small perturbation from a "background metric". Specifically, let's assume the background is the constant flat Minkowski metric

$$
\eta_{ab}=
\begin{bmatrix}
 -1 & 0 & 0 & 0 \\
 0 & 1 & 0 & 0 \\
 0 & 0 & 1 & 0 \\
 0 & 0 & 0 & 1
\end{bmatrix}
$$

and a perturbation $$\norm{h_{ab}}<<1$$ such that the total metric is $$g_{ab}=\eta_{ab}+h_{ab}$$. By plugging this inside Einstein's field equations and dropping all the terms in $$h_{ab}$$ that are higher than linear order, one can simplify the initial equations to reduce to

$$
(-\partial_t^2+\Delta)\overline{h}_{ab} = -16\pi T_{ab}.
$$

These are the linearized field equations for weak gravitational fields. Here, $$\overline{h}_{ab} = h_{ab}-\eta_{ab}h/2$$ is the trace-reversed metric perturbation and $$h=\eta^{cd}h_{cd}$$. Note that $$\partial_t^2$$ and $$\Delta$$ reduce to the ordinary second-order time derivative and the flat-space Laplace operator. Looking closely at the left-hand side, one understands that this is a *wave equation* for the perturbation.

### The chirp 

Solving a linear wave equation with a source is a well-understood problem, and a lot can actually be worked out by hand for this one. Think of it like ripples on a pond: when two massive objects swing around each other, they shake the fabric of spacetime, and those shakes spread outward as waves, exactly as the equation above describes. Just like ripples carry energy away from a stone dropped in water, gravitational waves carry energy away from the orbiting pair. That energy has to come from somewhere, so the orbit itself pays for it: the two bodies drift slightly closer together, which — exactly as in the two-body problem — makes them orbit faster. A faster orbit means a higher-frequency wave, and that rising pitch and loudness as the pair spirals together is the whole story behind the "chirp." One specific case made history on the 14th of September 2015, 100 years after Einstein's work on general relativity.

Working this out precisely for two massive objects orbiting each other, the wave equation above admits an analytical solution built from retarded Green's functions. It turns out that (taking $$G=c=1$$ for simplicity):
1. The orbit loses energy at a rate

$$
\frac{\mathrm{d} E}{\mathrm{d} t} = -\frac{32}{5}\frac{M^3\mu^2}{R^5}
$$

where $$M=m_1+m_2$$ is the total mass, $$\mu = \dfrac{m_1m_2}{m_1+m_2}$$ is the reduced mass (as introduced in the [two-body problem]({{ "/rabbit-holes/three-body-problem/" | relative_url }}) card), and $$R$$ is the separation between the two bodies.
2. The energy loss causes the separation $$R$$ to shrink at a rate

$$
\frac{\mathrm{d} R}{\mathrm{d} t} = -\frac{64}{5}\frac{M^2\mu}{R^3}
$$

In other words, gravitational waves drain energy out of the binary system, causing it to spiral inward and eventually collide.
3. The frequency of the emitted gravitational wave (twice the orbital frequency, since the source's shape repeats twice per orbit) evolves as

$$
f_{GW} = \frac{5^{3/8}}{8\pi}\frac{1}{\mathcal{M}^{5/8}(T-t)^{3/8}}
$$

where $$\mathcal{M}=M^{2/5}\mu^{3/5}$$ is the so-called *chirp mass* and $$T$$ is the time of collision.


The Hulse–Taylor pulsar, discovered in 1974, was the first binary pulsar ever found: a system in which two neutron stars orbit each other, one of which is a pulsar — an immensely fast-rotating neutron star that sweeps a beam of radiation past us once per rotation, like a lighthouse. Because one of the two stars is a pulsar, we can time its pulses extremely precisely, and from that timing infer the orbital period to very high accuracy. This has been tracked since 1975, and the resulting measurements over the years are shown as the red dots in the figure below.

<figure class="figure">
  <img src="{{ "/assets/numalg/HulseTaylor.png" | relative_url }}" alt="Evidence of orbital decay in PSR B1913+16. The data points indicate the observed change in the time of periastron with date, relative to a system not undergoing decay. The parabola illustrates the theoretically expected change according to general relativity.">
  <figcaption>Evidence of orbital decay in PSR B1913+16. The data points indicate the observed change in the time of periastron with date, relative to a system not undergoing decay. The parabola illustrates the theoretically expected change according to general relativity.</figcaption>
</figure>

You can see how the orbital period appears to decay with time. Almost every scientist, if asked what the blue line is, would probably say it's a fit to the orbital decay. Well, it turns out that's not a fit at all — it's the prediction general relativity makes, given only the system's initial measured values! And it fits extremely well. This was one of the first *indirect* tests of general relativity.

The first *direct* (!) test of general relativity happened on the 14th of September 2015, when the LIGO and Virgo labs were able to detect experimentally (!!) the passing of a gravitational wave on Earth. That means scientists were able to measure a tiny stretching and squeezing of space on Earth and match it to a black hole collision that happened roughly 1.3 billion light-years away.

## Numerical relativity

It is at this point that numerical relativity comes into play. The LIGO and Virgo labs use astronomically precise optical equipment called a laser interferometer to measure variations in distance. The output of these measurements is a variation in the intensity of a laser signal, connected to tiny changes in distance. The signal is analyzed by studying its frequency and amplitude over time. What was done for this very first discovery was to simulate a huge number of black-hole spirals and mergers (using numerical relativity and other strategies), and then extract the frequency response that each such event would leave on the interferometers on Earth. These catalogs were then continuously compared against the output of the experimental apparatus. It was a true gift to have a signal show up as soon as the experiment was operational!

To get a feel for this, let's plot the frequency evolution predicted by the analytical formula above for the first detected gravitational wave, GW150914.

```python

import numpy as np
import matplotlib.pyplot as plt

# ------------------------- inputs -------------------------
# G, c below are in cgs (cm, g, s), so all masses must be in grams.
Msun = 1.989*10**33
Parsec = 3.086*10**18
Mpc = 1.0e6*Parsec

# Component masses (Msun), luminosity distance (Mpc), and the GW frequency
# at which the signal enters the detectors' sensitive band (Hz).
EVENTS = {
    "GW150914": dict(m1=36.0, m2=29.0, distance_Mpc=410.0, f_start=30.0),
    "GW170817": dict(m1=1.46, m2=1.27, distance_Mpc=40.0, f_start=40.0),
}

EVENT = "GW150914"  # switch to "GW170817" to reproduce the other event

event = EVENTS[EVENT]
m1, m2 = event["m1"]*Msun, event["m2"]*Msun
R0 = event["distance_Mpc"]*Mpc

M = m1 + m2
mu = m1 * m2 / M
Mchirp = mu**(3/5) * M**(2/5)
T = 0
c = 3*10**10
G = 6.673*10**(-8)

# Cutoff frequency used to avoid the final blow-up
f_crit = 4.9*10**3 * (Msun/Mchirp)  # Hz

def frequency(t):
    f = (5**(3/8)/(8*np.pi))*(c**3/G/Mchirp)**(5/8) / (T - t)**(3/8)
    if f[-1] > f_crit:
        raise ValueError("Frequency exceeds critical value.")
    return f

def tau_of_f(f):
    """Invert frequency(t) to get time-to-merger (T - t) for a given GW frequency."""
    coef = (5**(3/8)/(8*np.pi))*(c**3/G/Mchirp)**(5/8)
    return (coef/f)**(8/3)

# Start where the event enters the detectors' sensitive band and stop just
# below f_crit, i.e. just before this leading-order approximation breaks down.
tau_start = tau_of_f(event["f_start"])
tau_end = tau_of_f(0.98*f_crit)
# A high point count is needed to resolve the orbital phase near f_crit
# without aliasing, especially for long, slowly-chirping signals like GW170817.
t = np.linspace(T - tau_start, T - tau_end, 2000)

f = frequency(t)

fig, ax = plt.subplots(figsize=(8, 6))
ax.semilogy(t, f)
ax.set_xlabel('Time (s)')
ax.set_ylabel('Frequency (Hz)')
ax.set_title(EVENT)

fig.savefig(f"binary_chirp_{EVENT}.png", dpi=150)
```

<figure class="figure">
  <img src="{{ "/assets/numalg/binary_chirp_GW150914.webp" | relative_url }}" alt="Analytical frequency evolution for the gravitational wave GW150914.">
  <figcaption>Analytical frequency evolution for the gravitational wave GW150914.</figcaption>
</figure>

And let's have a look at what the orbits of the two black holes look like

```python
def R_of_t(t):
    return (G*Mchirp/c**2) * (5*c**5/(256*G*Mchirp))**(1/4) * (T - t)**(1/4)
R = R_of_t(t)

def omega_of_t(t):
    return frequency(t) * np.pi

def R_of_t(t):
    return (G*Mchirp/c**2) * (5*c**5/(256*G*Mchirp))**(1/4) * (T - t)**(1/4)

def tau_of_f(f):
    """Invert frequency(t) to get time-to-merger (T - t) for a given GW frequency."""
    coef = (5**(3/8)/(8*np.pi))*(c**3/G/Mchirp)**(5/8)
    return (coef/f)**(8/3)

omega = omega_of_t(t)
phi = np.concatenate(([0.0], np.cumsum(0.5*(omega[1:] + omega[:-1]) * np.diff(t))))
x1, y1 = -(m2/M)*R*np.cos(phi), -(m2/M)*R*np.sin(phi)
x2, y2 =  (m1/M)*R*np.cos(phi),  (m1/M)*R*np.sin(phi)
 
# ------------------------- static trajectory plot -------------------------
fig, ax = plt.subplots(figsize=(6, 6))
ax.plot(x1, y1, lw=0.7, color="tab:blue", label=f"m1 = {m1}")
ax.plot(x2, y2, lw=0.7, color="tab:red", label=f"m2 = {m2}")
ax.plot(0, 0, "k+")
ax.set_aspect("equal")
ax.set_title(f"{EVENT} inspiral trajectory (chirp only, cut off before merger)")
ax.legend()
fig.savefig(f"binary_trajectory_{EVENT}.png", dpi=150)

```

<figure class="figure">
  <img src="{{ "/assets/numalg/binary_trajectory_GW150914.webp" | relative_url }}" alt="Analytical trajectory evolution for the gravitational wave GW150914.">
  <figcaption>Analytical trajectory evolution for the gravitational wave GW150914.</figcaption>
</figure>

The results from the actual observation, again taken from Wikipedia, are shown below

<figure class="figure">
  <img src="{{ "/assets/numalg/LIGO_measurement_of_gravitational_waves.svg" | relative_url }}" alt="LIGO measurement of the gravitational waves at the Hanford (left) and Livingston (right) detectors, compared with the theoretical predicted values.">
  <figcaption>LIGO measurement of the gravitational waves at the Hanford (left) and Livingston (right) detectors, compared with the theoretical predicted values.</figcaption>
</figure>

Actually visualizing what a gravitational wave looks like is tricky to code up directly, even with the analytical solution we found above. Qualitatively, though, we can lean on the analogy with Newtonian gravity: we already know gravitational waves obey the law

$$
(-\partial_t^2+\Delta)\overline{h}_{ab} = -16\pi T_{ab}.
$$

where $$(-\partial_t^2+\Delta)$$ is commonly referred to as the D'Alembert operator. Dropping down to the scalar version, we just get the classic 2D wave equation

$$
(-\partial_t^2+\Delta)\phi = f
$$

and we can lean on some established FEM code to simulate it. In this case, the gravitational waves produced by a binary inspiral behave a lot like a rotating quadrupole source driving this same wave equation. Here is the code for such a simulation using NgSolve (because I'm more acquainted with it):

```python
# %%
# A finite element simulation of a scalar wave equation with a rotating
# "quadrupole" source at the center of a circular domain -- a simple,
# visualizable stand-in for a gravitational wave. A damping layer near
# the outer edge absorbs the outgoing wave so it doesn't reflect back.

from ngsolve import *
from ngsolve.webgui import Draw
from netgen.geom2d import CSG2d, Circle
import time

# --- 1) Geometry: a circular domain, wave absorbed near the boundary ---
Rin = 2.0             # radius of the region we actually care about
pml_thickness = 0.5   # thickness of the absorbing outer ring
Rout = Rin + pml_thickness

geo = CSG2d()
maxh = 0.1

circle_big = Circle(center=(0, 0), radius=Rout, bc="bc_circle_1")
circle_small = Circle(center=(0, 0), radius=Rout/5, bc="bc_circle_2")
diff = circle_big - circle_small

circle_small.Maxh(maxh/5)
diff.Maxh(maxh)

geo.Add(diff)
geo.Add(circle_small)

mesh = Mesh(geo.GenerateMesh())
order = 3
mesh.Curve(order)

r_ = sqrt(x*x + y*y)

# --- 2) Source: a rotating dipole or quadrupole at the center ---
# A source rotating rigidly at angular speed Omega is just
# cos(m*Omega*t)*pattern_cos + sin(m*Omega*t)*pattern_sin for two fixed
# spatial patterns (m=1 for a dipole, m=2 for a quadrupole), so we only
# need to build those two patterns once and rescale them every step.
source_type = "quadrupole"   # "dipole" or "quadrupole"

d = 0.06
sigma_src = 0.015
amp = 40.0

def G(cx, cy):
    return exp(-((x - cx)**2 + (y - cy)**2)/(2*sigma_src**2))

if source_type == "dipole":
    m = 1
    pattern_cos = amp*(G(d, 0) - G(-d, 0))
    pattern_sin = amp*(G(0, d) - G(0, -d))
elif source_type == "quadrupole":
    m = 2
    pattern_cos = amp*(G(d, 0) + G(-d, 0) - G(0, d) - G(0, -d))
    pattern_sin = amp*(G(d, d) + G(-d, -d) - G(d, -d) - G(-d, d))
else:
    raise ValueError("source_type must be 'dipole' or 'quadrupole'")

wave_speed = 3
wavelength = 1.0
fcen = wave_speed/wavelength
Omega = 2*pi*fcen/m

# --- 3) FE space, matrices, and the absorbing sponge layer ---
fes = H1(mesh, order=order, dirichlet="bc_circle_1")
p, q = fes.TnT()

Mmat = BilinearForm(p*q*dx).Assemble()
Kmat = BilinearForm(grad(p)*grad(q)*dx).Assemble()   # discrete -Delta

# eta(x) ramps smoothly from 0 up to eta_max across the outer ring
# [Rin, Rout], damping the wave before it can reflect off the boundary.
eta_max = 60.0
eta = eta_max * IfPos(r_ - Rin, ((r_ - Rin)/pml_thickness)**2, 0.0)
Dmat = BilinearForm(eta*p*q*dx).Assemble()

freedofs = fes.FreeDofs()

# --- 4) Time stepping: Newmark-beta (unconditionally stable) ---
# The equation to march forward is M*p_tt + D*p_t + K*p = F(t). Newmark
# turns each step into a linear solve for p, against a matrix that never
# changes -- so we assemble and factorize it just once, up front.
dt = 0.025   # ~40 steps per period of the driving frequency
tend = 8

beta, gamma = 0.25, 0.5
c0 = 1/(beta*dt**2)
c1 = 1/(beta*dt)
c2 = 1/(2*beta) - 1
c3 = gamma/(beta*dt)
c4 = gamma/beta - 1
c5 = dt*(gamma/(2*beta) - 1)

Amat = Mmat.mat.CreateMatrix()
Amat.AsVector().data = c0*Mmat.mat.AsVector() + c3*Dmat.mat.AsVector() + Kmat.mat.AsVector()
Ainv = Amat.Inverse(freedofs, inverse="sparsecholesky")

Lsrc_cos = LinearForm(pattern_cos*q*dx).Assemble()
Lsrc_sin = LinearForm(pattern_sin*q*dx).Assemble()

# --- 5) Initial condition: start in balance with the source at t=0 ---
# Rather than ramping the source up from zero, we solve once for the
# field that's already in equilibrium with the source frozen at its t=0
# orientation. Initial velocity and acceleration are then exactly zero.
Kinv = Kmat.mat.Inverse(freedofs, inverse="sparsecholesky")

p0 = GridFunction(fes)
p0.vec.data = Kinv * Lsrc_cos.vec

pold, vold, aold = GridFunction(fes), GridFunction(fes), GridFunction(fes)
pold.vec.data = p0.vec
vold.vec[:] = 0
aold.vec[:] = 0

# --- 6) Time loop ---
gfp = GridFunction(fes)
gfp.vec.data = pold.vec
scene = Draw(gfp, order=3, autoscale=False,
             min=-0.01, max=0.01, deformation=True, scale=10)

probe_point = mesh(1.5, 0.0)   # a fixed point where we record the field
ts, probe_vals = [], []

anew = pold.vec.CreateVector()
vnew = pold.vec.CreateVector()
rhs = pold.vec.CreateVector()

t = 0.0
i = 0
vtkout = VTKOutput(mesh,coefs=[gfp],names=["gfp"],filename="./gr_wave/gr_wave",subdivision=2)
vtkout.Do(time = t)
with TaskManager():
    while t < tend:
        t_new = t + dt
        rhs.data = cos(m*Omega*t_new)*Lsrc_cos.vec + sin(m*Omega*t_new)*Lsrc_sin.vec
        rhs.data += Mmat.mat*(c0*pold.vec + c1*vold.vec + c2*aold.vec)
        rhs.data += Dmat.mat*(c3*pold.vec + c4*vold.vec + c5*aold.vec)

        gfp.vec.data = Ainv * rhs

        anew.data = c0*(gfp.vec - pold.vec) - c1*vold.vec - c2*aold.vec
        vnew.data = c3*(gfp.vec - pold.vec) - c4*vold.vec - c5*aold.vec

        pold.vec.data = gfp.vec
        vold.vec.data = vnew
        aold.vec.data = anew

        t = t_new
        i += 1
        ts.append(t)
        probe_vals.append(gfp(probe_point))
        if i % 4 == 0:
            scene.Redraw()

        vtkout.Do(time = t)

import matplotlib.pyplot as plt
plt.plot(ts, probe_vals)
plt.xlabel("t")
plt.ylabel("p(1.5, 0.0, t)")
plt.title(f"Classical FEM (H1 + Newmark) -- rotating {source_type} at the center")
plt.show()
```

<figure class="figure">
  <video src="{{ "/assets/numalg/gr_wave.mp4" | relative_url }}" poster="{{ "/assets/numalg/gr_wave.0320.webp" | relative_url }}" autoplay loop muted playsinline></video>
  <figcaption>Wave equation with rotating quadrupole forcing, as a proxy for gravitational wave visualization</figcaption>
</figure>

### But why do they call it chirp?

The frequency of the final ramp-up of GW150914 goes from ~30 to ~170 Hz. The audible range for the human ear is from ~20 to ~20,000 Hz. So it turns out that if that wave were not gravitational but a mechanical (sound) wave, we would actually be able to hear it! Here's a rendition of what that sound is for GW150914 — almost like a *bird chirp*.

<figure class="figure">
  <audio controls src="{{ "/assets/numalg/chirp.wav" | relative_url }}"></audio>
  <figcaption>Audio rendition of the GW150914 chirp, with the frequency sweep mapped directly onto an audible tone.</figcaption>
</figure>

*This page is a starting draft.*

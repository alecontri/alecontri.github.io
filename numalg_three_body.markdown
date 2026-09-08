---
layout: page
title: A restricted fantasy
eyebrow: NumAlg
permalink: /numalg/three-body-problem/
back_url: /numalg/
back_label: NumAlg
---

Gravitational $N$-body dynamics is a good playground for time integrators: the right-hand side is cheap to evaluate, the exact solution is known in the $N=2$ case (so you can actually measure your error), and the $N=3$ case is chaotic enough to expose any integrator that's secretly cutting corners.

## The two-body problem

Two point masses $m_1, m_2$ interacting under Newtonian gravity reduce, after passing to relative coordinates $\b{r} = \b{r}_2 - \b{r}_1$, to a single second-order ODE for the relative position:

$$
\ddot{\b{r}} = -\frac{G(m_1+m_2)}{\norm{\b{r}}^3}\,\b{r} = -\frac{\mu}{\norm{\b{r}}^3}\,\b{r}.
$$

Written as a first-order system in $\b{y} = (\b{r}, \dot{\b{r}})$, this is the model problem I use to sanity-check every integrator below: it conserves the specific energy $E = \tfrac12\norm{\dot{\b{r}}}^2 - \mu/\norm{\b{r}}$ and angular momentum $\b{L} = \b{r}\times\dot{\b{r}}$ exactly, and its solution is a conic section (an ellipse, for bound orbits), so any secular drift in $E$ or in the orbit's shape is entirely a discretization artifact.

## Time integrators: BDF1&ndash;6 and Crank&ndash;Nicolson

For a generic ODE $\dot{\b y} = f(t, \b y)$, the backward differentiation formulas (BDF$k$) use the last $k$ solution values to build a $k$-th order accurate, implicit multistep method:

$$
\sum_{j=0}^{k} \alpha_j\, \b y_{n+1-j} \;=\; h\,\beta\, f(t_{n+1}, \b y_{n+1}).
$$

| Method | Formula |
|---|---|
| BDF1 (backward Euler) | $y_{n+1} - y_n = h f_{n+1}$ |
| BDF2 | $\tfrac{3}{2}y_{n+1} - 2y_n + \tfrac{1}{2}y_{n-1} = h f_{n+1}$ |
| BDF3 | $\tfrac{11}{6}y_{n+1} - 3y_n + \tfrac{3}{2}y_{n-1} - \tfrac{1}{3}y_{n-2} = h f_{n+1}$ |
| BDF4 | $\tfrac{25}{12}y_{n+1} - 4y_n + 3y_{n-1} - \tfrac{4}{3}y_{n-2} + \tfrac{1}{4}y_{n-3} = h f_{n+1}$ |
| BDF5 | $\tfrac{137}{60}y_{n+1} - 5y_n + 5y_{n-1} - \tfrac{10}{3}y_{n-2} + \tfrac{5}{4}y_{n-3} - \tfrac{1}{5}y_{n-4} = h f_{n+1}$ |
| BDF6 | $\tfrac{49}{20}y_{n+1} - 6y_n + \tfrac{15}{2}y_{n-1} - \tfrac{20}{3}y_{n-2} + \tfrac{15}{4}y_{n-3} - \tfrac{6}{5}y_{n-4} + \tfrac{1}{6}y_{n-5} = h f_{n+1}$ |

Only BDF1 and BDF2 are A-stable (the second Dahlquist barrier rules out A-stability for any linear multistep method beyond order 2); BDF3&ndash;6 are merely $A(\alpha)$-stable, with a shrinking stability wedge as $k$ grows. For an orbit problem this shows up as artificial damping or blow-up of the energy depending on which side of the wedge your step lands on, which makes BDF6 a great way to accidentally spiral a planet into its star.

The other workhorse is the (implicit) trapezoidal rule, usually called Crank&ndash;Nicolson in this context:

$$
y_{n+1} - y_n = \frac{h}{2}\big(f_n + f_{n+1}\big).
$$

It is second order and A-stable, and for a Hamiltonian system like the two-body problem it is *not* symplectic but tends to conserve energy far better than BDF2 in practice over long integrations, at the cost of one implicit solve per step for the same order of accuracy.

## The three-body problem

Adding a third mass removes the reduction to a single-body problem. For $N=3$ point masses:

$$
m_i\,\ddot{\b r}_i = G \sum_{j \neq i} \frac{m_j\,(\b r_j - \b r_i)}{\norm{\b r_j - \b r_i}^3}, \qquad i = 1,2,3.
$$

There is no closed-form solution in general — Poincaré's work on exactly this system is where chaos theory effectively started — but a handful of remarkable exact periodic solutions exist. My favourite is the equal-mass figure-eight choreography (Moore 1993, proved to exist by Chenciner & Montgomery in 2000): three equal masses chase each other around a single figure-eight-shaped curve, forever.

<figure class="figure">
  <img src="{{ "/assets/numalg/three-body-sketch.svg" | relative_url }}" alt="Sketch of the figure-eight three-body orbit, with the three equal masses marked at different phases along the curve">
  <figcaption>The equal-mass figure-eight choreography — a sketch, not simulation output. This is the template pattern for dropping a figure into a page: an <code>&lt;img&gt;</code> pointing at a file under <code>assets/</code>, wrapped in <code>&lt;figure class="figure"&gt;…&lt;figcaption&gt;</code>.</figcaption>
</figure>

## Code

A minimal RK4 integrator is enough to reproduce the figure-eight orbit and is what I use as a reference trajectory before comparing it against the BDF/Crank&ndash;Nicolson family above:

```python
import numpy as np

G = 1.0

def three_body_rhs(t, y, m):
    r = y[:6].reshape(3, 2)
    v = y[6:].reshape(3, 2)
    a = np.zeros_like(r)
    for i in range(3):
        for j in range(3):
            if i == j:
                continue
            diff = r[j] - r[i]
            dist = np.linalg.norm(diff)
            a[i] += G * m[j] * diff / dist**3
    return np.concatenate([v.ravel(), a.ravel()])

def rk4_step(f, t, y, h, *args):
    k1 = f(t, y, *args)
    k2 = f(t + h / 2, y + h / 2 * k1, *args)
    k3 = f(t + h / 2, y + h / 2 * k2, *args)
    k4 = f(t + h, y + h * k3, *args)
    return y + (h / 6) * (k1 + 2 * k2 + 2 * k3 + k4)

# Figure-eight choreography (Chenciner-Montgomery / Simo initial data)
m = np.array([1.0, 1.0, 1.0])
r1 = np.array([0.97000436, -0.24308753])
r2 = -r1
r3 = np.array([0.0, 0.0])
v3 = np.array([-0.93240737, -0.86473146])
v1 = v2 = -v3 / 2

y = np.concatenate([r1, r2, r3, v1, v2, v3])

h, steps = 1e-3, 20_000
trajectory = np.zeros((steps, 6))
for n in range(steps):
    trajectory[n] = y[:6]
    y = rk4_step(three_body_rhs, n * h, y, h, m)
```

Swapping `rk4_step` for a BDF2 predictor&ndash;corrector or a Crank&ndash;Nicolson update (a few Newton iterations per step, since the right-hand side is nonlinear) is the natural next experiment: the figure-eight is a good stress test, because any asymmetry an integrator introduces shows up almost immediately as the three loops drift apart.

<figure class="figure">
  <video src="{{ "/assets/numalg/template-placeholder.mp4" | relative_url }}" poster="{{ "/assets/numalg/template-placeholder-poster.jpg" | relative_url }}" autoplay loop muted playsinline></video>
  <figcaption>Placeholder — this is where a rendered trajectory movie would go; a Game of Life stand-in, not an orbit. This is the template pattern for an embedded clip: an <code>&lt;video&gt;</code> tag with <code>autoplay loop muted playsinline</code> (so it behaves like a silent, self-looping GIF instead of a full player with controls) and a <code>poster</code> frame for the instant before it loads.</figcaption>
</figure>

*This page is a starting draft — code and constants are illustrative and I'll refine them with my actual results.*

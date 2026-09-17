---
layout: page
title: A restricted fiction
eyebrow: Rabbit Holes
permalink: /rabbit-holes/three-body-problem/
back_url: /rabbit-holes/
back_label: Rabbit Holes
---

In 2024, a newly released Netflix series reignited interest in a long-standing problem in classical orbital mechanics. *The Three Body Problem* was an adaptation of the original 2008 sci-fi novel by Liu Cixin. In it, Earth makes contact with an alien civilization with a pretty serious problem: their home planet, Trisolaris, orbits within the triple-star system of Alpha Centauri. Unlike Earth, Trisolaris has no stable, periodic seasons — its climate is subject to violent, deadly swings in weather depending on the positions of its three suns. The Trisolaran civilization, although far more advanced than ours, has yet to find a way to predict how those positions (and therefore the weather) will evolve, and is badly in need of a solution.

Now, why is this problem so hard to solve? That's what this card is about.

My first dip into the research world was about simulating interplanetary satellite orbits — loosely speaking, predicting the path of a physical body in space given the influence of other physical bodies. So, for a little over nine months during my Bachelor's thesis, the Trisolarans and I were scratching our heads about the same kind of dilemma. Luckily, humans have also been chasing this mystery for a few centuries, so we'll start from the basics and try to understand what's going on.

## The one-body problem

Let's consider a standard, washing-machine-sized satellite moving through our Solar System. Given that we're nowhere near an extreme environment (black holes, pulsars, and all that very cool stuff), the fundamental force acting on a body in free fall through empty space is the gravitational pull of other bodies. The foundational work describing the dynamics of gravitationally interacting bodies was laid out by Sir Isaac Newton in the 17th century. He used empirical observations to deduce that the force $$F$$ between two bodies of mass $$m_1$$ and $$m_2$$ is given by

$$
F = G\frac{m_1m_2}{r^2},
$$

where the constant $$G=(6.674\times10^{−11}\ m^3\cdot kg^{−1}\cdot s^{−2})$$ is the as-of-today-accepted *gravitational constant* and $$r$$ is the distance between the two objects. He also authored the laws of motion, from which we know that $$F$$ is the force experienced by *both* masses — it's just that, from the point of view of $$m_1$$, it's directed towards $$m_2$$, and the other way around. In vector form, we could write

$$
\b{F}_{12} = -G\frac{m_1m_2}{\norm{\b{r}_{12}}^3}\b{r}_{12} = G\frac{m_1m_2}{\norm{\b{r}_{21}}^3}\b{r}_{21} = -\b{F}_{21},
$$

where $$\b{r}_{12}=\b{r}_1-\b{r}_2$$ and $$\b{r}_i$$, for $$i=1,2$$, are the position vectors of $$m_i$$ in some reference frame. Note that, as expected, $$\b{F}_{12}+\b{F}_{21}=\b{0}$$. The above formula is commonly referred to as *Newton's law of universal gravitation*.

I question the fact that "one-body problem" is an accepted term. The reason I used it as the title for this section is that the universal law of gravitation holds for the force between two *point masses*, i.e. objects for which all the mass is concentrated in a single point — and that's rarely the case in reality. So what happens for continuous bodies, like our interplanetary washing machine? Newton asked himself the same question when he realized that the Earth and the Moon were orbiting each other as if they were point masses, while clearly they weren't. It took Newton himself (~200 IQ) some twenty years to work out why — inventing infinitesimal calculus along the way — so we won't go into the details here. The loose idea is that any mass distribution generates a *potential field* in space, which is what other objects interact with. The potential can be expressed as 

$$
V(\b{x})=-\int_{\mathbb{R}^3}\frac{G}{\norm{\b{x}-\b{r}}}\rho(\b{r})\mathrm{d}\b{r},
$$

where $$\rho(\b{r})$$ is the mass density distribution and the integral is over the whole space. The gravitational field, and thus the acceleration of a small body in the space around the massive object, is the negative gradient of this gravitational potential $$\b{a} = -\nabla V$$. For those of you keen on partial differential equations (PDEs), the two are related by the following field equation

$$
\Delta V = 4\pi G \rho.
$$

The catch is that adding other masses changes the mass distribution itself — and therefore the potential — so the dynamics of multiple massive objects are intrinsically *coupled*: reason number one why this is hard to predict.

There is some good news, though:
1. The universal law of gravitation still applies well enough if we take $$r$$ to be the distance between each body's *center of mass*, provided $$r$$ is much bigger than the size of the two bodies.
2. We can approximate many celestial bodies in our Solar System as spherical objects whose center of mass coincides with their geometrical center.
3. These approximations are good enough for plenty of real applications, including our meter-sized, multi-ton satellite travelling anywhere from $$10^3$$ to $$10^8$$ kilometers away from other massive objects weighing between $$10^{26}$$ and $$10^{30}$$ kg.


## The two-body problem

It might be tempting to jump straight to adding some number $$N$$ of masses and try to simulate the whole system at once. That's definitely possible numerically, but doing so straight away means losing sight of the fundamental structure underlying gravitational $$N$$-body dynamics. We'll thus take a more pedagogical approach, focusing first on the two-body problem.

Sticking with the two point masses described above we have from Newton's second law that

$$
\begin{aligned}
m_1\b{a}_1 &= -G\frac{m_1m_2}{\norm{\b{r}_{12}}^3}\b{r}_{12} \\
m_2\b{a}_2 &= -G\frac{m_1m_2}{\norm{\b{r}_{21}}^3}\b{r}_{21} = G\frac{m_1m_2}{\norm{\b{r}_{12}}^3}\b{r}_{12}
\end{aligned}
$$

where $$\b{a}_1, \b{a}_2$$ are the two masses' accelerations. Given that $$\b{a}_1=\ddot{\b{r}}_1$$ and $$\b{a}_2=\ddot{\b{r}}_2$$, this is a second-order ordinary differential equation (ODE) system in the variables $$\b{r}_1$$ and $$\b{r}_2$$. A key aspect of the two-body problem is that it can be simplified. By adding the two equations together we get

$$
m_1\ddot{\b{r}}_1 + m_2\ddot{\b{r}}_2 = (m_1+m_2) \ddot{\b{R}}= \b{0},
$$

where we introduced the center of mass of the two particles as $$\b{R} = \frac{m_1\b{r}_1 + m_2\b{r}_2}{m_1+m_2}$$. The center of mass does not accelerate, and will just keep moving with whatever velocity it had at the start! By dividing each equation by its mass and subtracting the two, we instead obtain

$$
\ddot{\b{r}}_1 - \ddot{\b{r}}_2 = \frac{\b{F}_{12}}{m_1}-\frac{\b{F}_{21}}{m_2}=\Bigl(\frac{1}{m_1}+\frac{1}{m_2}\Bigr)\b{F}_{12},
$$

or, equivalently,

$$
\ddot{\b{r}}_{12} = -\Bigl(\frac{1}{m_1}+\frac{1}{m_2}\Bigr)G\frac{m_1m_2}{\norm{\b{r}_{12}}^3}\b{r}_{12}.
$$

The cool thing is that this is now a single, second-order ODE in the variable $$\b{r}_{12}$$ — and that's all I need to solve to simulate the dynamics of two bodies gravitating around each other. More often than not, the equation is rewritten as

$$
\ddot{\b{r}} = \frac{1}{\mu}\b{F}(\b{r}) = -\frac{G(m_1+m_2)}{\norm{\b{r}}^3}\b{r},
$$

where $$\mu = \frac{m_1m_2}{m_1+m_2}$$ is the so-called *reduced mass*. Physically, this says the relative motion $$\b{r}(t)$$ behaves exactly like a single fictitious body of mass $$\mu$$ orbiting a fixed center of mass $$M=m_1+m_2$$ — the whole two-body problem collapses into the one-body problem we already solved above. Once the evolution of $$\b{r}(t)$$ in time is known (that of $$\b{R}(t)$$ is trivially given by the initial conditions), one can reconstruct the orbit of the individual objects as

$$
\begin{aligned}
\b{r}_1(t) &= \b{R}(t)+ \frac{m_2}{m_1+m_2}\b{r}(t) \\
\b{r}_2(t) &= \b{R}(t)- \frac{m_1}{m_1+m_2}\b{r}(t)
\end{aligned}
$$

Two key properties of such a system are:
1. There exists a characteristic total energy of the system, $$E = \tfrac12\norm{\dot{\b{r}}}^2 - \mu/\norm{\b{r}}$$, that remains constant along the evolution.
2. The angular momentum $$\b{L} = \b{r}\times\dot{\b{r}}$$ is conserved too — and it's exactly this conservation that pins the motion to a fixed plane: the plane spanned by the initial relative position and the initial relative velocity.

## Time integrators: forward Euler, backward Euler, and a symplectic scheme

For a generic ODE $$\dot{\b y} = f(t, \b y)$$, the simplest possible numerical schemes are the two flavours of Euler's method. It is convenient, for the sake of this section, to rewrite the second-order equation of motion as a system of first-order equations

$$
\begin{equation}
\ddot{\b{y}} = f(t, \b{y}) \to
\begin{cases}
\dot{\b{y}} = \b{w} \\
\dot{\b{w}} = f(t, \b{y})
\end{cases}.
\end{equation}
$$

Note that the right-hand side of the original equation we are interested in is only dependent on the position. We will test our solvers with a simple, practical example. To keep things easy let's make this toy orbit so that $$\dot{\b{R}}=0$$ and the center of mass remains fixed in a point. Borrowing from what we have seen in the previous section, let's write some code to simulate the trajectory of two unequal point masses.

```python
import numpy as np
from scipy.optimize import fsolve
import matplotlib.pyplot as plt


G = 1
m1 = 2
m2 = 1
m = np.array([m1, m2])

# Initial positions/velocities, picked so the orbit is an exact circle and
# the center of mass starts at rest (see below).
r1 = np.array([1.0, 0])
r2 = np.array([-2.0, 0])
v1 = np.array([0., 1.0/3.0])
v2 = np.array([0., -2.0/3.0])
R0 = (m1*r1 + m2*r2)/(m1+m2)   # center of mass position
dR = (m1*v1 + m2*v2)/(m1+m2)   # center of mass velocity

# We only integrate the reduced problem: r = r1 - r2, v = v1 - v2.
r = r1-r2
v = v1-v2
y = np.concatenate([r, v])

def two_body_rhs(t, y, m):
    # r_ddot = -G(m1+m2) r / |r|^3, the reduced equation of motion.
    r = y[:2]
    v = y[2:]
    a = -G*(m[0] + m[1])*r/np.linalg.norm(r)**3

    return np.concatenate([v, a])

dt = 0.01          # timestep
n_orbits = 3        # how many orbital periods to simulate
dist = np.linalg.norm(r1 - r2)
omega = np.sqrt(G * (m1 + m2) / dist**3)   # angular velocity of the circular orbit
T = 2 * np.pi / omega          # orbital period
n_steps = int(n_orbits * T / dt)
traj1 = np.zeros((n_steps, 2))
traj2 = np.zeros((n_steps, 2))

def plot(traj1, traj2, solvername):
    # Static plot of the full trajectory of both bodies.
    fig1, ax1 = plt.subplots(figsize=(6, 6))
    ax1.plot(traj1[:, 0], traj1[:, 1], label="Body 1", color="tab:blue")
    ax1.scatter(traj1[-1,0], traj1[-1,1], color="blue", marker="o")
    ax1.plot(traj2[:, 0], traj2[:, 1], label="Body 2", color="tab:orange")
    ax1.scatter(traj2[-1,0], traj2[-1,1], color="orange", marker="o")
    ax1.scatter(0, 0, color="black", marker="+", label="Center of mass")
    ax1.set_aspect("equal")
    ax1.set_xlabel("x")
    ax1.set_ylabel("y")
    ax1.set_title("Two-body circular orbit (G=1): " + solvername)
    ax1.legend()
    fig1.savefig(solvername + ".png", dpi=150)

def simulate(y, scheme, solvername):
    for i in range(n_steps):
        y = scheme(two_body_rhs, i * dt, y, dt, m)
        # Undo the reduction: recover each body's position from r(t) and R(t).
        traj1[i] = R0 + i * dt * dR + y[:2]*m[1]/(m[0]+m[1])
        traj2[i] = R0 + i * dt * dR - y[:2]*m[0]/(m[0]+m[1])

    plot(traj1, traj2, solvername)
```

**Forward (explicit) Euler** evaluates the right-hand side at the *current* step:

$$
\b y_{n+1} = \b y_n + h\, f(t_n, \b y_n).
$$

It's first order and trivial to implement — plug in, get the next state, repeat. For an orbit problem, though, it has a very specific failure mode: it systematically pumps energy into the system, so the numerical orbit spirals slowly outward, step after step.

A Python function implementing the Forward Euler scheme looks like this

```python
def forward_euler(f, t, y, h, *args):
    # y_{n+1} = y_n + h f(t_n, y_n)
    k1 = f(t, y, *args)
    return y + h*k1

simulate(y, forward_euler, 'forward_euler')
```

<figure class="figure">
  <img src="{{ "/assets/numalg/two_body_forward_euler.webp" | relative_url }}" alt="Simulation of circular two-body orbit using Forward Euler scheme.">
  <figcaption>Simulation of circular orbit using Forward Euler scheme.</figcaption>
</figure>

**Backward (implicit) Euler** evaluates the right-hand side at the step you're solving *for* instead:

$$
\b y_{n+1} = \b y_n + h\, f(t_{n+1}, \b y_{n+1}),
$$

which means solving a (generally nonlinear) equation for $$\b y_{n+1}$$ at every step. Still only first order, but the error now goes the other way: it over-damps the system, and the orbit spirals inward instead.

A Python function implementing the Backward Euler scheme looks like this

```python
y = np.concatenate([r, v])   # reset to the initial condition

def backward_euler(f, t, y, h, *args):
    # Solve x = y + h f(t, x) for x = y_{n+1} with a nonlinear root-find.
    def func(x):
        return x-y-h*f(t, x, *args)
    return fsolve(func, x0=y)

simulate(y, backward_euler, 'backward_euler')
```

<figure class="figure">
  <img src="{{ "/assets/numalg/two_body_backward_euler.webp" | relative_url }}" alt="Simulation of circular two-body orbit using Backward Euler scheme.">
  <figcaption>Simulation of circular orbit using Backward Euler scheme.</figcaption>
</figure>

Both methods are "correct" in the sense that they converge as $$h\to 0$$, but for a conservative system like an orbit, first-order accuracy was never really the problem — the *systematic* energy drift is. In order to fix it, The idea now is to reorder the explicit Euler update: update $$\b w$$ first using the *old* $$ \b y_n $$, then update $$ \b y_{n+1} $$ using the *new* $$\b w_{n+1}$$:

$$
\b w_{n+1} = \b w_n + h\, f(t, \b y_n), \qquad \b y_{n+1} = \b y_n + h\, \b w_{n+1}.
$$

This is symplectic (or semi-implicit) Euler: still explicit, still only first order pointwise, but it exactly preserves phase-space volume. In practice that means the energy error no longer drifts monotonically in one direction — it oscillates around the true value and stays bounded, so a long-running orbit keeps roughly the right shape instead of slowly spiraling in or out.

A Python function implementing the Semi-implicit Euler scheme looks like this

```python
y = np.concatenate([r, v])   # reset to the initial condition

def semimplicit_euler(f, t, y, h, *args):
    # Update velocity with the OLD position first, then position with the
    # NEW velocity -- that reordering is what makes it symplectic.
    y_fe = y + h*f(t, y, *args)
    n = int(len(y)/2)
    y_new = np.concatenate([y[:n] + h*y_fe[n:], y_fe[n:]])
    return y_new

simulate(y, semimplicit_euler, 'semimplicit_euler')
```

<figure class="figure">
  <img src="{{ "/assets/numalg/two_body_semimplicit_euler.png" | relative_url }}" alt="Simulation of circular two-body orbit using Semi-implicit Euler scheme.">
  <figcaption>Simulation of circular orbit using Semi-implicit Euler scheme.</figcaption>
</figure>

Some remarks:
1. The reason people might still choose Forward Euler is its simplicity. In practice this usually comes with a very small timestep, to keep the energy drift small enough to be useful over the simulation's time horizon — but strictly speaking, smaller steps don't buy *stability* here, only a longer delay before it shows.
2. Choosing Backward Euler guarantees very good stability properties. The computational cost, though, is high compared to Forward Euler, since a nonlinear problem has to be solved at every step. People often use mixed implicit-explicit (IMEX) methods to trade off between Backward and Forward Euler.
3. These schemes are only first order. Of course higher-order schemes exist that achieve more accuracy, such as Backward Differentiation Formula (BDF) methods and Runge-Kutta (RK) methods, among others.
4. It's worth being precise about what "small changes in initial conditions" do here: for *this* two-body problem, nudging the initial condition just gives a smoothly different — but still perfectly regular, still exactly conic-section — orbit. The two-body problem is provably integrable and has no sensitive dependence on initial conditions; nothing chaotic is going on yet.

## The three-body problem

The moment has arrived — we're ready — let's add a third mass to the mix. For $$N=3$$ point masses the system reads:

$$
m_i\,\ddot{\b r}_i = G \sum_{j \neq i} \frac{m_j\,(\b r_j - \b r_i)}{\norm{\b r_j - \b r_i}^3}, \qquad i = 1,2,3.
$$

What can we say analytically about it? Well, the answer is that, as of now, there is no closed-form solution in general. Bruns proved in 1887 that no new algebraic first integrals exist beyond the ten classical ones (energy, momentum, angular momentum, and uniform motion of the center of mass) — the system simply doesn't hand you enough conserved quantities to pin the motion down analytically. Not only this, but Poincaré's work on exactly this system, a few years later, is where *chaos theory* effectively started. As already hinted above, generic initial conditions produce trajectories that are extremely sensitive to how you start them, with no periodicity in sight.

And yet — dial the initial conditions in *just* right, and the very same equations produce something remarkable: an exact, periodic orbit. There's a whole zoo of these; Šuvakov and Dmitrašinović alone catalogued more than a dozen topologically distinct families in 2013. A little hope in the vastness of chaos. The oldest and simplest is Lagrange's 1772 equilateral-triangle solution: place three masses — any masses, not just equal ones — at the corners of an equilateral triangle, and let the whole configuration rotate rigidly about the common center of mass. Let each mass have a fixed angular velocity 

$$
\omega^2 = \frac{G(m_1+m_2+m_3)}{l^3}.
$$

with respect to the center of mass, where $$l$$ is the length of the side of the initial equilateral triangle configuration. Intuitively, this works because the combined pull from the other two masses at each corner always points straight at the system's center of mass, no matter what the individual masses are — so, exactly like a single body on a circular orbit, there's one rotation speed that turns that pull into perfectly circular motion and keeps the triangle rigid forever. Each body then traces out a perfect circle. You can use the same numerical schemes as before to test it.

```python
import numpy as np
from scipy.optimize import fsolve
import matplotlib.pyplot as plt


G = 1
radius = 2       # circumradius: distance from the center to each mass
m1 = 1
m2 = 1.3
m3 = 2.7
m = np.array([m1, m2, m3])

# Three masses at the corners of an equilateral triangle (any masses work).
r1 = np.array([0, radius])
r2 = np.array([-radius*np.sqrt(3)/2, -radius/2])
r3 = np.array([radius*np.sqrt(3)/2, -radius/2])
r0 = np.array([r1, r2, r3, r1]).reshape(4, 2)   # closed loop, just for plotting

R = (m1*r1 + m2*r2 + m3*r3)/(m1+m2+m3)   # center of mass

# omega^2 = G(m1+m2+m3)/l^3, with side length l = radius*sqrt(3).
omega = np.sqrt(G * (m1 + m2 + m3) / (radius*np.sqrt(3))**3)
T = 2 * np.pi / omega          # orbital period

def compute_velocity(r, R, omega):
    # Velocity for uniform circular motion of point r around center R.
    diff = r - R
    direction = np.array([-diff[1], diff[0]])  # Perpendicular to the radius vector
    direction = direction / np.linalg.norm(direction)  # Normalize
    return omega * direction * np.linalg.norm(diff)
v1 = compute_velocity(r1, R, omega)
v2 = compute_velocity(r2, R, omega)
v3 = compute_velocity(r3, R, omega)

y = np.concatenate([r1, r2, r3, v1, v2, v3])

def three_body_rhs(t, y, m):
    # Newton's law of gravitation, summed pairwise over all three bodies.
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

dt = 0.01          # timestep
n_orbits = 3        # how many orbital periods to simulate

n_steps = int(n_orbits * T / dt)
traj1 = np.zeros((n_steps, 2))
traj2 = np.zeros((n_steps, 2))
traj3 = np.zeros((n_steps, 2))

def plot(traj1, traj2, traj3, solvername):
    # Static plot of the full trajectory of all three bodies.
    fig1, ax1 = plt.subplots(figsize=(6, 6))
    ax1.plot(r0[:, 0], r0[:, 1], label="Initial configuration", color="grey")
    ax1.plot(traj1[:, 0], traj1[:, 1], label="Body 1", color="tab:blue")
    ax1.scatter(traj1[-1,0], traj1[-1,1], color="blue", marker="o")
    ax1.plot(traj2[:, 0], traj2[:, 1], label="Body 2", color="tab:orange")
    ax1.scatter(traj2[-1,0], traj2[-1,1], color="orange", marker="o")
    ax1.plot(traj3[:, 0], traj3[:, 1], label="Body 3", color="tab:green")
    ax1.scatter(traj3[-1,0], traj3[-1,1], color="green", marker="o")
    ax1.set_aspect("equal")
    ax1.set_xlabel("x")
    ax1.set_ylabel("y")
    ax1.set_title("Three-body circular orbit (G=1): " + solvername)
    ax1.legend()
    fig1.savefig('three_body_' + solvername + ".png", dpi=150)

def simulate(y, scheme, solvername):
    for i in range(n_steps):
        y = scheme(three_body_rhs, i * dt, y, dt, m)
        traj1[i] = y[:2]
        traj2[i] = y[2:4]
        traj3[i] = y[4:6]

    plot(traj1, traj2, traj3, solvername)
```

Here are the results for the Semi-implicit scheme

<!-- <figure class="figure">
  <img src="{{ "/assets/numalg/three_body_forward_euler.webp" | relative_url }}" alt="Simulation of circular three-body orbit using Forward Euler scheme.">
  <figcaption>Simulation of circular orbit using Forward Euler scheme.</figcaption>
</figure>
<figure class="figure">
  <img src="{{ "/assets/numalg/three_body_Backward_euler.png" | relative_url }}" alt="Simulation of circular three-body orbit using Backward Euler scheme.">
  <figcaption>Simulation of circular orbit using Backward Euler scheme.</figcaption>
</figure> -->
<figure class="figure">
  <img src="{{ "/assets/numalg/three_body_semimplicit_euler.png" | relative_url }}" alt="Simulation of circular three-body orbit using Semi-implicit Euler scheme.">
  <figcaption>Simulation of circular orbit using Semi-implicit Euler scheme.</figcaption>
</figure>

Another one is the equal-mass figure-eight choreography (Moore 1993, proved to exist by Chenciner & Montgomery in 2000): three equal masses chase each other around a single figure-eight-shaped curve.

```python
# Figure-eight initial conditions (Chenciner-Montgomery / Simo).
m = np.array([1.0, 1.0, 1.0])
r1 = np.array([0.97000436, -0.24308753])
r2 = -r1
r3 = np.array([0.0, 0.0])
v3 = np.array([-0.93240737, -0.86473146])
v1 = v2 = -v3 / 2
r0 = np.array([r1, r2, r3, r1]).reshape(4, 2)
```

<!-- <figure class="figure">
  <img src="{{ "/assets/numalg/three_body_forward_euler_1.webp" | relative_url }}" alt="Simulation of figure eight three-body orbit using Forward Euler scheme.">
  <figcaption>Simulation of figure eight orbit using Forward Euler scheme.</figcaption>
</figure>
<figure class="figure">
  <img src="{{ "/assets/numalg/three_body_Backward_euler_1.png" | relative_url }}" alt="Simulation of figure eight three-body orbit using Backward Euler scheme.">
  <figcaption>Simulation of figure eight orbit using Backward Euler scheme.</figcaption>
</figure> -->
<figure class="figure">
  <img src="{{ "/assets/numalg/three_body_semimplicit_euler_1.png" | relative_url }}" alt="Simulation of figure eight three-body orbit using Semi-implicit Euler scheme.">
  <figcaption>Simulation of figure eight orbit using Semi-implicit Euler scheme.</figcaption>
</figure>

Both of these are measure-zero needles in a very large, very chaotic haystack: take the initial conditions of either of them and nudge a single coordinate by one part in a million, and by the time you've integrated a few periods the three loops no longer close. That sensitivity, more than the missing closed-form solution, is the real reason this problem is hard.

<figure class="figure">
  <video src="{{ "/assets/numalg/figure_eight_forward.mp4" | relative_url }}" poster="{{ "/assets/numalg/figure_eight_0.png" | relative_url }}" autoplay loop muted playsinline></video>
  <figcaption>Figure eight simulation using Forward Euler scheme. Initial masses positions are in grey</figcaption>
</figure>

<figure class="figure">
  <video src="{{ "/assets/numalg/figure_eight_semimplicit.mp4" | relative_url }}" poster="{{ "/assets/numalg/figure_eight_0.png" | relative_url }}" autoplay loop muted playsinline></video>
  <figcaption>Figure eight simulation using Forward Euler scheme. Initial masses positions are in grey</figcaption>
</figure>

### Is this all?

Not quite, we can push a little more. There exist a genuinely tractable special case: make one of the three bodies so light that it doesn't perturb the other two at all, while it's still fully pushed around by them. The two heavy bodies (the "primaries") then just solve an ordinary two-body problem between themselves — take that orbit circular, for simplicity, and you get the *circular restricted three-body problem* (CR3BP), a staple of spacecraft trajectory design.

The trick that makes it tractable is to stop watching from a fixed frame and instead switch to one that co-rotates with the two primaries, so they appear frozen in place. Normalizing units so that the total mass, the separation, and the orbital angular velocity are all $$1$$, and writing $$\mu = m_2/(m_1+m_2)$$ for the mass ratio, the primaries sit at $$(-\mu, 0)$$ and $$(1-\mu, 0)$$, and the massless third body at $$(x,y)$$ obeys

$$
\ddot x - 2\dot y = \frac{\partial \Omega}{\partial x}, \qquad \ddot y + 2\dot x = \frac{\partial \Omega}{\partial y},
$$

with the effective potential

$$
\Omega(x,y) = \frac{x^2+y^2}{2} + \frac{1-\mu}{r_1} + \frac{\mu}{r_2},
$$

$$r_1, r_2$$ being the distances to the two primaries. The extra $$\dot x, \dot y$$ terms are the Coriolis force; the $$(x^2+y^2)/2$$ term inside $$\Omega$$ is the centrifugal contribution. Because this rotating-frame system has no explicit time dependence, it buys back exactly one conserved quantity that the general three-body problem doesn't have: the *Jacobi integral*,

$$
C_J = 2\Omega(x,y) - (\dot x^2 + \dot y^2),
$$

constant along every trajectory. It's the closest thing this problem has to an energy, and a good numerical sanity check — if $$C_J$$ drifts during a simulation, the integrator is the problem, not the physics.

Setting $$\nabla \Omega = \b 0$$ gives the five Lagrange points: three collinear ones, $$L_1, L_2, L_3$$, that only exist as roots of a quintic with no closed form, and two — $$L_4$$ and $$L_5$$, at $$(0.5-\mu, \pm\sqrt3/2)$$ — that don't need solving anything, because they're exactly the equilateral-triangle configuration from Lagrange's 1772 solution above, just sitting still in the rotating frame instead of spinning in the inertial one.

As a concrete example, here's a small body released near $$L_4$$ in the Earth&ndash;Moon system ($$\mu\approx0.0122$$), with a tiny velocity kick so it doesn't sit exactly at the equilibrium:

```python
import numpy as np
from scipy.optimize import fsolve
import matplotlib.pyplot as plt


mu = 0.0122   # mass ratio m2/(m1+m2) -- roughly the Earth-Moon system

# L4, nudged with a small extra velocity
x4, y4 = 0.5 - mu, np.sqrt(3) / 2
y = np.array([x4, y4, -0.01, 0.01])

def omega_grad(x, y):
    # Gradient of the effective potential Omega(x, y).
    r1 = np.hypot(x + mu, y)
    r2 = np.hypot(x - 1 + mu, y)
    dOdx = x - (1 - mu) * (x + mu) / r1**3 - mu * (x - 1 + mu) / r2**3
    dOdy = y - (1 - mu) * y / r1**3 - mu * y / r2**3
    return dOdx, dOdy

def cr3bp_rhs(t, y):
    # CR3BP equations of motion, including the Coriolis terms.
    x, y, vx, vy = y
    dOdx, dOdy = omega_grad(x, y)
    ax = 2 * vy + dOdx
    ay = -2 * vx + dOdy
    return np.array([vx, vy, ax, ay])

dt = 0.001          # timestep
n_steps = 40000     # number of steps
T = dt*n_steps
traj1 = np.zeros((n_steps, 2))
CJ = np.zeros((n_steps, 3))

def plot(traj1, solvername):
    # Static plot of the trajectory, with both primaries marked.
    fig1, ax1 = plt.subplots(figsize=(6, 6))
    ax1.scatter(-mu, 0, color="orange", marker="o", label = "Primary 1")
    ax1.scatter(1-mu, 0, color="orange", marker="o", label = "Primary 2")
    ax1.plot(traj1[:, 0], traj1[:, 1], label="Body 1", color="tab:blue")
    ax1.scatter(traj1[-1,0], traj1[-1,1], color="blue", marker="o")
    ax1.set_aspect("equal")
    ax1.set_xlabel("x")
    ax1.set_ylabel("y")
    ax1.set_title("Circular restricted three-body problem (G=1): " + solvername)
    ax1.legend()
    fig1.savefig('cr3bp_' + solvername + ".png", dpi=150)

def forward_euler(f, t, y, h, *args):
    k1 = f(t, y, *args)
    return y + h*k1

def backward_euler(f, t, y, h, *args):
    def func(x):
        return x-y-h*f(t, x, *args)
    return fsolve(func, x0=y)

def semimplicit_euler(f, t, y, h, *args):
    y_fe = y + h*f(t, y, *args)
    n = int(len(y)/2)
    y_new = np.concatenate([y[:n] + h*y_fe[n:], y_fe[n:]])
    return y_new

def compute_CJ(y):
    # Jacobi integral C_J = 2*Omega - (vx^2 + vy^2); should stay ~constant.
    part1 = (y[2]**2 + y[3]**2)
    r1 = np.linalg.norm(y[:2] - np.array([-mu, 0]))
    r2 = np.linalg.norm(y[:2] - np.array([1-mu, 0]))
    part2 = 2*((y[0]**2 + y[1]**2)/2+(1-mu)/r1 +mu/r2)
    return part2 - part1

y0 = np.array([x4, y4, -0.01, 0.01])

# Run all three schemes from the same initial condition, so they're
# actually comparable, and track the Jacobi integral along each run.
y = y0.copy()
for i in range(n_steps):
    traj1[i] = y[:2]
    y = forward_euler(cr3bp_rhs, i * dt, y, dt)
    CJ[i, 0] = compute_CJ(y)
plot(traj1, 'forward_euler')

y = y0.copy()
for i in range(n_steps):
    traj1[i] = y[:2]
    y = backward_euler(cr3bp_rhs, i * dt, y, dt)
    CJ[i, 1] = compute_CJ(y)
plot(traj1, 'backward_euler')

y = y0.copy()
for i in range(n_steps):
    traj1[i] = y[:2]
    y = semimplicit_euler(cr3bp_rhs, i * dt, y, dt)
    CJ[i, 2] = compute_CJ(y)
plot(traj1, 'semimplicit_euler')

fig1, ax1 = plt.subplots(figsize=(6, 6))
ax1.plot(CJ[:,0], label="Forward Euler", color="blue")
ax1.plot(CJ[:,1], label="Backward Euler", color="orange")
ax1.plot(CJ[:,2], label="Semi-implicit Euler", color="green")
ax1.ticklabel_format(style='scientific', axis='y', scilimits=(0,0))
ax1.set_xlabel("time")
ax1.set_title("Jacobi integral evolution")
ax1.legend()
fig1.savefig("CJ.png", dpi=150)
```

Rather than drifting away, the body slowly loops around $$L_4$$ in a "tadpole" orbit. This is the special thing about $$L_4$$ and $$L_5$$: for realistic mass ratios they're *stable* equilibria, unlike $$L_1$$, $$L_2$$, $$L_3$$. Nudge a body near one of them and the Coriolis term doesn't let it fall away — instead it curls the motion into a slow loop, the same mechanism that keeps Jupiter's Trojan asteroids librating around its own $$L_4$$ and $$L_5$$ points, far ahead of and behind the planet along its orbit.

<figure class="figure">
  <img src="{{ "/assets/numalg/cr3bp_semimplicit_euler.png" | relative_url }}" alt="CR3BP simulation of motion around L4 Semi-implicit Euler scheme.">
  <figcaption>CR3BP simulation of motion around L4 Semi-implicit Euler scheme.</figcaption>
</figure>
<figure class="figure">
  <img src="{{ "/assets/numalg/CJ.webp" | relative_url }}" alt="Evolution of the Jacobi integral with different schemes.">
  <figcaption>Evolution of the Jacobi integral with different schemes.</figcaption>
</figure>

### Is this all all?

Not quite — we can also lean on numerical simulations directly. Once we're confident we have a good numerical scheme for a chaotic problem, numerical simulations let us launch a large number of runs and map out the *phase space* of the solution. This is one of the techniques used by modern orbit design, where precision is key: in a chaotic system, an error of a few millimeters in the initial orbit can amplify into an error of thousands of kilometers in the final orbit, and space engineers cannot afford that, especially with a human crew on board. Numerical simulations have provided a reliable way of planning, predicting, and correcting spacecraft orbits — and that has led to real, practical improvements in how we explore the solar system.

## Final takeaways

1. Given a certain problem, it is crucial to derive what we can analytically, especially conserved quantities. This can immensely simplify comprehension of the problem and point the way towards good numerical solvers. It also provides simplified examples with known, exact solutions that can function as fast test-beds during algorithm development.
2. Numerical methods have to take into account the structure of the underlying problem in order to provide an efficient and reliable solution. This not only greatly improves the stability of the overall algorithm, but also provides a constant check that the solution stays within the space of physically feasible configurations.
3. Computation is one of the pillars of science that, with precise accuracy and convergence properties, can fill the gap where other approaches can't reach.

<!-- <figure class="figure">
  <video src="{{ "/assets/numalg/template-placeholder.mp4" | relative_url }}" poster="{{ "/assets/numalg/template-placeholder-poster.jpg" | relative_url }}" autoplay loop muted playsinline></video>
  <figcaption>Placeholder — this is where a rendered trajectory movie would go; a Game of Life stand-in, not an orbit. This is the template pattern for an embedded clip: an <code>&lt;video&gt;</code> tag with <code>autoplay loop muted playsinline</code> (so it behaves like a silent, self-looping GIF instead of a full player with controls) and a <code>poster</code> frame for the instant before it loads.</figcaption>
</figure> -->

*This page is a starting draft.*

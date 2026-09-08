---
layout: page
title: The sound of spacetime
eyebrow: NumAlg
permalink: /numalg/gravitational-waves/
back_url: /numalg/
back_label: NumAlg
---

Numerical relativity was the topic that first got me hooked on the idea that you could *simulate* general relativity the same way you simulate fluids: discretize a PDE, march it forward in time, and watch physics come out the other end. My starting point was Baumgarte & Shapiro's *Numerical Relativity: Starting from Scratch*, which builds the whole machinery up from a 1+1 toy problem before tackling real binary inspirals — I'm following roughly the same path here.

## From Einstein's equations to a time-evolution problem

The Einstein field equations, $G_{\mu\nu} = 8\pi T_{\mu\nu}$, are not, on their face, an evolution problem: there is no built-in notion of "time" to march forward in. The 3+1 (ADM) formalism fixes this by slicing spacetime into a stack of spatial hypersurfaces $\Sigma_t$, each carrying a spatial metric $\gamma_{ij}$ and extrinsic curvature $K_{ij}$, connected by a lapse function $\alpha$ and shift vector $\beta^i$. Evolving $(\gamma_{ij}, K_{ij})$ forward in $t$ then really is an initial-value problem, of the same flavour as any other system of PDEs — just with a much less forgiving stability landscape. In practice nobody evolves the raw ADM equations; the standard choice (and the one I've worked with) is the BSSN reformulation, which conformally rescales the metric and promotes certain derivatives of the connection coefficients to independent evolved variables specifically to tame the numerical instabilities that plague ADM in strongly curved, dynamical spacetimes like a black-hole binary.

## The chirp

The observable I actually care about is the gravitational-wave strain $h(t)$ radiated by two compact objects spiralling into each other. Full numerical relativity is needed to get the merger and ringdown right, but the *inspiral* — while the two bodies are still well separated — is well described analytically by the leading-order post-Newtonian quadrupole formula, which is enough to build a toy version of the signature "chirp": a waveform that sweeps up in both frequency and amplitude as the binary loses energy to radiation and spirals inward. Writing $\mathcal{M}_c = (m_1 m_2)^{3/5}(m_1+m_2)^{-1/5}$ for the chirp mass, the time-to-coalescence at a given instantaneous frequency $f$ is

$$
\tau(f) = \frac{5}{256}\,\frac{c^5}{G^{5/3}(\pi f)^{8/3}\,\mathcal{M}_c^{5/3}},
$$

and inverting this relation gives the frequency sweep $f(t) \propto (\tau_0 - t)^{-3/8}$, with the strain amplitude growing roughly as $f^{2/3}$ right up until the post-Newtonian approximation breaks down near merger — exactly where a full numerical solve of the BSSN equations takes over.

<figure class="figure">
  <img src="{{ "/assets/numalg/chirp-sketch.svg" | relative_url }}" alt="Sketch of a gravitational-wave chirp waveform, sweeping up in frequency and amplitude">
  <figcaption>The characteristic "chirp": frequency and amplitude both climb as coalescence approaches. Sketch, not real strain data.</figcaption>
</figure>

## Code: a toy chirp

```python
import numpy as np

G, c, Msun = 6.674e-11, 2.998e8, 1.989e30

def chirp_mass(m1_msun, m2_msun):
    return (m1_msun * m2_msun) ** 0.6 / (m1_msun + m2_msun) ** 0.2

def leading_order_chirp(m1_msun, m2_msun, f0, n_samples=200_000):
    """Leading-order (Newtonian quadrupole) inspiral waveform.

    Valid only while the binary is well separated; a real inspiral-merger-
    ringdown waveform needs a full BSSN evolution near coalescence.
    """
    Mc = chirp_mass(m1_msun, m2_msun) * Msun
    tau = 5 / 256 * c**5 / (G ** (5 / 3) * (np.pi * f0) ** (8 / 3) * Mc ** (5 / 3))

    t = np.linspace(0, 0.999 * tau, n_samples)
    f = f0 * (1 - t / tau) ** (-3 / 8)                 # frequency sweep: the "chirp"
    phase = 2 * np.pi * np.cumsum(f) * (t[1] - t[0])
    strain = f ** (2 / 3) * np.cos(phase)               # amplitude grows with frequency

    return t, f, strain

t, f, h = leading_order_chirp(m1_msun=30, m2_msun=25, f0=20.0)
```

The next step on my list is to replace this leading-order toy model with an actual BSSN evolution of a head-on or inspiralling black-hole pair on a finite-difference or finite-element grid, and to compare the extracted waveform against this analytic estimate to see exactly where the post-Newtonian approximation stops being trustworthy.

*This page is a starting draft — the physics is right in spirit, but I'll swap in my own numbers and plots once the simulation is running.*

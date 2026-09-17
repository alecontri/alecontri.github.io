---
layout: page
title: A realistic conjecture?
eyebrow: Rabbit Holes
permalink: /rabbit-holes/willmore-flow/
back_url: /rabbit-holes/
back_label: Rabbit Holes
---

I want to talk here about what is part of my PhD thesis: numerical methods for cellular dynamics endowed with an evolving, possibly deformable interface. All the details of our latest work can be found in the following preprint

> A. Contri, E. A. Francis, A. Massing, P. Rangamani. *Mechanochemical Feedback between Cell Shape and Intracellular Mechanics Revealed by a Finite-Element Framework.* bioRxiv, 2026. [Link]({{ "https://www.biorxiv.org/content/10.64898/2026.07.03.736361v1" }})

and will be available at the GitHub page below, where you can also find documentation and some tutorials to simulate this and other phenomena

> TBA

## Why cell shape is a mechanics problem

Cells constantly reshape themselves — crawling, engulfing particles, budding off vesicles, growing dendritic spines, even condensing droplets of protein against the inside of their own membrane — and underneath all of that reshaping is, quite literally, a mechanics problem. Three things talk to each other in a loop: the extracellular environment (a source of chemical and mechanical signals), the plasma membrane (the thin bilayer separating inside from outside), and the cytoskeleton just beneath it, which reorganizes in response and pushes back on the membrane in turn. Close that loop and, over and over across biology, you get shape change: a neutrophil chasing down a pathogen, a synapse strengthening by growing a mushroom-shaped spine, a vesicle budding off to ferry cargo somewhere else. It's a genuinely rich landscape — see the reviews by Argudo et al. (2016) and Rangamani (2022) for a much fuller picture than I can give here.

<div class="figure-row">
  <figure class="figure">
    <img src="{{ "/assets/numalg/phagocytosis.jpeg" | relative_url }}" alt="Time-lapse microscopy of a neutrophil engulfing a bead during phagocytosis, from first contact to complete engulfment">
    <figcaption>A neutrophil engulfing a bead, from first contact to complete engulfment. Adapted from Boero et al. (2023), CC BY 4.0.</figcaption>
  </figure>

  <figure class="figure">
    <img src="{{ "/assets/numalg/droplet_wetting_1.jpg" | relative_url }}" alt="Confocal microscopy of a biomolecular condensate wetting the inside of a lipid membrane, shown in separate condensate, membrane, and merged channels">
    <figcaption>A biomolecular condensate (cyan) wetting a membrane (magenta) — the droplet reshapes the membrane it sits against. Adapted from Mangiarotti et al. (2023), CC BY 4.0.</figcaption>
  </figure>
</div>

The membrane itself has a bit of a split personality, and it's worth being precise about which half of it this card is about. Laterally, the lipids making it up can slide past each other freely, so *within* the surface the membrane behaves like a two-dimensional fluid. But bending the surface *out of that plane* costs energy — the bilayer resists curvature much more than it resists sliding, the way a sheet of paper folds reluctantly but slides across a table with no resistance at all. On the timescales I care about, that second, elastic side of the story usually dominates the fluid one, and that's what the rest of this card is about: not how the membrane flows, but how it bends.

<figure class="figure">
  <img src="{{ "/assets/numalg/fluid_deformable.webp" | relative_url }}" alt="Schematics of how fluid-deformable membranes behave.">
  <figcaption>Left: Undeformed initial configuration. Center-Left: Membrane bends out-of-plane but in-plane phospholipid ordering remains unaltered. Center-Right: Membrane flows in-plane leaving the shape of the domain unaltered, but redistributing the position of the phospholipids. Right: Membrane both flows in-plane and bends out-of-plane.</figcaption>
</figure>

## A primer on curvature

For the sake of simulations, the thickness of the membrane can be considered negligibly thin compared to the cellular volumetric compartments we are interested in solving for. More often than not then, the membrane itself is approximated as a surface dividing intra- and extra-cellular compartments. The geometry of surfaces and their evolution is a complex and elaborate topic, but in what follows we can present, in a very simplified way, the core concepts that play a role here.

At every point of a surface there's a direction "straight out" — the normal vector $$\b{n}$$. Walk along the surface and watch how that normal tips over as you go: this rate of tipping is captured by an operator called the *Weingarten map* (or *shape operator*) $$\b{W}=-\nabla_{\Gamma}\b{n} $$, where $$\nabla_\Gamma$$ is the surface gradient. Imagine the Weingarten map as a matrix that "lives" on the surface; this matrix is characterized by some important properties, like being symmetric and nullifying every normal vector you apply it to. Being a symmetric matrix, $$\b{W}$$ has, for a 2D surface in 3D, two real eigenvalues, and it's their invariants we actually care about. The eigenvalues are called the *principal curvatures*, $$\kappa_1$$ and $$\kappa_2$$. Two crucial combinations of the latter show up everywhere in what follows:

- the **mean curvature** $$\kappa=\kappa_1+\kappa_2$$, roughly how much the surface bulges outward on average at that point (zero for a flat plane, the same sign everywhere on a sphere);
- the **Gaussian curvature** $$K=\kappa_1\kappa_2$$, which instead measures the *type* of bend — positive for a dome (both principal curvatures agree in sign, like the top of a ball), negative for a saddle (they disagree, like a Pringle chip), and famously an *intrinsic* property of the surface: you can compute $$K$$ using only distances measured within the surface, without ever looking at how it sits in space (Gauss's *Theorema Egregium*). A neat consequence, the Gauss&ndash;Bonnet theorem, says that $$\int_\Gamma K\,\mathrm dA=2\pi\chi(\Gamma)$$ depends only on the surface's topology $$\chi$$ — bend a sphere however you like, dent it, squash it, pinch it, and the total Gaussian curvature never changes.

<!-- <figure class="figure">
  <img src="{{ "/assets/numalg/curvature-sketch.svg" | relative_url }}" alt="A bumpy curve with normal vectors at several points, and at the sharpest bend a dashed circle showing the osculating circle whose radius sets the local curvature">
  <figcaption>The tighter the bend, the smaller the circle that hugs it, and the larger the curvature — curvature is qualitatively 1 / (radius of that circle).</figcaption>
</figure> -->

## From general shells to a simple membrane

Curvature elasticity for a thin sheet doesn't have to start from a membrane at all — it's a special, simplified case of a much older subject: the theory of thin elastic shells. The richest version, a *Cosserat surface*, tracks a deformable surface together with an independent, deformable *director* vector attached to every point — six degrees of freedom in total in 3D, since the surface's position and the director's orientation and length are all free to vary on their own. Constrain the director to keep a fixed length, so it can still tilt but no longer stretch, and you get a *Naghdi shell*: five degrees of freedom, with the director still free to swing away from the surface normal, capturing genuine transverse shear.

Take one more step and lock the director exactly onto the surface's own normal vector — no independent tilting left at all — and you land on a *Kirchhoff&ndash;Love shell*: three degrees of freedom, with bending now measured purely by how the second fundamental form (the normal's own rate of tipping, from the curvature primer above) changes across the surface. That single constraint quietly turns what was a second-order problem into a fourth-order one in the surface position — the same jump in difficulty that makes Willmore flow harder than mean curvature flow later on, and for exactly the same geometric reason.

<figure class="figure">
  <img src="{{ "/assets/numalg/ElasticToCanham.webp" | relative_url }}" alt="Four panels showing a membrane cross-section with a director vector, progressively constrained from fully free (Cosserat) to fixed length (Naghdi) to locked onto the normal (Kirchhoff-Love) to absent entirely, leaving bending only (Canham-Helfrich)">
  <figcaption>Each step removes degrees of freedom from the director and the surface deformability, until only the bare surface and its bending are left.</figcaption>
</figure>

The Canham&ndash;Helfrich membrane described next is one further simplification down from there: assume the in-plane fluidity of the bilayer is *rotationally symmetric*, which amounts to a vanishing shear modulus and zero in-plane stretch. Drop those and you're left with an energy that can only depend on the second fundamental form — which, for a 2D surface in 3D, means it can only depend on $$\kappa$$ and $$K$$.

## The Canham&ndash;Helfrich energy

Canham (1970) first modeled the biconcave shape of red blood cells as the shape that *minimizes* a simple energy built purely from mean curvature. Helfrich (1973) generalized it shortly after, arguing from basic physics that — once you neglect in-plane stretching, which the fluid bilayer barely resists anyway — bending really is all that's left; famously, he reasoned his way from "curvature should be negligible in the swelling of vesicles, apart from special cases" to "it seems permissible to entirely neglect tilt and stretching" once a vesicle's volume drops below a critical threshold.

<!-- <figure class="figure">
  <img src="{{ "/assets/numalg/canham_1.webp" | relative_url }}" alt="Schematic of a lipid bilayer as two coupled surfaces roughly 100 angstroms apart, showing how bending the bilayer stretches one surface and compresses the other, and how in-plane forces stretch or shear the surface">
  <figcaption>The bilayer as a thin elastic sheet: bending it apart stretches one face and compresses the other (top), while separately it can be stretched or sheared in-plane (bottom). Adapted from Canham (1970), with permission from Elsevier.</figcaption>
</figure> -->

The resulting energy, still the standard model in quantitative membrane biophysics today, is

$$
\mathcal E_H(\Gamma) = \int_\Gamma \Bigl[\tfrac{\gamma_W}{2}(\kappa-\bar\kappa)^2 + \gamma_G K\Bigr]\,\mathrm dA + \gamma_t|\Gamma|,
$$

where $$\gamma_W$$ is the bending rigidity, $$\bar\kappa$$ is a *spontaneous curvature* (a preferred bend, coming e.g. from an asymmetry between the bilayer's two leaflets), $$\gamma_G$$ is a Gaussian-curvature modulus, and $$\gamma_t$$ is a membrane tension. Since Gauss&ndash;Bonnet makes the $$\gamma_G K$$ term a fixed topological constant for a closed surface, it is often ignored in the dynamics and from here on too.

This energy is more than a pretty formula — it's genuinely predictive. Seifert, Berndl and Lipowsky (1991) mapped out its full phase diagram of equilibrium vesicle shapes as a function of reduced volume and spontaneous curvature, and found that minimizing $$\mathcal E_H$$ reproduces the entire observed zoo of red blood cell shapes — prolate, oblate, stomatocyte, pear-shaped, budded — as those parameters are dialed. Deuling and Helfrich (1976) confirmed this quantitatively against real, osmotically deflated cells: essentially the whole family of observed axisymmetric shapes falls out of numerically minimizing one energy.

<!-- <figure class="figure">
  <img src="{{ "/assets/numalg/canham_2.webp" | relative_url }}" alt="Photographs of red blood cells at successive stages of osmotic swelling, each paired with the outline predicted by minimizing the Canham-Helfrich energy at the matching reduced volume">
  <figcaption>Real red blood cell shapes (left of each pair) at successive stages of osmotic swelling, next to the outline that minimizing the energy above predicts at the matching volume (right). Adapted from Canham (1970), with permission from Elsevier.</figcaption>
</figure> -->

Set $$\bar\kappa=\gamma_G=\gamma_t=0$$ and $$\mathcal E_H$$ collapses to the *Willmore energy*, $$\mathcal E_W(\Gamma)=\tfrac{\gamma_W}{2}\int_\Gamma \kappa^2\,\mathrm dA$$. It's long been known that, among *all* closed surfaces regardless of topology, this is minimized by the round sphere. An open question set in the 1960s was what minimizes it once you fix the surface to be a torus instead, which turned out to be much harder. This question took the name of *Willmore conjecture* and had repercussions in many mathematical fields dealing with manifolds. The conjecture was finally settled in 2012 by Marques and Neves: the surprising answer is the Clifford torus, a very particular, highly symmetric torus that lives naturally in the 3-sphere rather than in flat space.

## Gradient flows

Given any energy defined on the space of surfaces, there's a canonical way to let a surface relax towards a minimizer: move each point in the normal direction, at whatever (signed) rate $$v^\perp$$ decreases the energy fastest. We talk about normal deformations since tangential deformations do not modify the shape of the object, and, given the energy only depends on the shape, a tangential motion would not modify the energy at all.

Formally, one tries to write the first variation of the energy as a linear functional of that normal velocity: $$\delta\mathcal E(\Gamma(t))=\langle \mathcal E'(\Gamma(t)), v^\perp\rangle$$. If such a functional exists, the choice $$v^\perp=-\mathcal E'(\Gamma(t))$$ turns this into $$\delta\mathcal E=-\langle v^\perp,v^\perp\rangle\le0$$ — a built-in guarantee that the energy can only go down as the surface evolves. That's an $$L^2$$-gradient flow, and it's the canonical dissipative dynamics for a system where viscous drag dominates inertia — which, at the length and force scales of a cell membrane, it very much does.

Two special cases of this recipe are worth naming. Keep only the area term ($$\gamma_W=\gamma_G=0$$) and you get *mean curvature flow*, $$v^\perp=\gamma_t\kappa$$: an ordinary second-order geometric PDE, well understood, with well-documented finite-time singularities (neck-pinching, collapse), and a natural stepping stone before tackling anything harder. Keep the bending term instead ($$\gamma_t=\gamma_G=0$$) and you get *Helfrich flow* (Willmore flow, when additionally $$\bar\kappa=0$$):

$$
v^\perp = \gamma_W\Bigl(-\Delta_\Gamma(\kappa-\bar\kappa) - (\kappa-\bar\kappa)\norm{\b W}^2 + \tfrac12(\kappa-\bar\kappa)^2\kappa\Bigr).
$$

Because curvature already involves two derivatives of the surface's position, this flow is not only nonlinear but also fourth order in the position — a genuinely harder beast than mean curvature flow, both to analyze and to discretize. In practice the two are often combined and constrained (fixed area, fixed enclosed volume) to model a real vesicle relaxing towards one of the equilibrium shapes from the phase diagram above.

## Numerics: the BGN trick

The obvious obstacle to discretizing a fourth-order geometric PDE directly is that you'd need to construct finite elements on a surface, which can get quite tricky, especially if one needs continuous *derivatives* across mesh edges. Early approaches sidestepped the issue altogether: level-set and phase-field methods (surveyed by Deckelnick, Dziuk and Elliott, 2005) embed the evolving surface implicitly in a fixed background grid, avoiding explicit mesh management at the cost of solving over the whole ambient volume and picking up extra geometric consistency errors along the way.

Barrett, Garcke and Nürnberg found a more direct route in 2007: a genuinely *parametric* method — the surface's own position is the unknown being solved for, unlike the level-set/phase-field surfaces above — that still needs no explicit chart or global parametrization of the surface, working directly on the triangulated mesh instead. The trick: introduce the mean curvature vector $$\b\kappa=\kappa\b n$$ as an extra unknown alongside the surface position itself, and use the identity $$\kappa\b n = \Delta_\Gamma\,\b{Id}$$ to turn one fourth-order equation into two coupled second-order ones — a *mixed formulation*. Both unknowns can then live in the simplest possible (piecewise-linear) finite element space, no exotic elements required. A nice side effect: the very same equation that recovers the curvature also happens to nudge the mesh nodes tangentially into a well-spread-out configuration, essentially for free — which matters enormously in practice, since curvature flows are notorious for silently wrecking mesh quality until a simulation quietly stops meaning anything. The scheme was later extended from curves in the plane to genuine surfaces in 3D, and on to the full Helfrich functional with spontaneous curvature and area difference elasticity (ADE) effects; see the review by Barrett, Garcke and Nürnberg for the full family of variants that followed.

For a long time, though, having a scheme that *worked* in practice and having a scheme *proven* to converge were two different things. Kovács, Li and Lubich closed that gap: their 2019 paper established optimal-order convergence for mean curvature flow, and a 2020 follow-up did the same — a substantially harder analysis, requiring higher-order geometric bootstrap arguments — for Willmore flow itself. (Dziuk and Elliott's classic survey remains the reference of choice for the broader surface finite element machinery these results sit on.)

### A simple mean curvature flow algorithm

The mean curvature vector identity $$\kappa\b n = \Delta_\Gamma\,\mathrm{Id}$$ was first used to derive what could be considered the simplest surface finite element method for mean curvature flow. The flow we are interested in discretizing is simply

$$
v^\perp = \kappa \quad \text{ or equivalently } \quad \b{v} = \kappa\b{n}
$$

The velocity of the surface is nothing but the time derivative of its own position, $$\b v = \mathrm{d}\b X/\mathrm{d}t$$, where $$\b X$$ is the position vector of the surface nodes. Substituting this and the identity above into $$\b v=\kappa\b n$$ turns it directly into an evolution equation for the position itself:

$$
\frac{\mathrm{d}\b{X}}{\mathrm{d}t}=\Delta_\Gamma\,\b{Id}
$$

In what follows we propose an NgSolve script to simulate the mean curvature flow of a sphere.

```python
from ngsolve import *
from netgen.occ import *
from ngsolve.webgui import Draw

order = 1
tau = 2e-4

#### sphere case
R = 1
sphere = Sphere((0,0,0),R).faces[0]
mesh = Mesh(OCCGeometry(sphere).GenerateMesh(maxh=0.15)).Curve(order)

fesH = VectorH1(mesh,order=order)
u,v = fesH.TnT()

gfset = GridFunction(fesH) # current displacement

gfX = GridFunction(fesH) # position of points
gfXold = GridFunction(fesH) # old position of points

Mstar = BilinearForm(fesH)
Mstar += (u*v + tau*InnerProduct(Grad(u).Trace(),Grad(v).Trace()))*ds(deformation=gfset)
Mstar.Assemble()

# precompute initial inverse
inv = Mstar.mat.Inverse(fesH.FreeDofs(), inverse="sparsecholesky")

A = BilinearForm(fesH)
A += InnerProduct(Grad(u).Trace(),Grad(v).Trace())*ds(deformation=gfset)
A.Assemble()
```
The sphere will shrink to a point in finite time. The exact solution has radius $$R(t) = \sqrt{R_0^2-4\,t}$$ and at time $$T_{\mathrm{max}}=\frac{R_0^2}{4}$$ the radius becomes zero. Initialize $$\b{X}^0=\b{Id}$$ and zero displacement.

```python
t = 0

# time at which point is reached = R**2/4
Tend = R**2/4-1e-2
ex_R = sqrt(R**2-4*t)

# Reset initial data
# displ = 0,  X = id
gfset.vec[:] = 0
gfX.Set( CF( (x,y,z) ), definedon=mesh.Boundaries(".*"))

# auxiliary vector for time stepping scheme
r = gfset.vec.CreateVector()

scene = Draw(Norm(gfset), mesh, deformation=gfset)
```

During the time-stepping we save the old position, assemble the matrices at the current surface and update the positions. Then the displacement gets updated.

```python
i = 0
t = 0
with TaskManager():
    while t < Tend:
        print ("\rt=", t, end="")
        
        # save old position
        gfXold.vec.data = gfX.vec
        
        # assemble and invert
        Mstar.Assemble()
        A.Assemble()
        inv.Update()
        
        # update position
        r.data = A.mat*gfX.vec
        gfX.vec.data -= tau*inv*r
        
        # update displacement
        gfset.vec.data += gfX.vec-gfXold.vec
        
        if i % 10 == 0:
            scene.Redraw()
        t += tau
        i += 1
```

<figure class="figure">
  <video src="{{ "/assets/numalg/mc_sphere.mp4" | relative_url }}" poster="{{ "/assets/numalg/mc_sphere.0000.webp" | relative_url }}" loop muted playsinline controls preload="none"></video>
  <figcaption>Mean curvature flow of a sphere</figcaption>
</figure>

To simulate the evolution of a hollow cube, use the following parameters:

```python
body = Box(occ.Pnt(-1, -1, -1), occ.Pnt(1, 1, 1))
geo = OCCGeometry(body)
mesh = Mesh(geo.GenerateMesh(maxh=0.15, optsteps2d=3, perfstepsend=MeshingStep.MESHSURFACE))

Tend = 0.35
```

<figure class="figure">
  <video src="{{ "/assets/numalg/mc_square.mp4" | relative_url }}" poster="{{ "/assets/numalg/mc_square.0000.webp" | relative_url }}" loop muted playsinline controls preload="none"></video>
  <figcaption>Mean curvature flow of a hollow cube</figcaption>
</figure>

### Numerical method for Helfrich flow

It is a quite more involved matter to produce algorithms for Helfrich flow but, as already mentioned, many routes have been explored, each with its own advantages and limitations. In my case, we were interested in eventually simulating Helfrich flow of *realistic*, imaging-derived meshes. This quite ambitious challenge finally found its first successful outcome in the article cited at the very beginning of this card. The algorithm that allowed us to do so was an adaptation of the one presented in the article

> Garcke, Harald and Nürnberg, Robert and Zhao, Quan. *An Energy-Stable Parametric Finite Element Method for Willmore Flow with Normal-Tangential Velocity Splitting.* Society for Industrial and Applied Mathematics, 2026. [Link]({{ "https://epubs.siam.org/doi/epdf/10.1137/25M1773878" }})

Without going into the details, in the GitHub repository linked at the top of this page you find how you can simulate such dynamics, even on realistic geometries. I show here a couple of interesting simulations resulting from the algorithm.

Below is a pure Helfrich flow of a cigar-like shape that evolves under spontaneous curvature.

<figure class="figure">
  <video src="{{ "/assets/numalg/sigar_51_DuanLi.mp4" | relative_url }}" poster="{{ "/assets/numalg/sigar_51_DuanLi.0000.webp" | relative_url }}" loop muted playsinline controls preload="none"></video>
  <figcaption>Cigar-like shape evolving under Helfrich flow with spontaneous curvature −3. The cigar's aspect ratio is 5 to 1, and the colorbar shows the mean curvature.</figcaption>
</figure>

And here below is a more complex example of a system of reacting species that interact with the deformable membrane of a dendritic spine (a mushroom-like tiny component of a neuron synapse). The mesh in this case is derived directly from imaging of realistic dendritic spines.

<figure class="figure">
  <video src="{{ "/assets/numalg/fine_tetr_mesh_front.mp4" | relative_url }}" poster="{{ "/assets/numalg/fine_tetr_mesh_front.0000.webp" | relative_url }}" loop muted playsinline controls preload="none"></video>
  <figcaption>Interaction of a stable, realistic membrane with a system of reacting species. The colorbar shows the concentration of the main species pushing on the membrane.</figcaption>
</figure>


*This page is a starting draft.*

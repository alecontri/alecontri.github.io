---
layout: page
title: A realistic conjecture?
eyebrow: NumAlg
permalink: /numalg/willmore-flow/
back_url: /numalg/
back_label: NumAlg
---

Most of the surfaces I simulate — cell membranes, mostly — don't just carry chemistry on top of a fixed shape; the shape itself is part of the physics. Willmore flow is the cleanest model I know for curvature-driven shape evolution, and it's the natural next piece to bolt onto the surface finite element framework from my PhD.

## The Willmore energy and its gradient flow

For a closed surface $\Sigma$ with mean curvature $H$, the Willmore energy is

$$
\mathcal{W}(\Sigma) = \int_\Sigma H^2 \,\d A,
$$

a bending energy that (up to boundary terms and a topological constant, by Gauss&ndash;Bonnet) is exactly the Helfrich bending energy used to model lipid bilayers. Its $L^2$-gradient flow moves each point of the surface normal to itself,

$$
\partial_t \b x = -\big(\Delta_\Sigma H + 2H(H^2 - K)\big)\,\b n,
$$

where $K$ is the Gaussian curvature and $\Delta_\Sigma$ the Laplace&ndash;Beltrami operator on the (moving) surface. It's a fourth-order geometric PDE, which is the main source of both its numerical difficulty and its usefulness: it's the simplest flow that penalizes sharp bending rather than just surface area, which is exactly the kind of shape energy a real membrane resists.

## Discretizing on realistic meshes

The fourth-order operator is the first obstacle: a conforming $C^1$ surface finite element space is impractical on general triangulations, so, following Dziuk and others, I split the flow into a mixed system of two coupled second-order problems by introducing the mean curvature vector $\b H = H\b n$ as an independent unknown:

$$
\b H = -\Delta_\Sigma \b x, \qquad \partial_t \b x = -\Delta_\Sigma \b H - 2\b H\,(\norm{\b H}^2 - K) ,
$$

which only needs standard $C^0$ piecewise-linear surface elements for both $\b x$ and $\b H$, at the cost of solving a coupled saddle-point-like system at every step.

The second obstacle is the "realistic" part. Idealized test surfaces (spheres, tori, smooth analytic shapes) are forgiving; segmented cell geometries are not. Willmore flow on an unstructured, realistic mesh tends to degrade element quality over time as the tangential component of the flow (which does nothing to the geometry but everything to the mesh) accumulates, so a working scheme needs some form of tangential redistribution or tangential-velocity correction on top of the normal motion above, plus occasional remeshing once element quality drops below a threshold — otherwise the simulation quietly stops being a discretization of the continuous flow and starts being a discretization of a degenerate mesh.

<figure class="figure">
  <img src="{{ "/assets/numalg/willmore-sketch.svg" | relative_url }}" alt="Sketch of a triangulated surface mesh relaxing from an irregular outer shape to a smoother inner shape under Willmore flow">
  <figcaption>A rough mesh (faint) relaxing toward a smoother, lower-bending-energy shape (solid) under the flow above. Sketch, not simulation output.</figcaption>
</figure>

## Where this connects to my PhD work

This is the natural extension of the finite element framework I built during my PhD and my time at UC San Diego with Padmini Rangamani and Emmet Francis, described in:

> A. Contri, E. A. Francis, A. Massing, P. Rangamani. *Mechanochemical Feedback between Cell Shape and Intracellular Mechanics Revealed by a Finite-Element Framework.* bioRxiv, 2026. [Link]({{ "https://www.biorxiv.org/content/10.64898/2026.07.03.736361v1" }})

That framework couples surface advection-diffusion-reaction equations to membrane kinematics to capture mechanochemical feedback — membrane-tension-regulated migration, neutrophil protrusion, dendritic-spine remodeling — using simplified, prescribed deformation laws for the shape update. Swapping that deformation law for the mixed Willmore scheme above is the direction I'm currently most excited about: it would let the chemistry (signaling, actin dynamics) and the bending energy of the membrane drive each other directly, instead of through a deformation model that has to be tuned to look right.

*This page is a starting draft — I'll flesh it out with results and figures from my own simulations once the Willmore solver is integrated into the framework.*

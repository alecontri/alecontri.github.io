---
layout: page
title: Research
eyebrow: What I work on
permalink: /research/
---

My research sits at the intersection of numerical analysis and geometry: finite element methods for partial differential equations posed on evolving surfaces. Most of my PhD has been spent on advection-diffusion-reaction (ADR) equations coupled to a deforming membrane, with two threads running in parallel — proving that the coupled fluid/geometry discretization actually converges, and building the stabilized, bound- and mass-preserving schemes needed to make the simulations physically trustworthy. That work has grown into a finite element framework, developed with André Massing and, during a research stay at UC San Diego, with Padmini Rangamani and Emmet Francis, that couples surface ADR equations to membrane mechanics to study mechanochemical feedback in cell shape — things like membrane-tension-regulated migration, neutrophil protrusion, and actin remodeling in dendritic spines.

Going forward, I want to push this framework in two directions. The first is deeper into the geometry: coupling the ADR/mechanics solver to genuine curvature-driven shape evolution (Willmore-type flows) so that chemical signaling and membrane shape can feed back on each other fully, rather than through simplified deformation models. The second is broader in scope — carrying the meshed, stabilized-FEM toolkit I've built for biological membranes over to other moving-domain and moving-boundary problems I find equally compelling, from celestial mechanics to debris-flow modeling, and eventually experimenting with learned surrogates for the parts of these simulations that are still too expensive to run at the resolutions I actually want.

If any of this overlaps with what you're working on, I'd love to hear from you — see the [contact links](mailto:{{ site.email }}) below, or have a look at what I've been building for fun on the [NumAlg]({{ "/numalg/" | relative_url }}) page.

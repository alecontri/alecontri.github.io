---
layout: page
title: Research
eyebrow: What I work on
permalink: /research/
---

The common denominator of my research has been dealing with time-dependent and evolving-domain problems. Most of my expertise lies in the classical finite element method (FEM), although I also have some experience with hybrid mesh-particle methods. In my most recent work, I have pivoted toward computational biomechanics in the effort of bridging the gap between the accuracy and convergence properties of FEM algorithms and their applicability to realistic scenarios. This work has grown into a finite element framework, developed with my supervisor André Massing and in collaboration with the UC San Diego lab of Padmini Rangamani. The framework is focused on mechanochemical feedback in cell dynamics — things like membrane-tension-regulated migration, neutrophil protrusion, cell motility and actin remodeling in dendritic spines. A big component of this research has been dealing with deformable membranes that undergo large deformations and the related surface-bulk coupling.

If I had to place my current studies I would say that my research sits at the intersection of numerical analysis and geometry. Working with these types of problems has made me realize the following:
1. The effort to prove stability and convergence properties of algorithms is crucial to have trustworthy instruments, but an eye has to be kept on the applications of interest in order to facilitate the transition and usability of the code
2. Preserving the structures embedded in the PDEs of interest is key not only to design stable algorithms but also to maintain their interpretability when real phenomena are simulated
3. There is an existing bottleneck between state-of-the-art numerical algorithms and computational science applications that needs to be bridged. A lot has yet to be done, but the technology is mature enough for this transition

Going forward, I would love to expand my studies in the following ways:
1. Much has yet to be done for the cell reshaping mechanism I have encountered in the last few years. On one hand I want to advance the software engineering side of my framework to production level, to actually test how far we can push the claims made in our two contributions. On the other hand, I believe there is room for development of novel models that can represent a more complex, accurate physics. In this context I am looking at integrating the elastic and fluid counterpart in both the bulk and surfaces to provide stable algorithms that have realistic, predictive capability.
2. Connected to the above, I am very interested in the world of active matter (nematic and polar crystals, active turbulence and so on) across scales and fields. I am attracted by the algorithm development challenges that it poses, especially on surfaces, and the structures that underlie some of such models. It is remarkable how the same PDEs can span such disparate topics as bacteria swimming, fish schooling, bird flocking and star formation. And this excites me a lot.
3. FEMs are dear to my heart, but I am aware they are not the solution for every PDE modeling question. On the longer term, I would like to become more acquainted with learning methods. In specifics, I see in structure-preserving, physics-informed learning algorithms the key to achieve the applicability I am striving to achieve. I believe in this not only as a per-se technique but also as a useful tool to fit together with classical techniques.
4. Finally, since I am constantly enchanted by nature and its wonders (and concerned about its current and future status), I would love to explore tangential research strands linked to environmental science. Ocean, glacier, weather dynamics and collective animal behaviour are next on my list as passions I would gladly welcome into my daily work.

If any of this overlaps with what you're working on, I'd love to hear from you — see the [contact links](mailto:{{ site.email }}) below, or have a look at what I've been building for fun on the [Rabbit Holes]({{ "/rabbit-holes/" | relative_url }}) page.

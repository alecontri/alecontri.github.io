---
layout: page
title: Introduction
permalink: /introduction/
---

Smooth Manifolds
----

The purpose of this chapter is to introduce the mathematical objects on which our structures will live. They are basically generalized spaces on which one can do calculus. We are interested in applying calculus-like objects as its tools are necessary to describe the geometry of these spaces, e.g. volume or curvature. For this purpose topological spaces are not enough, since a definition of smoothness is impossible to give in that context, and we have to ask for more regularity.  In order to enable integration and differentiation, it is thus required that our spaces locally look like an Euclidean space $\RR^n$.

Our focus will be in introducing the necessary tools to be able to understand them and how to compare them with the discrete "numerical" counterpart. Mathematically, these objects can be described taking two different point of views:

- Intrinsic: we describe the object as if all the quantities describing it were strictly living on it. It is a very useful approach to keep the notation simple and avoid extra information to "pollute" our study. It is the preferred point of view to understand the invariants at stake.
- Extrinsic: we consider the object immersed in a larger space called the "ambient" space of which our manifold is a piece. We zoom out, allowing extra information from the surrounding to enter the game. Although more complicated, it is the preferred approach to switch to practical implementation, since once can use (*very carefully*) the tools of the infamous Euclidean space to operate on the manifold. For us, it is extremely important as a mean of comparison between the dicrete version and the smooth one for convergence analysis, since the two objects will be both immersed in the same ambient space. It is also useful when the manifold evolves in time, changing its shape.

Some math preliminaries:
1. [Smooth Manifolds]({{ site.baseurl }}/smooth_manifolds/)
2. [Tangent Space]({{ site.baseurl }}/tangent_space/)
3. [Submanifolds]({{ site.baseurl }}/submanifolds/)
4. [Vectors]({{ site.baseurl }}/vectors/) and [Covectors]({{ site.baseurl }}/covectors/)
5. [Tensors]({{ site.baseurl }}/tensors/)
5. [Riemannian Manifolds]({{ site.baseurl }}/riemann/)
6. [Integration]({{ site.baseurl }}/integration/)
7. [Finite Elements]({{ site.baseurl }}/fem/)

**A. Overview of Surface Finite Elements**
- Definition and applications
- Importance of convergence analysis


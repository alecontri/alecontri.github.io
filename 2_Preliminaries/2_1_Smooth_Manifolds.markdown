---
layout: page
title: Smooth Manifolds 
permalink: /smooth_manifolds/
exclude: true
---

To define and understand smooth manifolds we first need to define its closest precursor: the topological manoflold.

***Topological Manifold***

Suppose $M$ is a topological space. We say that $M$ is a **topological $n$-manifold** if it has the following properties:
- $M$ is a **Hausdorff space**
- $M$ is **second-countable**
- $M$ is **locally Euclidean of dimension $n$** : each point of $M$ has a neighborhood which is homeomorphic to an open suset of $\RR^n$.

The third property means that for each $p\in M$ we can find:
- an open subset $U\subseteq M$ containing $p$,
- an open subset $\hat{U}\subseteq\RR^n$, and
- a homeomorphism $\phi:\hat{U}\to U$ (a.k.a. a bijective, continuous function).

<div class="math-box">
  <div class="box-title">Why do we define it like this?</div>
  <div class="box-content">
      Requiring that manifolds share these properties helps to ensure that manifolds behave in the ways we expect from our experience with Euclidean spaces. For example, in a Hausdorff space,finite subsets are closed and limits of convergent sequences are unique. There are illed cases like the empty set itself, where all sequences converge to the same element and this causes troubles.  Second-countability is instead linked to the existence of partition of unity and thus to the ability of performing integration on it, fast-forward we are really interested in doing it. A nice feature is that both properties are inherited by subspaces and finite products.
  </div>
</div>

> **Remark**: A nonempty $n$-dimensional topological manifold cannot be homeomorphic to a $m$-dimensional manifold unless $m=n$.

A **coordinate chart** on $M$ is a pair $(U,\phi)$, where $U$ is an open subset of $M$ and $\psi = \phi^{-1}:U\to \hat{U}$ is a homeomorphism from $U$ to an open subset $\hat{U}=\phi(U)\subseteq \RR^n$. Given a chart $(U,\psi)$ we call the set $U$ a *coordinate domain*. The map $\phi$ is called a *(local) coordinate map*, and the component functions $(x^1,\ldots,x^n)$ of $\phi$, defined by $\phi(p)=(x^1(p), \ldots, x^n(p))$, are called **local coordinates** on $U$.

----
<br>

Now that we introduced topological manifolds, we add on top of that an additional structure, in particular a smooth one.

***Smooth Structures***

> **Remider**: If $U$ and $V$ are open subsets of Euclidean spaces $\RR^n$ and $\RR^m$, respectivley, a function $F:U\to V$ is said to be **smooth** if each of its component functions has continuous partial derivatives of all orders. If in addition $F$ is bijective and has smooth inverse map, it is called a **diffeomorphism**.

Let $M$ be a topological $n$-manifolds. If $(U,\phi)$, $(V,\psi)$ are two charts such that $U\cap V\neq \emptyset$, the composite map $\psi\circ\phi^{-1}:\phi(U\cap V)\to \psi(U\cap V)$ is called the _transition map_ from $\phi$ to $\psi$ (composition of homeomorphisms and thus homeomorphism itself). Two charts  $(U,\phi)$ and $(V,\psi)$ are said to be _smoothly compatible_ if either $U\cap V = \emptyset$ or the transition map $\psi\circ\phi^{-1}$ is a diffeomorphism.

We define an **atlas** for $M$ to be a collection of charts whose domains cover $M$. An atlas $\c{A}$ is called a _smooth atlas_ if any two charts in $\c{A}$ are smoothly compatible with each other. A smooth atlas $\c{A}$ on $M$ is _maximal_ if it is not properly contained in any larger smooth atlas. This just means that any chart that is smoothly compatible with every chart in $\c{A}$ is already in $\c{A}$. 

----
<br>

We are now finally able to define our core structures:

<div class="math-box">
  <div class="box-title">Definition of Smooth Manifold</div>
  <div class="box-content">
      A <strong>smooth manifold</strong> is a pair $(M,\c{A})$, where $M$ is a topological manifold and $\c{A}$ is a maximal smooth atlas on $M$
  </div>
</div>

We than have a series of specifications which follows.

***Smooth maps***

Let $M,N$ be smooth manifolds, and let $F:M\to N$ be any map. We say that $F$ is a **smooth map** if for every $p\in M$, there exist smooth charts $(U, \phi)$ containing $p$ and $(V,\psi)$, containing $F(p)$ such that $F(U)\subseteq V$ and the composite map $\psi\circ F \circ \phi^{-1}$ is smooth from $\phi(U)$ to $\psi(V)$. 
- The definition of smooth **real-** and **vector-values** functions is a special case of smooth map where $N=\RR^k$ and $\psi = Id :\RR^k\to\RR^k$.
- The requirement $F(U)\subseteq V$ is added so that smoothness implies continuity.

***Manifolds with boundary***

Define the *closed $n$-dimensional upper half-space* $\bb{H}^n\subseteq \RR^n$ as
$$
\bb{H}^n=\{ (x^1,\ldots,x^n)\in \bb{R}^n:x^n\geqslant 0 \}.
$$

An $n$-dimensional **topological manifold with boundary** is a second-countable Hausdorff space $M$ in which every point has a neighborhood homeomorphic either to an open subset of $\bb{R}^n$ or to a (relatively) open subset of $\bb{H}^n$. When it is necessary to make the distinction, we will call $(U,\phi)$ an *interior chart* if $\phi(U)$ is an open subset of $\bb{R}^n$, and a *boundary chart* if $\phi(U)$ is an open subset of $\bb{H}^n$ such that $\phi(U)\cap \partial\bb{H}^n\neq \emptyset$.

<div class="math-box">
  <div class="box-title">To note</div>
  <div class="box-content">
  <ul>
      <li> A manifold with boundary might have empty boundary.</li>
      <li> A manifold is a manifold with boundary, whose boundary is empty. Thus, every manifold is a manifold with boundary, but a manifold with boundary is a manifold if and only if its boundary is empty.</li>
   </ul>
  </div>
</div> 

In the literature you will also encounter the terms *closed manifold* to mean a compact manifold without boundary, and a *open manifold* to mean a noncompact manifold without boundary.



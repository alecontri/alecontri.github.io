---
layout: page
title: Riemanninan Manifolds 
permalink: /riemann/
exclude: true
---

We intorduce geometry into smooth manifolds using the theory of finite-dimensional vector spaces.

Let $M$ be a smooth manifold with or without boundary. A **Riemannian metric on $M$** is a smooth symmetric covariant 2-tensor field on $M$ that is positive definite at each point. A **Riemannian manifolds** is a pair $(M,g)$, where $M$ is a smooth manifold and $g$ is a Riemannian metric on $M$. A **Riemannian manifold with boundary** is defined similarly.

> A Riemannian metric is not the smae thing as a metric in metric spaces, even though the concepts are linked.

In any smooth local coordinates $(x^i)$, a Riemannian metric can be written
$$
g = g_{ij} dx^i\otimes dx^j
$$
where $g_{ij}$ is a symmetric positive definite matrix of smooth funcitons. The notation $g=g_{ij}dx^idx^j$ is also used.

<div class="math-box">
  <div class="box-title">Proposition</div>
  <div class="box-content">
    Every smooth manifold with or without boundary admits a Riemannian metric.
  </div>
</div>

Note that different Riemannian metrics can be defined on a manifold which enjoy different properties, so there is nothing canonical about it!

The eixstence of a Riemannian metric allows us to define
1. The **length** of **norm** of a tangent vector $v\in\T{p}{M}$ is defined to be 

    $$
    |v|_g=\langle v,v\rangle^{1/2}=g_p(v,v)^{1/2}
    $$
2. The **angle** between two nonzero tangent vectors $v,w\in \T{p}{M}$ is the unique $\theta\in [0,\pi]$ satisfying

    $$
    \cos\theta=\frac{\langle v,w \rangle_g}{|v|_g|w|_g}
    $$
3. Tangent vectors $v,w\in \T{p}{M}$ are said to be **orthogonal** if $\langle v,w \rangle_g=0$. This means either one or both vectors are zero, or the agle between them is $\pi/2$.

This allows to define **orthonormal frames**. Let $(M,g)$ be a $n$-dimensional Riemannian manifold with or without boundary. A local frame $(E_1,\ldots,E_n)$ for $M$ on an open subset $U\subset M$ is an **orthonormal frame** if the vectors $\restr{E_1}{p},\ldots,\restr{E_n}{p}$ form an orthonromal basis for $\T{p}{M}$ at each point $p\in U$, or equivalently $\langle E_1,E_j\rangle = \delta_{ij}$.

> Let $(M,g)$ be a Riemannian manifold with or without boundary. For each $p\in M$, there is a smooth orthonormal frame on a neighborhood of $p$.

Note that the above doesn't say that there always exist smooth coordinates on anighborhood of $p$ such that the coordinate frame is orthonormal.

<div class="math-box">
  <div class="box-title">Proposition</div>
  <div class="box-content">
    Suppose $F:M\to N$ is a smooth map and $g$ is a Riemannian metric on $N$. Then $F^\ast g$ is a Riemannian metric on $M$ if and only if $F$ is a smooth immersion.
  </div>
</div>

%%%% Put example here

If $(M,g)$ and $(\t{M}, \t{g})$ are both Reimannian manifolds, a smooth map $F:M\to \t{M}$ is called a **(Riemannian) isometry** if it is a diffeomorphism that satisfies $F^\ast\t{g}=g$. More generally, $F$ is called a **local isometry** if every point $p\in M$ has a neighborhood $U$ such that $\restr{F}{U}$ is an isometry of $U$ onto an open subset of $\t{M}$; or equivalently, if $F$ is a local diffeomorphism satisfying $F^\ast\t{g}=g$.

If there exist a Riemannian isometry between $(M,g)$ and $(\t{M},\t{g})$, we say that they are **isometric** as Riemannian manifolds. If each point of $M$ has a neighborhood that is isometric to an open subset of $(\t{M}, \t{g})$, then we say that $(M,g)$ is **locally isometric** to $(\t{M}, \t{g})$. The study of properties of Riemannian manifolds that are invariant under (local or global) isometries is called **Riemannian geoemtry**.

One such property is _flatness_. A Riemaniian $n$-manifold $(M,g)$ is said to be a **flat Riemannian mnaifold**, and $g$ is a flat metric, if $(M,g)$ is locally isometric to the Euclidean space $\bb{R}^n$ with the standard metric. In fact, in the 1-dimensional case very metric is flat.

-------
<br>

**Riemannian submanifolds**

Pullback metrics are especially important for submanifolds. If $(M,g)$ is a Reimannian manifold with or without boundary, every submanifold $S\subseteq M$ (immersed or embedded, with or without boundary) automatically inherits a pullback metric $\i^\ast g$, where $\i:S\hookrightarrow M$ is inclusion. In this setting, the pullback metric is also called the **induced metric** on $S$. By definition, this means for $v,w\in \T{p}{S}$ that

$$
(\i^\ast g)(v,w)=g(d\i_p(v),d\i_p(w))=g(v,w),
$$

because $d\i_p:\T{p}{S}\to \T{p}{M}$ is our usual identification of $\T{p}{S}$ as a subspace of $\T{p}{M}$. Thus $\i^\ast g$ is just the restriction of $g$ to pairs of vectors tangent to $S$. With this metric, $S$ is called a **Riemannian submanifold (with or without boundary) of $M$**.

_The Normal Bundle_

Suppose $(M,g)$ is an $n$-dimensional Riemannian manifold with or without boundary, and $S\subseteq M$ is a $k$-dimensional Riemaniian submanifold (also with or without boundary). Just as we did for submanifolds of $\bb{R}^n$, for any $p\in S$ we say that a vector $v\in \T{p}{M}$ is **normal to $S$** if $v$ is orthogonal to every vector in $\T{p}{S}$ with respect to the inner product $\langle \cdot, \cdot \rangle_g$. The **normal space to $S$ at $p$** is the subspace $N_pS\subset\T{p}{M}$ consisting of all vectors that are normal to $S$ at $p$, and the **normal bundle of $S$** is the subset $NS\subseteq \T{}{M}$ consisting of the union of all the normal spaces at points of $S$. The projection $\pi_{NS}:NS\to S$ is defined as the restriction to $NS$ of $\pi:\T{}{M}\to M$.

<div class="math-box">
  <div class="box-title">Proposition</div>
  <div class="box-content">
    Let $(M,g)$ be a Riemannian $n$-manifold with or without boundary. For any immersed $k$-dimensional submanifold $S\subseteq M$ with or without boundary, the normal bundle $NS$ is a smooth rank-$(n-k)$ subbundle of $\restr{\T{}{M}}{S}$. For each $p\in S$, there is a smooth frame for $NS$ on a neighborhood of $p$ that is othonromal with respect to $g$.
  </div>
</div>

-------
<br>

**Riemannian Distance Function**

Riemannian metric gives the ability to define lengths of curves on the manifold. Suppsoe $(M,g)$ is a Riemannian manifold with or without boundary. If $\gamma:[a,b]\to M$ is a piecewise smooth curve segment, the **length of $\gamma$** is

$$
L_g(\gamma)=\int_a^b|\gamma(t)'|\mathrm{d}t
$$

which is well-defined since the argument is continuous at all but finitely many values and has well-defined limits from left and right at those points.

<div class="math-box">
  <div class="box-title">Proposition</div>
  <div class="box-content">
    Suppsoe $(M,g)$ is a connected Riemannian manifold. For any $p,q\in M$, the <strong>(Riemannian) distance from $p$ to $q$</strong>, denoted by $d_g(p,q)$, is defined as the infimum of $L_g(\gamma)$ over all piecewise smoothcurve segments $\gamma$ from $p$ to $q$.
  </div>
</div>

<div class="math-box">
  <div class="box-title">Theorem</div>
  <div class="box-content">
    Let $(M,g)$ be a connected Riemannian manifold. With the Riemannian distance function, $M$ is a metric space whose topology is the same as the original manifold topology.
  </div>
</div>

As a consequence of the above, all the terminology of metric spaces can be carried over to connected Riemannian manifolds. Thus, a commected Riemannian manifold $(M,g)$ is said to be complete, and $g$ is said to be a **complete Riemannian metric**, if $(M,d_g)$ is a complete metric space (i.e. every Cauchy sequance in $M$ converges to a point in $M$); and a subset $B\subseteq M$ is said to be **bounded** if there exist a constant $K$ such that $d_g(x,y)\leq K$ for all $x,y\in B$.


-------
<br>

The Riemannian metric also provides a natural isomorphism between the tangent and cotangent bundles. Given a Riemannian metric $g$ on a smooth manifold $M$ with or without boundary, we define a bundle homomorphism $\hat{g}:\T{}{M}\to \cT{}{M}$ as follows. For each $p\in M$ and each $v\in \T{p}{M}$, we let $\hat{g}(v)\in\cT{p}{M}$ be the covector defined by

$$
\hat{g}(v)(w)=g_p(v,w) \text{ for all } w\in \T{p}{M}.
$$

In this case we denote the components of the covector field $\hat{g}(X)$ by

$$
\hat{g}(X)=X_j \d x^j, \quad \text{ where } X_j=g_{ij}X^i.
$$
and we say that $\hat{g}(X)$ is obtained from $X$ by **lowering the index**. The notation $X^\flat$ is frequently used for $\hat{g}(x)$.

The inverse operation can also be accomplished through a map $\hat{g}^{-1}:\cT{p}{M}\to \T{p}{M}$. For a covector field $\omega\in \c{X}^\ast(M)$, the vector field $$\hat{g}^{-1}(\omega)$ has the coordinate representation

$$
\hat{g}^{-1}(\omega)=\omega^i\frac{\partial}{\partial x^i}, \quad \text{ where } \omega^i=g^{ij}\omega_j.
$$

We use the notation $\omega^\sharp$ for $\hat{g}^{-1}(\omega)$, and say that $\omega^\sharp$ is obtained from $\omega$ by **raising an index**. Because the symbols $\flat$ and $\sharp$ are borrowed from the musical notation, these two inverse isomorphisms are frequently called the **musical isomoprhisms**.

<div class="math-box">
  <div class="box-title">Definition</div>
  <div class="box-content">
    For any smooth real-valued function $f$ on a Riemannian manifold $(M,g)$ with or without boundary, we define a vector field called the <strong> gradient of $f$ </strong> by

    $$
    \mathrm{grad} f=(\d f)^\sharp=\hat{g}^{-1}(\d f)
    $$

    Unraveling the definitions the gradient satisfies

    $$
    \langle \mathrm{grad} f, X \rangle_g=\hat{g}(\mathrm{grad} f)(X)=\d f(X) = Xf
    $$

    Thus, the gradeint is the unique vector field that satisfies

    $$
    \langle \mathrm{grad} f, \cdot\rangle = \d f.
    $$
  </div>
</div>

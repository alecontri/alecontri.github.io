---
layout: page
title: Submanifolds 
permalink: /submanifolds/
exclude: true
---

The $\rank$ plays a central role as the *only* property of differentials that is independent of the local cart chosen. Moreover, maps whose differential has constant $\rank$ turn out to be good local descriptors of the manifold considered and its structure.

% Maybe add Inverse Function theorem

***Submersion, Immersion and Embedding***

Given a smooth map $F:M\to N$ and a point $p\in M$, we define the **$\rank$ of $F$ at $p$** to be the $\rank$ of the linear map $dF_p:\T{p}{M}\to \T{F(p)}{N}$.

<div class="math-box">
  <div class="box-title">Rank theorem</div>
  <div class="box-content">
    Suppose $M$ and $N$ are smooth manifolds of dimension $m$ and $n$, respectively, and $F:M\to N$ is a smooth map with constant $\rank$ $r$. For each $p\in M$ there exist smooth charts $(U,\phi)$ for $M$ centered at $p$ and $(V,\psi)$ for $N$ centered at $F(p)$ such that $F(U)\subseteq V$, in which $F$ has a coordinate representation of the from

    $$
        \hat{F}(x^1,\ldots,x^r,x^{r+1},\ldots, x^m) = (x^1,\ldots,x^r,0, \ldots, 0).
    $$
  </div>
</div>

> The Implicit function theorem is a particularization of the Rank theorem above.

Let $M$ and $N$ be smooth manifolds, and suppose $F:M\to N$ is a smooth map of constant $\rank$. The most important types of maps are:
- $F$ is a **submersion** if its differential is surjective at each point, or equavalently if it has contant $\rank$ equal to $\dim N$. With reference to the assumptions above we have:
    $$
        \hat{F}(x^1, \ldots,x^n, x^{n+1},\ldots, x^m)=(x^1,\ldots, x^n)
    $$
- $F$ is an **immersion** if its differential is injective at each point, or equivalently if it has contant $\rank$ equal to $\dim M$. With reference to the assumptions above we have:
    $$
         \hat{F}(x^1,\ldots,x^m) = (x^1,\ldots, x^m,0 ,\ldots, 0).
    $$
- $F$ is a **local diffeomorphism** if every point $p\in M$ has a neighborhood $U$ such that $\restr{F}{U}$ is a diffeomorphism onto an open subset of $N$, or equivalently if $F$ is both a submersion and an immersion.
-  $F$ is a **smooth embedding** if it is an injective immersion that is also a topological embedding (a homeomorphism onto its image, endowed with the subspace topology).

All of the above can be extended globally saing that:
- If $F$ is surjective, then it is a smooth submersion.
- If $F$ is injective, then it is a smooth immersion.
- If $F$ is bijective, then it is a diffeomorphism.

>If $M$ is a smooth manifold with or without boundary and $U\subseteq M$ is an open submanifold, the inclusion map $U \hookrightarrow M$ is a smooth embedding

<div class="math-box">
  <div class="box-title">Rank theorem for manifolds with boundaries</div>
  <div class="box-content">
    Suppose $M$ is a smooth $m$-manifold with boundary, $N$ is a smooth $n$-manifold, and $F:M\to N$ is a smooth immersion. For any $p\in \partial M$, there exist a smooth boundary chart $(U,\phi)$ for $M$ centered at $p$ and a smooth coordinate chart $(V,\psi)$ for $N$ centered at $F(p)$ with $F(U)\subseteq V$, in which $F$ has the coordinate representation
    $$
        \hat{F}(x^1,\ldots, x^m)=(x^1,\ldots, x^m, 0,\ldots,0)
    $$
  </div>
</div>

It is useful to bear in mind some examples of injective smooth maps that are **not** smooth embedding.
- The map $\gamma : \bb{R} \to \bb{R}^2$ given by $\gamma(t)=(t^3,0)$ is a smooth map and a topological embedding, but it is not a smooth embbedding because $\gamma'(0)=0$.
- Consider the curve $\beta:(-\pi,\pi)\to \bb{R}^2$ defined by
        $$
            \beta(t)=(\sin(2t),\sin(t)).
        $$
        Its image is a set that looks like a figure-eight in the plane. It is easy to see that $\beta$ is an injective smooth immersion becaise $\beta'(t)$ never vanishes; but it is not a topological embedding., because its image is compact in the subspace topology, while it's domain is not.

---
<br>

***Embedded and Immersed submanifolds***

Suppose $\t{M}$ is a smooth submanifold with or without boundary. An **immersed $n$-dimensional submanifold** is a subset $M\subset\t{M}$ endowed with a topology (not necessarily the subspace topology) that makes it into a $n$-dimensional topological manifold and a smooth structure such that the inclusion map $M\hookrightarrow\t{M}$ is a smooth immersion. It is called an **embedded submanifold** if the inclusion is a smooth embedding, or equivalently it the given topology on $M$ is the subspace topology. Immersed and embedded **submanifold with boundary** are defined similarly. In each case the **codimension of $M$** is the difference $\dim\t{M}-\dim M$. A submanifold of codimension 1 is known as a **hypersurface**.

This is only one definition of submanifolds using charts. Alternative deifitions exist using: local parametric reresentation, local graph representation, local levelset representation. Many of the existing submanifolds are modeled as follows.

*Level Sets*

If $\phi:M\to N$ is any map and $c$ is any point of $N$, we call the set $\phi^{-1}(c)$ a **level set of $\phi$**


> Let $M$ and $N$ be smooth manifolds, and let $\phi:M\to N$ be a smooth map with constant $\rank$ $r$. Each level set of $\phi$ is a properly embedded submanifold of codimension $r$ in $M$.


> If $M$ and $N$ are smooth manifolds and $\phi:M\to N$ is a smooth submersion, then each level set of $\phi$ is a properly embedded submanifold whose codimension is equal to the dimension of $N$.


If $\phi :M\to N$ is a smooth map, a point $p\in M$ is said to be a **regular point of $\phi$** if $d\phi_p:\T{p}{M}\to \T{p}{N}$ is surjective; it is a **critical point of $\phi$** otherwise. Thus:
- Every point of $M$ is critical if $\dim M < \dim N$
- Every point is regular if and only if $F$ is a submersion. 

A level set $\phi^{-1}(c)$ is called a **regular level set** if every point of the level set $\phi^{-1}(c)$ is a regular point.

<div class="math-box">
  <div class="box-title">Level Set Theorem</div>
  <div class="box-content">
    Every regular level set of a smooth map between smooth manifolds is a properly embedded submanifold whose codimension is equal to the dimension of the codomain.

    Also, every embedded $k$-submanifold of a $m$-smooth manifold $M$ has to be the level set of a smooth submersion $\phi:M\to \bb{R}^{m-k}$. 
  </div>
</div>

_Examples_

- $\bb{S}^n$ is an embedded submanifold of $\bb{R}^{n+1}$. The sphere is a regular level set of the smooth funciton $f:\bb{R}^{n+1}\to \bb{R}$ given by $f(x)=\vert x\vert^2$, since $df_x(v)=2\sum_i x^iv^i$ is surjective except at the origin.
- The torus of revolution given by the surface of revolution obtained from the circle $(r-2)^2 +z^2=1$. It is a regular level set of the function $\phi(x,y,z) = \left( \sqrt{x^2+y^2}-2\right)^2+z^2$, which is smooth on $\bb{R}^3$ minus the $z$-axis.
    In fact this, every **surface of revolution** is an embedded $2$-dimensional submanifold of $\bb{R}^3$. We can define them as follows. Let $H$ be the half-plane $\{(r,z):r>0\}$, and suppose $C\subseteq H$ is an embedded $1$-dimensional submanofold. The **surface fo revolution** determined by $C$ is the subset $S_C\subseteq \bb{R}^3$ given by
    $$
        S_C=\left\{(x,y,z):\left(\sqrt{x^2+y^2},z\right)\in C\right\}.
    $$
    One can show that this results in a regular level-set.


***Immersed submanifolds***

Sometimes embedded submanifols can result in being too restrictive because for example they do not allow self-intersections. It is then worth to spend a few more words on this larger family.

Suppose $M$ is a smooth manifold with or without boundary and $S\subseteq M$ is an immersed submanifold. If any of the following holds, then $S$ is embedded.
- $S$ has codimension $0$ in $M$.
- The inclusion map $S\subseteq M$ is proper, i.e. the inclusion map sends compact sets into compact sets.
- $S$ is compact.

What can go wrong for a manifold to be immersed and not embedded?

- **Injectivity** of $F$ itself. Even if $F$ can be a smooth immmersion it can be not injective itself. Consider for example the map $F:\bb{R}\to\bb{R}^2$ idefined by $F(t):t\to(\sin(t), \sin(2t))$. The map is a smooth immersion, but it is not injective in $(0,0)$.
- **Homeomorphism** into its image. Consider the map for the circle $F:[0,2\pi)\to S^1\subset \bb{R}^2$ given by $F(t):t\to (\cos(t), \sin(t))$  It is an immersino and it is injecitive (making it an immersion), but the topology of the codomain is different from the domain one, as the circle is a compact set while the interval is open.

We will mostly deal with embeddings, but there are ways to generalize these concepts using only immersions and still guarantee that
- the tangential space is well defined and has the same dimension of the domain
- particular behaviours are allowed such as intersections and kinks.
    
*The Tangent Space to a Submanifold*

Let $M$ be a smooth manifold with or without boundary, and let $S\subseteq M$ be an immersed or embedded submanifold. Since the inclusion map $\imath :S\hookrightarrow M$ is a smooth immersion, at each point $p\in S$ we have an injective linear map $d\imath_p:\T{p}{S}\to \T{p}{M}$. In terms of derivations, this injection works in the following way: for any vector $v\in \T{p}{S}$, the image vector $\tilde{v}=d\imath_p(v)\in \T{p}{M}$ acts on smooth functions on $M$ by 

$$
    \tilde{v}f=d\imath_p(v)f=v(f\circ \imath)=v(f\vert_S).
$$

We identify $\T{p}{S}$ with its image under this map, thereby thinking of $\T{p}{S}$ as a certain linear subspace of $\T{p}{M}$. This identification makes sense regardless of whether $S$ is embedded or immersed.

Fun facts:
- Suppose $M$ is a smooth manifold and $S\subseteq M$ is an embedded submanifold. Suppose you are given $\phi:U\to N$ such that $U\cap S$ is a level set for $\phi$, i.e. $\phi$ is any so-called _local defining map_ for $S$. Then $\T{p}{S}=\ker d\phi_p:\T{p}{M}\to T_{\phi(p)}S$ for each $p\in S\cap U$.
- Suppose $S\subseteq M$ is a level set of smooth submersion $\phi = (\phi^1,\ldots, \phi^k):M\to \bb{R}^k$. A vector $v\in \T{p}{M}$ is tangent to $S$ if and only if $v\phi^1=\ldots=v\phi^k=0$.


If $M$ is a smooth manifold with boundary and $p\in \partial M$, the vectors in $\T{p}{M}$ can be separated into three classes: tangent to the boundary, inward pointing and outward pointing. 
1. If $p\in \partial M$, a vector $v\in \T{p}{M}\setminus T_{p}\partial M$ is said to be **inward pointing** if for some $\epsilon>0$ there exists a smooth curve $\gamma :[0,\epsilon)\to M$ such that $\gamma(0)=p$ and $\gamma'(0)=v$
2. The vector is **outward-pointing** if there exists such a curve whose domain is $(-\epsilon, 0]$.

If $M$ is a smooth manifold with boundary, a **boundary defining function** for $M$ is a smooth function $f:M\to [0,\infty)$ such that $f^{-1}(0)=\partial M$ and $df_p\neq 0$ for all $p\in \partial M$.

>Every smooth manifold with boundary admits a boundary defining function.

*Submanifolds with Boundary*

The definitions for submanifolds with boundary are straightforward generalizations of the ones for ordinary submanifolds.

When dealing with manifolds with boundary, they are often considered as embedded in a larger manifold which is without boundary. One way of doing it it's to merging two disjoint unions of the same manifold along the respective boundaries. It can be proven that the resulting manifold is
- a topological manifold without boundary
- smooth
- the maps from the final manifold to each of the two copies of the original are smooth emebeddings
- the final manifold is compact if and only if the starting one is compact. The same holds for connectivity. 

---
<br>

**The Whitney approximation Theorems**

<div class="math-box">
  <div class="box-title">Whitney Approximation Theorem</div>
  <div class="box-content">
    Suppose $M$ is a smooth manifold with or without boundary, and $F:M\to \bb{R}^{k}$ is a continuous function. Given any positive continuous function $\delta : M\to \bb{R}$, there exists a smooth function $\tilde{F}:M\to \bb{R}^k$ that is $\delta$-close to $F$. If $F$ is smooth on a closed subset $A \subseteq M$, then $\tilde{F}$ can be chosen to be equal to $F$ on $A$. 
  </div>
</div>

The above theorem if of fundamental importance when we will have to deal with smooth approximations to maps between manifolds. 

For this purpose we introduce **tubular neighborhoods**. For each $x\in \bb{R}^n$, the tangent space $\T{x}{\bb{R}^n}$ is canonically identified with $\bb{R}^n$ itself, and the tangent bundle $\T{}{\bb{R}^n}$ is canonically diffeomorphic to $\bb{R}^n\times \bb{R}^n$. By virtue of this identification, each tangent space $\T{x}{\bb{R}^n}$ inherits a Euclidean dot product. Suppose $M\subseteq \bb{R}^n$ is an embedded $m$-dimensional submanifold. For each $x\in M$, we define the **normal space to $M$ at $x$**  to be the $(n-m)$-dimensional subspace $ \c{N}\_{x} M \subseteq \T{x}{\bb{R}^n}$  consisting of all vectors that are orthogonal to $\T{x}{M}$ with respect to the Eucledian dot product. 

<div class="math-box">
  <div class="box-title">Small comment</div>
  <div class="box-content">
    The definition of normal space will be generalized when we will have introduced Riemaniann metrics (see ).
  </div>
</div>

The **normal bundle of $M$**, denoted by $\c{N} M$, is the subset of $\T{}{\bb{R}^n}\approx \bb{R}^n\times \bb{R}^n$ consisting of vectors that are normal to $M$:

$$
    \c{N} M=\{ (x,v)\in \bb{R}^n\times \bb{R}^n:x\in M, \; v\in \c{N}_xM \}.
$$

There is a natural projection $\pi_{\c{N} M}:\c{N} M\to M$ defined as the restriction to $\c{N} M$ of $\pi :\T{}{\bb{R}^n}\to \bb{R}^n$.

<div class="math-box">
  <div class="box-title">Theorem</div>
  <div class="box-content">
    If $M\subseteq \bb{R}^n$ is an embedded $m$-dimensional submanifold, then $\c{N} M$ is an embedded $n$-dimensional submanifold of $\T{}{\bb{R}^n}\approx \bb{R}^n\times\bb{R}^n$.
  </div>
</div>


Thinking of $\c{N} M$ as a submanifold of $\bb{R}^n\times \bb{R}^n$, we define $E:\c{N} M \to \bb{R}^n$ by

$$
    E(x,v) =x+v.
$$

This maps each normal space $\c{N}\_x M$ affinely onto the affine subspace through $x$ and orthogonal to $\T{x}{M}$. Clearly, $E$ is smooth, because it is the restriction to $\c{N} M$ of the addition map $\bb{R}^n\times \bb{R}^n\to \bb{R}^n$. 

A **tubular neighborhood of $M$** is a neighborhood $U$ of $M$ in $\bb{R}^n$ that is the diffeomorphic image under $E$ of an open subset $V\subseteq \c{N} M$ of the form
$$
    V=\{ (x,v)\in \c{N} M : \vert v \vert<\delta(x) \},
$$
for some positive continuous function $\delta :M\to \bb{R}$.

% Add image of what is meant

> Every embedded submanifold of $\bb{R}^n$ has a tubular neighborhood.


A **retraction** of a topological space $X$ onto a subspace $M\subseteq X$ is a continuous map $r:X\to M$ such that $\restr{r}{M}$ is the indentity map of $M$.

Let $M\subseteq \bb{R}^n$ be an embedded submanifold. If $U$ is any tubular neighborhood of $M$, there exists a smooth map $r:U\to M$ that is both a retraction and a smooth retraction.



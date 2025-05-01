---
layout: page
title: Vectors
permalink: /vectors/
exclude: true
---

If $\pi:M\to N$ is any continuous map, a **section of $\pi$** is a continuous right inverse for $\pi$, i.e. a continuous map $\sigma:N\to M$ such that $\pi\circ \sigma : {Id}_N$.

% insert image explaining as in book

A **local section of $\pi$** is a continuous map $\sigma:U\to M$ defined on some open subset $U\subseteq N$ and satisfying the analogous relation $\pi\circ\sigma = {Id}_U$.

<div class="math-box">
  <div class="box-title">Vector Field</div>
  <div class="box-content">
    If $M$ is a smooth manifold with or without boundary, a <strong>vector field on $M$</strong> is a section of the map $\pi :\T{}{M}\to M$. More concretely, a vector field is a continuous map $X:M\to \T{}{M}$, ususally written $p\to X_p$, with the property that

    $$
        \pi\circ X={Id}_M,    
    $$

    or equivalently, $X_p\in \T{p}{M}$ for each $p\in M$.
  </div>
</div>

We are primarely interested in **smooth vector fields**, the ones that are smooth as maps from $M$ to $\T{}{M}$. A **rought vector field on $M$** is a (not necessarily continuous) map $X:M\to \T{}{M}$ satisfying the equation above. Just as for functions, if $X$ is a vector field on $M$, the **support of $X$** is defined to be the closure of the set $\{ p\in M:X_p\neq 0 \}$. A vector field is said to be **compactly supported** if its support is a compact set. 

What follows are a series of statement that follow from the fact that a vector field is defined using derivations (a.k.a. tangent vectors).

- If $X:M\to \T{}{M}$ is a rough vector field and $(U,(x^i))$ is any smooth coordinate chart for $M$, we can write the value of $X$ at any point $p\in U$ in term of the coordinate basis vectors:

    $$
        X_p=X^i(p)\restr{\frac{\partial}{\partial x^i}}{p}.
    $$

    This defines $n$ functions $X^i:U\to \bb{R}$, called the **component functions of $X$** in the given chart.
- Let $M$ be a smooth manifold with or without boundary, and let $X:M\to \T{}{M}$ be a rough vector field. If $(U,(x^i))$ is any smooth coordinate chart on $M$, then the restriction of $X$ to $U$ is smooth if and only if its component functions with respect to this chart are smooth.
- If $(U,(x^i))$ is any smooth chart on $M$, the assignment
    $$
    p\mapsto \restr{\frac{\partial}{\partial x^i}}{p} 
    $$
    determines a vector field on $U$, called the $i$**th coordinate vector field** and denoted by $\partial/\partial x^i$. It is smooth because its component functions are constants.
- The vector field $V$ on $\bb{R}^n$ whose vlaue at $x\in \bb{R}^n$ is 

    $$
    V_x=x^1\restr{\frac{\partial}{\partial x^1}}{x}+ \cdots + x^n\restr{\frac{\partial}{\partial x^n}}{x}
    $$

    is smooth because its coordinate functions are linear. It vanishes at the origin, and points radially outwards everywhere else. It is called **Euler vector field**.
- If $M$ is a smooth  manifold with or without boundary and $A\subseteq M$ is an arbitrary subset, a **vector field along $A$** is a continuous map $X:A\to \T{}{M}$ satisfying $\pi\circ X = {Id}\_A$ (or in other words $X_p\in \T{p}{M}$ for each $p\in A$). We call it a **smooth vector field along $A$** if for each $p\in A$, there is a neighborhood $V$ of $p$ in $M$ and a smooth vector field $\t{X}$ on $V$ that agrees with $X$ on $V\cap A$. 
- Let $M$ be a smooth manifold with or without boundary. Given $p\in M$ and $v\in \T{p}{M}$, there is a smooth global vector field $X$ on $M$ such that $X_p=v$.

<div class="math-box">
  <div class="box-title">To note</div>
  <div class="box-content">
    If $M$ is a smooth manifold with or without boundary, it is standard to use the notation $\c{X}(M)$ to denote the set of all smooth vector fields on $M$. It is a vector space under pointwise addition and scalar multiplication:

    $$
        (aX+bY)_p=aX_p+bY_p.
    $$
  </div>
</div>

Let $M$ be a smooth manifold with or without boudary.
1. If $X$ and $Y$ are smooth vector fields on $M$ and $f,g\in C^{\infty}(M)$, then $fX+gY$ is a smooth vector field.
2. $\c{X}(M)$ is a module over the ring $C^\infty(M)$.
    

Although smooth local frames are plentiful, global ones are not. A smooth manifold with or without boundary is said to be **parallelizable** if it admits a smooth global frame. Parallelizability of $M$ is intimately connected to the question of wheter its tangent bundle is diffeomorphic to the product $M\times \bb{R}^n$. The simplest example of a nonparallelizable manifold is $\bb{S}^2$. It turns out that $\bb{S}^1$, $\bb{S}^3$, and $\bb{S}^7$ are the _only_ spheres that are parallelizable. If $X\in \c{X}(M)$ and $f$ is a smooth real-valued function defined on an open subset $U\subseteq M$, we obtain a new function $Xf:U\to \bb{R}$, defined by
$$
    (Xf)(p)=X_pf.
$$

Let $M$ be a smooth manifold woth or without boundary, and let $X:M\to \T{}{M}$ be a rough vector field. The following are equivalent:
- $X$ is smooth.
- For every $f\in C^\infty(M)$, the function $Xf$ is smooth on $M$.
- For evry open subset $U\subseteq M$ and every $f\in C^\infty(U)$, the function $Xf$ is smooth on $U$.

In general, a map $X:C^\infty(M)\to C^\infty(M)$ is called a **derivation** (as distinct from a _derivation at p_) if it is linear over $\bb{R}$ and satisfies the above equation for all $f,g\in C^\infty(M)$.

Let $M$ be a smooth manifold with or without boundary. A map $D:C^\infty(M)\to C^\infty(M)$ is a derivation if and only if it is of the form $Df=Xf$ for some smooth vector field $X\in \c{X}(M)$.

Because of this result, we sometimes _identify_ smooth vector fields on $M$ with derivations of $C^\infty(M)$, using the same letter for both the vector field (thought of as a smooth map from $M$ to $\T{}{M}$) and the derivation (thought of as a linear map from $C^\infty(M)$ to itself).


**Vector Fields and Smooth Maps**

If $F:M\to N$ is a smooth map and $X$ is a vector field on $M$, then for each point $p\in M$, we obtain a vector $dF_p(X_p)\in \T{F(p)}{N}$ by applying the differential of $F$ to $X_p$. However, this does not in general define a _vector field_ on $N$. For example, if $F$ is not surjective, there is no way to decide what vector to assign to a point $q\in N\setminus F(M)$. If $F$ is not injective, then for some points of $N$ there may be several different vectors obtained by applying $dF$ to $X$ at different points of $M$.

<div class="math-box">
  <div class="box-title">Definition</div>
  <div class="box-content">
    Suppose $F:M\to N$ is smooth and $X$ is a vector field on $M$, and suppose there happens to be a vector field $Y$ on $N$ with the property that for each $p\in M$, $dF_p(X_p)=Y_{F(p)}$. In this case, we say the vector fields $X$ and $Y$ are <strong>$F$-related</strong>.
  </div>
</div>


Suppose $F:M\to N$ is a smooth map between manifold with of without boundary, $X\in \c{X}(M)$, and $Y\in \c{X}(N)$. then $X$ and $Y$ are $F$-related if and only if for every smooth real-valued function $f$ defined on an open subset of $N$,

$$
    X(f \circ F) = (Yf)\circ F.
$$

<div class="math-box">
  <div class="box-title">Proposition</div>
  <div class="box-content">
    Suppose $M$ and $N$ are smooth manifolds with or without boundary, and $F:M\to N$ is a diffeomorphism. For every $X\in \c{X}(M)$, there is a unique smooth vector field on $N$ that is $F$-related to $X$.
  </div>
</div>

In the situation of the preceding proposition we denote the unique vector field that is $F$-related to $X$ by $F_\ast X$, and call it the **pushforward of $X$ by $F$**. Remeber, **it is only when $F$ is a diffeomorphism that $F_\ast X $ is defined**.

Suppose $F:M\to N$ is a diffeomorphism and $X\in \c{X}(M)$. For any $f\in C^\infty(N)$,
$$
    ((F_*X)f)\circ F = X(f\circ F).
$$


If $S\subseteq M$ is an immersed or embedded submanifold (with or without boundary), a vector field $X$ on $M$ does not encessarily restrict to a vector field on $S$, because $X_p$ may not lie in the subspace $\T{p}{S}\subseteq \T{p}{M}$ at a point $p\in S$. Given a point $p\in S$, a vector field $X$ on $M$ is said to be **tangent to $S$ at $p$** if $X_p\in \T{p}{S}\subseteq \T{p}{M}$. It is **tangent to $S$** if it is tangent to $S$ at every point of $S$.

>Let $M$ be a smooth manifold, $S\subseteq M$ be an embedded submanifold with or without boundary, and $X$ be a smooth vector field on $M$. Then $X$ is tangent to $S$ if and only if $(Xf)\vert_S=0$ for every $f\in C^\infty(M)$ such that $f\vert_S \equiv 0$.

>Suppose $S\subseteq M$ is an immersed submanifold with or without boundary, and $Y$ is a smooth vector field on $M$. If there is a vector field $X\in \c{X}(S)$ that is $\imath$-related to $Y$, where $\imath :S \hookrightarrow M$ is the inclusion map, then clearly $Y$ is tangent to $S$, because $Y_p=d\imath_p(X_p)$ is in the image of $d\imath_p$ for each $p\in S$.

>Let $M$ be a smooth manifold, let $S\subseteq M$ be an immersed submanifold with or without boundary, and let $\imath :S\hookrightarrow M$ denote the inclusion map. If $Y\in \c{X}(M)$ is tangent to $S$, then there is a unique smooth vector field on $S$, denoted by $Y\vert_S$, that is $\imath$-related to $Y$.
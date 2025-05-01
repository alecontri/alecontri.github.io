---
layout: page
title: Covectors
permalink: /covectors/
exclude: true
---

Let $V$ be a finite-dimensional vector space. We define a **covector on $V$** to be a real-valued linear functional on $V$, that is, a linear map $\omega:V\to \bb{R}$. The space of all covectors on $V$ is itself a real vector space under the obvious operations of pointwise addition and scalar multiplication. It is denoted by $V^\ast$ and called the **dual space of $V$**.


Let $V$ a finite-dimensional vector space. Given any basis $(E_1,\dots, E_n)$ for $V$, let $\varepsilon^1,\dots,\varepsilon^n\in V^\ast$ be the covectors defined by
$$
    \varepsilon^i(E_j)=\delta_j^i.
$$
Then $(\varepsilon^1,\dots,\varepsilon^n)$ is a basis for $V^*$, called the **dual basis to $(E_j)$**. Therefore, $\dim V^\ast=\dim V$.

We can express an arbitrary covector $\omega \in V^\ast$ in terms of the dual basis as
$$
    \omega = \omega_i\varepsilon^i,
$$
where the components are determined by $\omega_i=\omega(E_i)$. The action of $\omega$ on a vector $v=v^jE_j$ is
$$
    \omega(v)=\omega_iv^i.
$$
Suppose $V$ and $W$ are vector spaces and $A:V\to W$ is a linear map. We define a linear map $A^\ast:W^\ast\to V^\ast$, called the **dual map** or **transpose of $A$**, by
$$
    (A^*\omega)(v) = \omega(Av) \quad \text{for } \omega\in W^*,\;v\in V.
$$


The dual map satisfies the following properties:
- $(A\circ B)^\ast=B^\ast\circ A^\ast$.
- $(Id_V)^\ast:V^\ast\to V^\ast$ is the identity map of $V^\ast$.


Apart from the fact tha the dimenaion of $V^\ast$ is the same as that of $V$, the second most important fact about dual spaces is the following characterization of the **second dual space** $V^{\ast\ast}=(V^\ast)^\ast$. For each vector space $V$ there is a natural, basis independent map $\xi:V\to V^{\ast}$, defined as follows. For each vector $v\in V$, define a linear functional $\xi(v):V^*\to \bb{R}$ by
$$
    \xi(v)(\omega)=\omega(v) \quad \text{for } \omega\in V^*.
$$

For any finite-dimensional vector space $V$, the map $\xi:V\to V^{\ast\ast}$ is an isomorphism.

When $V$ is finite dimensional, we can unambigously identify $V^{\ast\ast}$ with $V$ itself, because the map $\xi$ is canonically defined, without reference to any basis. It is important that although $V^\ast$ is also isomorphic to $V$ (for the simple reasonthat any two finite-dimensional vector spaces of the same dimension are isomorphic), ther is no _canonical_ isomorphism $V\cong V^\ast$.

**Tangent covectors**

For each $p\in M$, we define the **cotangent space at $p$**, denoted by $\cT{p}{M}$, to be the dual space to $\T{p}{M}$:
$$
    \cT{p}{M} =(\T{p}{M})^\ast.
$$
Elements of $\cT{p}{M}$ are called **tangent covectors at $p$**, or just **covectors at $p$**.

In the early days of smooth manifold theory, mathematicians tended to think of a tangent vector at a point $p$ as an assignment of an $n$-tuple of real numbers to each smooth coordinate system, with the property that the $n$-tuples $(v^1,\dots,v^n)$ and $(\t{v}^1,\dots,\t{v}^n)$ assigned to two different coordinate systems $(x^i)$ and $(\t{X}^j)$ were related by the transformation laws
$$
    \t{v}^j=\frac{\partial \t{x}^j}{\partial x^i}(p)v^i.
$$

Similarly, a tangent covector was thought of as an $n$-tuple $(\omega_1,\dots,\omega_n)$ that ransforms according to the following slightly different rule:

$$
    \omega_i=\frac{\partial \t{x}^j}{\partial x^i}(p)\t{\omega}_j.
$$

Since coordinate vector fields transform as

$$
    \restr{\frac{\partial}{\partial x^i}}{p}=\frac{\partial \t{x}^j}{\partial x^i}(p)\restr{\frac{\partial}{\partial \t{x}^j}}{p}
$$

by simple application of the chain rule, this transformation rule was considered as fundamental. Thus it became customary to call tangent covectors **covariant vectors** because their components transform in the same way as the coordinate partial derivatives, with the Jacobian matrix $(\partial\t{x}/\partial x^i)$ multiplying the objects associated with the "new" coordinates $(\t{x}^j)$ to obtain those associated with the "old" coordinates $(x^i)$. Analogously, tangent vectors were called **contravariant vectors** because their components transform in the opposite way. Note that this use of the terms covariant and contravariant has nothing to do with the covariant and contravariant functors of category theory.

%% Link to the 'pushforward' (derivation) for vector fields and the fact that I need the inverse

**Covector Fields**

For any smooth manifold $M$ with or without boundary, the disjoint union

$$
\cT{}{M}=\coprod_{p\in M} \cT{p}{M}
$$

is called the **cotangent bundle of $M$**. It has a natural projection map $\pi:\cT{}{M} \to M$ sending $\omega\in \cT{p}{M}$ to $p\in M$. As above, given any smooth local coordinates $(x^i)$ on an open subset $U\subset M$, for each $p\in U$ we denote the basis for $\cT{p}{M}$ dual to $(\restr{\partial/\partial x^i}{p})$ by $(\restr{\lambda^i}{p})$. This defines $n$ maps $\lambda^1,\ldots, \lambda^n:U\to \cT{}{M}$, called **coordinate covector fields**.

> Let $M$ be a smooth $n$-manififold with or without boundary. With its standard projection map and the natural vector space structure of each fiber, the cotangent bundle $\cT{}{M}$ has a unique topology and a smooth structure making it into a smooth rank-$n$ vector bundle over $M$ for which all coordinate fields are smooth local sections.

As in the case of the tangent bundle, smooth local coordinates for $M$ yield smooth local coordinates for its cotangent bundle. If $(x^i)$ are smooth local coordinates on an open subset $U\subset M$, the map $\pi^{-1}(U)$ to $\bb{R}^{2n}$ given by

$$
\restr{\xi_i\lambda^i}{p}\to (x^1(p),\ldots,x^n(p),\xi_1,\ldots,\xi_n)
$$

is a smooth coordinate chart for $\cT{}{M}$. We call $(x^i,\xi_i)$ the **natural coordinates for $\cT{}{M}$** associated with $(x^i)$.

A (local or global) section of $\cT{}{M}$ is called a **covector field** or a **differential 1-form** (see %%%%%).

In any smooth local coordinates on an open subset $U\subset M$, a (rough) covector field $\omega$ can be written in terms of the coordinate covector fields $(\lambda^i)$ as $\omega =\omega_i\lambda^i$ for $n$ functions $\omega_i:U\to \bb{R}$ called the **component functions of $\omega$**. They are characterized by

$$
\omega_i(p)=\omega_p\left(\restr{\frac{\partial}{\partial x^i}}{p}\right)
$$

<div class="math-box">
  <div class="box-title">Side comment</div>
  <div class="box-content">
    If $\omega$ is a (rough) covector field and $X$ is a vector field on $M$, then we can form a function $\omega(X):M\to \bb{R}$ by

    $$
    \omega(X)(p)=\omega_p(X_p), \quad p\in M
    $$

    If we write $\omega=\omega_i\lambda^i$ and $X=X^j\partial/\partial x^j$ in terms of local coordinates, then $\omega(X)$ has the local coordinate representation $\omega(X)=\omega_iX^i$.
  </div>
</div>

Given a local frame $(E_1,\ldots,E_n)$ for $\T{}{M}$ over an open subset $U$, there is a uniquely determined (rough) local coframe $(\varepsilon^1,\ldots,\varepsilon^n)$ over $U$ such that $(\restr{\varepsilon^i}{p})$ is the dual basis to $(\restr{E_i}{p})$ for each $p\in U$, or equivalently $\varepsilon^i(E_j)=\delta_j^i$. This coframe is called the **coframe dual to ($E_i$)**. The same holds vice-versa and I get, from the coframe, the **frame dual to $(\varepsilon^i)$**.

> Given a smooth coframe $(\varepsilon^i)$, a covector $\omega$ is smooth if and only if its components functions with respect to $(\varepsilon^i)$ are smooth.

We denote the real vector space of all smooth covector fields on $M$ by $\c{X}^\ast(M)$.

<div class="math-box">
  <div class="box-title">Definition of differential (again)</div>
  <div class="box-content">
    Let $f$ be a smooth real-valued function on a smooth manifold $M$ with or without boundary. We define a covector field, called the **differential of $f$**, by

    $$
    df_p(v)=vf, \quad \text{for } v\in \T{p}{M} 
    $$
  </div>
</div>
> The differential of a smooth funciton is a smooth covector field.

Applying the definition in coordinates, one can see that: **the coordinate covector field $\lambda^i$ is none other than the differential $dx^i$!!!**

From now on we will thus just drop the notation $\lambda^i$ and use $dx^i$.

%%% Insert example

You may have noticed that for a a smooth real-valued function $f:M\to\bb(R)$, we have two different definitions for the differential of $f$ at a point $p\in M$:
- as linear map between tangent spaces $\T{p}{M}\to \T{f(p)}{\bb{R}}$
- as covector at $p$, i.e. linear map between $\T{p}{M} \to \bb{R}$.
These are actually the same objec once taken into account the canonical identification between $\bb{R}$ and its tangent space $\T{f(p)}{\bb{R}}$.

**Pullbacks of covector fields**

As we have seen, a smooth map yields a linear map on tangent vectors called the differential. Dualizing this leads to a linear map on covectors going in the opposite direction.

Let $F:M\to N$ be a smooth map between smooth manifolds with or without boundary, and let $p\in M$ be arbitrary. The differential $dF_p:\T{p}{M}\to \T{F(p)}{N}$ yields a dual linear map

$$
dF_p^\ast:\cT{F(p)}{N}\to \cT{p}{M},
$$

called the (**pointwise**) **pullback by $F$ at $p$**, or the **cotangent map of $F$**. Unraveling the definitions, we see that $dF_p^\ast$ is characterized by

$$
dF_p^\ast(\omega)(v)=\omega(dF_p(v)), \quad \text{for }\omega\in \cT{F(p)}{N}, \; v\in\T{p}{M}.
$$

As we have seen, the pushforwards of vector fields under smooth maps are defined only in the special cases of diffeomorphism or Lie group homeomorphism. The surprising thing abut covectors is that **covector fields *always* pull back to covector fields**.

Given a smooth map $F:M\to N$ and a covector field $\omega$ on $N$, defone a rough covector field $F^\ast\omega$ on $M$, called **pullback of $\omega$ by $F$**, by

$$
(F^\ast\omega)_p=dF_p^\ast(\omega_{F(p)}).
$$

It acts on a vector $v\in \T{p}{M}$ by

$$
(F^\ast\omega)_p(v)=\omega_{F(p)}(dF_p(v)).
$$

<div class="math-box">
  <div class="box-title">Proposition</div>
  <div class="box-content">
    Let $F:M\to N$ be a smooth map between smooth manifolds with or without boundary. Suppose $u$ is a continuous real-valued funciton on $N$, and $\omega$ is a covector field on $N$. Then

    $$
    F^\ast(u\omega)=(u\circ F)F¨\ast\omega
    $$

    If in addition $u$ is smooth, then

    $$
    F^\ast du = d(u\circ F).
    $$
  </div>
</div>

<div class="math-box">
  <div class="box-title">Proposition</div>
  <div class="box-content">
    Suppose $F:M\to N$ is a smooth map between smooth manifolds with or without boundary, and let $\omega$ be a covector field on $N$. Then $F^\ast\omega$ is a (continuous) covector field on $M$. If $\omega$ is smooth, then so is $F^\ast\omega$.
  </div>
</div>

%%%%% put exercises to show how it works in practice

----
<br>

**Restricting covector fields to submanifolds**

Suppose $M$ is a smooth manifold with or without boundary, $S\subset M$ is an immersed submanifold with or without boundary, and $\i :S\hookrightarrow M$ is the inclusion map. If $\omega$ is any smooth covector field on $M$, the pullback by $\i$ yields a smooth covector field $\i^\ast\omega$ on $S$. To see what this means, let $v\in\T{p}{S}$ be arbitrary, and compute

$$
(\i^\ast\omega)_p(v)=\omega_p(d\i_p(v))=\omega_p(v),
$$

since $d\i_p:\T{p}{S}\to \T{p}{M}$ is just the inclusion map, under our usual identification of $\T{p}{S}$ with a subspace of $\T{p}{M}$. Thus, $\i^\ast\omega$ is just the restriction of $\omega$ to vetors tangent to $S$. However, $\i^\ast\omega$ might equal zero at a given point of $S$, even though considered as a covector field on $M$, $\omega$ might not vanish there.

%%%% Insert example

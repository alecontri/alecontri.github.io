---
layout: page
title: Tangent Space
permalink: /tangent_space/
exclude: true
---

% Summary missing: tangent space (needed for both submanifolds and vector fields etc) and the differential

***Tangent space***

Let $M$ be a manifold with or without boundary. For every point $p\in M$, a **tangent vector at $p$** is a linear map $v:C^\infty\to \bb{R}$ that is a **derivation** at $p$, meaning that for all $f,g\in C^\infty(M)$ it satisfies the product rule

$$
v(fg)=f(p)vg+g(p)vf
$$

The set of all tangent vectors at $p$ is denoted $\T{p}{M}$ and called the **tangent space at $p$**.

<div class="math-box">
  <div class="box-title">To note</div>
  <div class="box-content">
    <ul>
        <li> In the above definition we can recognize properties of the classical 'derivative'. For example, given a smooth manifold $M$ (with or without boundary), a derivation $v\in \T{p}{M}$ and a function $f\in C^\infty(M)$ then if $f$ is constant, $vf=0$; </li>
        <li> Suppose $M$ is a $n$-dimensional manifold (with of without boundary). Then for each $p\in M,~\T{p}{M}$ is a $n$-dimensional vector space.</li>
    </ul>
  </div>
</div>

Suppose $M$ is $n$-dimensional and $\phi:U\to\hat{U}\subset \bb{R}^n$ is a smooth coordinate chart on some open subset $U\subset M$. Writing the coordinate functions of $\phi$ as $(x^1,\ldots,x^n)$, we define the _coordinate vectors_ $\restr{\frac{\partial}{\partial x^1}}{p},\ldots,.\restr{\frac{\partial}{\partial x^n}}{p}$ by

$$
\restr{\frac{\partial}{\partial x^1}}{p} f=\restr{\frac{\partial}{\partial x^1}}{\phi(p)} (f\circ \phi^{-1})
$$

<div class="math-box">
  <div class="box-title">Explanation</div>
  <div class="box-content">
    It was really cumbersome for me to interpret this the first time, so here is an un-asked explanation.

    Start from the right. We have a function $\t{f}:~ f\circ \phi^{-1}$, which is a function from $\bb{R}^n$ to $\bb{R}$. We differentiate it along the coordinate $x_1$: this gives a second function with values in $\bb{R}$. Then we compute the value of this function at $\phi(p)$, which is a point in $\bb{R}^n$.
     
    Now interpret $\frac{\partial}{\partial x^1}$ purely as a symbol. This symbol is a linear map (a derivation) that lives in $\T{p}{M}$ and acts of the function $f$, which lives in $M$, giving as output a number for every point $p$. This number must be always equal to the number we obtained before on the left hand side. This <strong>defines</strong> the derivation $\frac{\partial}{\partial x^1}$ and all the others similarly.
  </div>
</div>

These coordinate vectors form a basis for $\T{p}{M}$, which therefore has dimension $n$. Thus once a smooth coordinate chart has been chosen, every tangent vector $v\in \T{p}{M}$ can be written uniquely in the form

$$
v=v^i\restr{\frac{\partial}{\partial x^i}}{p}=v^1\restr{\frac{\partial}{\partial x^1}}{p}+\dots+v^n\restr{\frac{\partial}{\partial x^n}}{p}
$$

where the components $v^1,\ldots, v^n$ are obtained by applying $v$ to the coordinate functions: $v^i=v(x^i)$.

<div class="math-box">
  <div class="box-title">Remark</div>
  <div class="box-content">
    On a finite-dimensional vector space $V$ with its standard smooth manifold structure, there is a natural (basis-independent) identification of each tangent space $\T{p}{V}$ with $V$ itself. In terms of coordinates $(x^i)$ induced on $V$ by any basis, this is the correspondance $(v^1,\ldots,v^n)\iff \sum_iv^i\restr{\frac{\partial}{\partial x^i}}{p}$.
  </div>
</div>

----
<br>

***The differential***

Now if we are given two manifolds $M$ and $N$, it makes no sense to talk about linear maps between them, but it makes sense to talk about linear maps between their tangent spaces $\T{p}{M}$ and $\T{p}{N}$ since they are both vector spaces.

<div class="math-box">
  <div class="box-title">Definition of Differential</div>
  <div class="box-content">
    If $F:M\to N$ is a smooth map and $p$ is any point in $M$, we define a linear map $dF_p:\T{p}{M}\to \T{F(p)}{N}$, called the <strong>differential of $F$ at $p$</strong>, by

    $$
    dF_p(v)f=v(f\circ F), \; v\in \T{p}{M}, ~\forall f\in C^\infty(N).
    $$
  </div>
</div>

Once we have chosen local coordinates $(x^i)$ for $M$ and $(y^i)$ for $N$, we find by unwinding the definitions that the coordinate representation of the differential is given by the **Jacobian matrix** of the coordinate representation of $F$, which is its matrix of first-order derivatives:

$$
dF_p\left( \restr{v^i\frac{\partial}{\partial x^i}}{p} \right) = \frac{\partial F^j}{\partial x^i}(p)v^i\restr{ \frac{\partial}{\partial y^j}}{F(p)}.
$$

<div class="math-box">
  <div class="box-title">Un-asked explanation</div>
  <div class="box-content">
    The image of $dF_p(v)$ is a tangent vector of $N$. As seen before for $M$, it can be expressed as sum of basis functions for the tangent space $\T{F(p)}{N}$, i.e. $dF_p(v)=w_j\restr{\frac{\partial}{\partial y^j}}{F(p)}$ for some coefficients $w_j$. What are these coefficients? I apply the definition to a coordinate tangent vector:
    $$
    dF_p\left( \restr{v^i\frac{\partial}{\partial x^i}}{p} \right) f = v^i\restr{ \frac{\partial}{\partial x^i}}{p}(f\circ F)= v^i \sum_j\restr{\frac{\partial}{\partial y^j}}{\t{p}} f(\t{p})\restr{\frac{\partial}{\partial x^i}}{p} F_j(p)
    $$
    where $\t{p}=F(p)$ and the product rule has been used.
  </div>
</div>

%% Exercise: prove that differential of identity is identity and that differential of composition is composition of differentials.

For every $p\in M$, the dual vector space to $\T{p}{M}$ is called the **cotangent space** at $p$. This is the space $\cT{p}{M}=(\T{p}{M})^\ast$ of real-valued linear functionals on $\T{p}{M}$, called (**tangent**) **covectors at $p$**. For every $f\in C^\infty(M)$ and $p\in M$, there is a covector $df_p\in \cT{p}{M}$ called the **differential of $f$ at $p$**, defined by

$$
df_p(v)=vf \text{ for all } v\in \T{p}{M}.
$$

In the differential geometry literature, the differential is sometimes called the **tangent map**, the **total derivative**, or simply the **derivative of $F$**. Becasue it "pushes" tangent vectors forward from the domain manifold to the codomain, it is also called the **(pointwise) pushforward**.

<div class="math-box">
  <div class="box-title">Note</div>
  <div class="box-content">
    The pushforward can be seen as a special case of differential where $F$ takes values in $\bb{R}$.
  </div>
</div>

Suppose $(U,\phi)$ and $(V, \psi)$ are two smooth charts on $M$, and $p\in U\cap V$. Let us denote the coordinate functions of $\phi$ by $(x^i)$ and those of $\psi$ by $(\tilde{x}^i)$. Any tangent vector at $p$ can be represented with respect to either basis $(\partial/\partial x^i\vert_p)$ or $(\partial/\partial \tilde{x}^i\vert_p)$. The two representations are related by

$$
    \restr{\frac{\partial}{\partial x^i}}{p}=\frac{\partial\tilde{x}^j}{\partial x^i}(\phi(p))\restr{\frac{\partial}{\partial\tilde{x}^j}}{p}
$$

This transformation rule was considered as fundamental. Thus it became customary to call tangent covectors **covariant vectors** because their components transform in the same way as the coordinate partial derivatives, with the Jacobian matrix $(\frac{\partial \t{x}}{\partial {x}^i})$ multiplying the objects associated with the ”new” coordinates $(\t{x}^j)$ to obtain those associated with the ”old" coordinates $(x^i)$. Analogously, tangent vectors were called contravariant vectors because their
components transform in the opposite way.

----
<br>

***The Tangent Bundle***

Given a smooth manifold $M$ with or without boundary, we define the **tangent bundle of $M$**, denoted by $\T{}{M}$, to be the disjoint union of the tangent spaces at all points of $M$:
$$
   \T{}{M}= \coprod_{p\in M} \T{p}{M}
$$
The tangent bundle comes equipped with a natural **projection map** $\pi:\T{}{M}\to M$, which sends each vector in $\T{p}{M}$ to the point $p$ at which it is tangent: $\pi(p,v)=p$.
If $M$ is a smooth manifold, the tangent bundle $\T{}{M}$ can be thought of simply as a dsjoint union of vector spaces; but it is much more than that.

By putting together the differentials of $F$ at all points of $M$, we obtain a globally defined map between tangent bundles, called the **global differential** or **global tangent map** and denoted by $dF : \T{}{M} \to \T{}{N}$.


>If $F:M\to N$ is a smooth map, then its global differential $dF:\T{}{M}\to \T{}{N}$ is a smooth map.

Suppose $F:M\to N$ and $G:N\to P$ are smooth maps.
* $d(G\circ F)=dG\circ dF$
* $d(id_M)=id_{\T{}{M}}$
* If $F$ is a diffeomorphism, then $dF:\T{}{M} \to \T{}{N}$ is also a diffeomorphism, and $(dF)^{-1}=d(F^{-1})$

***Alternative Definitions of Tangent Space***

Tangent spaces can be defined in different ways, all with their advantages and disadvantages:
- Definition using spaces of germs of derivations of $C^{\infty}$ functions. It makes clearer the local nature of the tangent space without requiring bump functions. It is the only definition available for real-analytic or complex-analytic manifolds. The drawback is that it adds an additional level of complication to an already highly abstract definition.
- Definition as equivalence classes of curves. It makes easy to define the differential of a smooth map and it is more gemoetrically intuitive. It has the serious drawback that the existence of a vector space structure is not obvious.
- Definition as equivalence class of $n$-tuples. The first definition of all. It is similar to the Euclidean approach but requires tedious computations involving the chain rule to show that the operation are independent on the choice of coordinates.



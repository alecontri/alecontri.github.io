---
layout: page
title: Tensors 
permalink: /tensors/
exclude: true
---

Suppose $V_1\ldots, V_k$, and $W$ are vector spaces. A map $F:V_1\times\ldots\times V_k\to W$ is said to be **multilinear** if it is linear as a function of each variable separately when the others are held fixed: for each $i$,

$$
F(v_1,\ldots,av_i+a'v_i',\ldots, v_k) = a F(v_1,\ldots,v_i,\ldots, v_k) + a'F(v_1,\ldots,v_i',\ldots, v_k)
$$

> The set of all multilinear maps from $V_1\times\ldots\times V_k$ to $W$, indicated as $L(V_1,\ldots, V_k; W)$ is a vector space under the usual operations of pointwise addition and scalar multiplication:   
>$$
(F+F')(v_1,\ldots,v_k)=F(v_1,\ldots,v_k)+F'(v_1,\ldots,v_k)
$$
$$
(aF)(v_1,\ldots,v_k)a(F(v_1,\ldots,v_k))
$$

<div class="math-box">
  <div class="box-title">Examples of multilinear functions</div>
  <div class="box-content">
    <ul>
        <li> the dot product</li>
        <li> the cross product</li>
        <li> the determinant</li>
        <li> the brakets in Lie algebra</li>
    </ul>
  </div>
</div>

Suppose $V$ is a vector space, and $\omega,\eta\in V^\ast$. Define a function $\omega\otimes \eta: V\times V\to \bb{R}$ by

$$
    \omega\otimes\eta(v_1,v_2)=\omega(v_1)\eta(v_2)
$$

The linearity of $\omega$ and $\eta$ guarantees that $\omega\otimes\eta$ is a bilinear function of $v_1$ and $v_2$, so $\omega\otimes\eta$ is itself a multilinear map.

The above cna be generalized to arbitrary real-valued multilinear functions as follow: let $V_1,\ldots, V_k,W_1, \ldots,W_l$ be real vector spaces, and suppose $F\in L(V1,\ldots,V_k;\bb{R})$ and $G\in L(W_1,\ldots,W_l;\bb{R})$. Define a function

$$
F\otimes G: V_1\times\ldots V_k\times W_1\times\ldots W_l \to \bb{R}
$$

by

$$
F\otimes G (v_1,\ldots, v_k,w_1,\ldots,w_l)=F(v_1,\ldots,v_k)G(w_1,\ldots,w_l)
$$
> $F\otimes G$ is an element of $L(V_1,\ldots,V_k,W_1,\ldots,W_l;\bb{R})$, called the **tensor product of $F$ and $G$**.

<div class="math-box">
  <div class="box-title">Proposition</div>
  <div class="box-content">
    Let $V_1,\ldots, V_k$ be real vector spaces of dimensions $n_1,\ldots, n_k$, respectively. For each $j\in \{1, \ldots, k\}$, let $(E_1^{(j)}, \ldots, E_{n_j}^{(j)})$ be a basis for $V_j$, and let $(\varepsilon_{(j)}^1,\ldots,\varepsilon_{(j)}^{n_j})$ be the corresponding dual basis for $V_j^\ast$. Then the set

    $$
    \c{B}=\{ \varepsilon_{(1)}^{i_1}\otimes\ldots\otimes\varepsilon_{(k)}^{i_k} :1\leq i_1\leq n_1,\ldots,1\leq i_k\leq n_k \}
    $$

    is a basis for $L(V_1,\ldots,V_k;\bb{R})$, which therefore has dimension equal to $n_1\cdots n_k$.
  </div>
</div>

<br>

_Covariant and Contrariant Tensors on a Vector Space_

Let $V$ be a finite-dimensional real vector space. If $k$ is a positive integer, a **covariant $k$-tensor on $V$** is an element of the $k$-fold tensor product $V^\ast\otimes\cdot\otimes V^\ast$, which we typically think of as a real-valued multiliear function of $k$ elements of $V$:

$$
\alpha : \underbrace{V\times\cdots\times V}_{k \text{ copies}} \to \bb{R}.
$$

The number $k$ is called the **rank of $\alpha$**. A $0$-tensor is, by convention, just a real number (a real-valued funciton depending multilinearly on no vectors!). We denote the vector space of all covariant $k$-tensors on $V$ by the shorthand notation

$$
T^k(V^\ast)= \underbrace{V^\ast\otimes \cdots \otimes V^\ast}_{k \text{ copies}}.
$$

<div class="math-box">
  <div class="box-title">Examples</div>
  <div class="box-content">
    <ul>
        <li> Every linear functional $\omega:V\to \bb{R}$ is multilinear, so a covariant 1-tensor is just a covector. Thus, $T^1(V^\ast)$ is equal to $V^\ast$.</li>
        <li> A covariant 2-tensor on $V$ is a real-valued bilinear funciton of two vectors, also called a **bilinear form**. One example is the dot product on $\bb{R}^n$. More generally, every inner product is a covariant 2-tensor.</li>
        <li> The determinant, thought of as a function of $n$ vectors, is a covariant $n$-tensor on $\bb{R}^n$.</li>
    </ul>
  </div>
</div>

For any finite-dimensional real vector space $V$, we define the space of **contravariant tensors on $V$ of rank $k$** to be the vector space

$$
T^k(V) = \underbrace{V\otimes\cdots\otimes V}_{k \text{ copies}}.
$$

In particular, $T^1(V)=V$, and by convention $T^0(V)=\bb{R}$. Beacuse we are assuming that $V$ is finite-dimensional, it is possible to identify this space with the set of multilinear functions of $k$ covectors:

$$
T^k(V) \cong \{\text{multilinear funcitons }\alpha: \underbrace{V^\ast\times\cdot\times V^\ast}_{k \text{ copies}}\to \bb{R}\}
$$

Even more generally, for any nonnegative integers $k,l$, we define the space of **mixed tensors on $V$ of tyoe $(k,l)$** as 

$$
T^{(k,l)}(V)=\underbrace{V\otimes\cdots\otimes V}_{k \text{ copies}}\otimes\underbrace{V^\ast\otimes\cdots\otimes V^{\ast}}_{l \text{ copies}}
$$

Some of these spaces are identical:

$$
\begin{aligned}
    &T^{(0,0)}(V)=T^0(V^\ast)=T^0(V)=\bb{R}, \\
    &T^{(0,1)}(V)=T^1(V^\ast)=V^\ast, \\
    &T^{(1,0)}(V)=T^1(V)=V, \\
    &T^{(0,k)}(V)=T^k(V^\ast), \\
    &T^{(k,0)}(V)=T^k(V).
\end{aligned}
$$

<br>

_Symmetric Tensors_

Let $V$ be a finite-dimensional vector space. A convariant k-tensor $\alpha$ on $V$ is said to be **symmetric** if its value is unchanged by interchanging any pair of arguments:

$$
\alpha(v_1,\ldots,v_i,\ldots,v_j,\ldots,v_k)=\alpha(v_1,\ldots,v_j,\ldots,v_i,\ldots,v_k)
$$

whenever $1\leq i < j \leq k$.

Let $S_k$ denote the **symmetric group on $k$ elements**, that is, the group of permutations of the set $\{1,\ldots,k\}$. Given a $k$-tensor $\alpha$ and a permutation $\sigma\in S_k$, we define a new $k$-tensor ${}^\sigma\alpha$ by

$$
{}^\sigma \alpha(v_1,\ldots,v_k) = \alpha(v_{\sigma(1)},\ldots,v_{\sigma(k)})
$$

We define a projection $\sym: T^k(V^\ast)\to \Sigma^k(V^\ast)$ called **symmetrization** by

$$
\sym \alpha = \frac{1}{k!}\sum_{\sigma\in S_k}{}^\sigma\alpha.
$$

More explicitly:

$$
(\sym \alpha)(v_1,\ldots,v_k)=\frac{1}{k!}\sum_{\sigma\in S_k}\alpha(v_{\sigma(1)},\ldots,v_{\sigma(k)})
$$

If $\alpha$ and $\beta$ are symmetric tensors on $V$, then $\alpha\otimes\beta$ is not symmetric in general. However, using the symmetrization operator, it is possible to define a new product that takes a pair of symmetric tensors and yields another symmetric tensor. If $\alpha\in \Sigma^k(V^\ast)$ and $\beta\in\Sigma^l(V^\ast)$, we define their **symmetric product** to be the $(k+l)$-tensor $\alpha\beta$ given by

$$
\alpha\beta = \sym (\alpha\otimes\beta)
$$

Explicitly

$$
\alpha\beta(v_1,\ldots,V_{k+l}) = \frac{1}{(k+l)!}\sum_{\sigma\in S_{k+l}}\alpha(v_{\sigma(1)},\ldots,v_{\sigma(k)})\beta(v_{\sigma(k+1)},\ldots,v_{\sigma(k+l)})
$$

<br>

_Alternating Tensors_

We assume that $V$ is a finite-dimensional real vector space. A covariant $k$-tensor $\alpha$ on $V$ is said to be **alternating** (or **antisymmetric** or **skew-symmetric**) if it changes sign whenever two of its arguments are interchanged. This means that for all vectors $v_1,\ldots,v_k\in V$ and every pair of distinct indices $i,j$ it satisfies

$$
\alpha(v_1,\ldots,v_i,\ldots,v_j,\ldots,v_k)=-\alpha(v_1,\ldots,v_j,\ldots,v_i,\ldots,v_k).
$$

Alternating covariant $k$-tensors are also variously called **exterior forms, multilinear covectors**, or **$k$-covectors**. The subspace of all alternating covariant $k$-tensors on $V$ is denoted by $\Lambda^k(V^\ast)\subseteq T^k(V^\ast)$.

> Recall that the **sign of $\sigma$**, denoted by $\sgn\sigma$, is equal to $+1$ if $\sigma$ is even and $-1$ if $\sigma$ is odd.

> Every $0$-tensor is both symmetric and alternating. Similarly, every $1$-tensor is both symmetric and alternating.

---

<br>


**Tensors ans Tensor Fields on Manifilds**

Let $M$ be a smooth manifold with or without boundary. We define the **bundle of covariant $k$-tensors on $M$** by

$$
T^k\cT{}{M}=\prod_{p\in M}T^k(\cT{p}{M})
$$

Analogously, the **bundle of contraviariant $k$-tensors** is defined by

$$
T^k\T{}{M}=\prod_{p\in M}T^k(\T{p}{M})
$$

and the **bundle of mixed tensors of type $(k,l)$** by

$$
T^{(k,l)}\T{}{M}=\prod_{p\in M}T^{(k,l)}(\T{p}{M})
$$

Any one of thes ebundles is called a **tensor bundle over $M$**. A section of a tensor bundle is called a **(covariant, contravariant, or mixed) tensor field on $M$**. A **smooth tensor field** is a section that is smooth in the usual sense of smooth sections of vector bundles.

Since smooth covariant tensor fields are of particular interest for us, we introduce the notation for the space of all smooth covariant $k$-tensor fields:

$$
\TT{k}{M} = \Gamma(T^k\cT{}{M})
$$

where $\Gamma$ indicates the space of sections of the tensor bundle indicated.

%%%% maybe mention smoothness properties

A symmetric tensor field on a manifold (with or without boundary) is simply a covariant tensor field whose value at each point is a symmetric tensor. The symmetric product of two or more tensor fields is defined pointwise, just like the tensor product.

Alternating tensor filds are called **differetial forms**, we will study them in another section.

**Pullbacks of tensor fields**

Just like covector fields, covariant tensor fields can be pulled back by a smooth map to yield tensor fields on the domain. The reason why we focus on the covariant case is that this contruction works only in this case.

Suppose $F:M\to N$ is a smooth map. For any point $p\in M$ and any $k$-tensor $\alpha\in T^k(\cT{F(p)}{N})$, we define a tensor $dF_p^\ast(\alpha)\in T^k(T_p^\ast M)$, called the **pointwise pullback of $\alpha$ by $F$ at $p$**, by

$$
dF_p^\ast(\alpha)(v_1,\ldots,v_k)=\alpha(dF_p(v_1)\ldots,dF_p(v_k))
$$

for any $v_1,\ldots,v_k\in \T{p}{M}$. If $A$ is a covariant $k$-tensor field on $N$, we define a rough $k$-tensor field $F^\ast A$ on $M$, called the **pullback of $A$ by $F$**, by

$$
(F^\ast A)_p=dF_p^\ast(A_{F(p)})
$$

This tensor field acts on vectors $v_1,\ldots, v_k\in \T{p}{M}$ by

$$
(F^\ast A)_p(v_1,\ldots,v_k)=A_{F(p)}(dF_p(v_1),\ldots,dF_p(v_k))
$$

<div class="math-box">
  <div class="box-title">Properties of tensor pullbakcs</div>
  <div class="box-content">
  Suppose $F:M\to N$ and $G:N\to P$ are smooth maps. $A$ and $B$ are covariant tensor fields on $N$, and $f$ is a real-valued function $N$.
    <ul>
        <li> $F^\ast(fB)=(f\circ F)F^\ast B$. </li>
        <li> $F^\ast(A \otimes B)=F^\ast A \otimes F^\ast B$. </li>
        <li> $F^\ast (A+B)= F^\ast A + F^\ast B$. </li>
        <li> $F^\ast B$ is a (continuous) tendor field, and is smooth if $B$ is smooth. </li>
        <li> $(G\circ F)^\ast B = F^\ast (G^\ast B)$. </li>
        <li> $(\text{Id}_N)^\ast B = B$. </li>
    </ul>
  </div>
</div>

<div class="math-box">
  <div class="box-title">Corollary</div>
  <div class="box-content">
  Let $F:M\to N$ be smooth, and let $B$ be a covariant $k$-tensor field on $N$. If $p\in M$ and $(y^i)$ are smooth coordinates for $N$ on a neighborhood of $F(p)$, then $F^\ast B$ has the following expression in a neighborhood of $p$:

  $$
    F^\ast(B_{i_1\ldots i_k} dy^{i_1}\otimes\ldots\otimes dy^{i_k}) = (B_{i_1\ldots i_k}\circ F) d(y^{i_1}\circ F)\otimes \cdots \otimes d(y^{i_k}\circ F)
  $$
  </div>
</div>

In words the above just says that $F^\ast B$ is computed by the same technique used to compute the pullback of a covector field.
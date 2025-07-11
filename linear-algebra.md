---
# You can also start simply with 'default'
theme: seriph
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: https://www.loliapi.com/acg/pc/
# some information about your slides (markdown enabled)
title: Linear Algebra in OI
# apply unocss classes to the current slide
class: text-center
# https://sli.dev/features/drawing
drawings:
  persist: false
# slide transition: https://sli.dev/guide/animations.html#slide-transitions
transition: slide-left
# enable MDC Syntax: https://sli.dev/features/mdc
mdc: true
# enable download-as-pdf with clicks
download: true
---

# Linear Algebra in OI

Dongwu Chen (PKU EECS)

<div @click="$slidev.nav.next" class="mt-12 py-1" hover:bg="white op-10">
  Press Space for next page <carbon:arrow-right />
</div>

<div class="absolute bottom-2 left-2 text-xs">
  {{ new Date().toLocaleDateString() }}
</div>

<div class="abs-br m-6 text-xl">
  <a href="https://github.com/pare1lel/slides" target="_blank" class="slidev-icon-btn">
    <carbon:logo-github />
  </a>
</div>

---
transition: slide-up
level: 2
---

# Who am I?

An undergraduate student at PKU EECS

- About to enter the junior year, but still very weak...
- Had some experience in OI, but forgot most of it after retiring...
- I'm here to give a lecture? Really?

<img src="/mutsumi-flag.gif" style="position: absolute; top: 250px; left: 150px; width: 150px; height: auto;">
<div style="position: absolute; top: 250px; left: 350px">

- If there's anything you don't understand, it must be my fault.
- Feel free to ask me on QQ, WeChat, or E-mail.
- E-mail: [2165175330@qq.com](mailto:2165175330@qq.com)
- This slide is made with [Slidev](https://cn.sli.dev). Check the [guide](https://cn.sli.dev/guide/ui) for some usages!

</div>

<div class="absolute top-2 right-2 text-xs">
  <SlideCurrentNo /> / <SlidesTotal />
</div>

<style> h1 { color: #2B90B6; } </style>

---

# Table of Contents

The <u>foundation</u> of linear algebra, from an <u>algorithmic</u> perspective.

1. From <Link to="4">Vector Space</Link> to <Link to="8">Linear Basis</Link>.
2. From <Link to="12">Linear Map</Link> to <Link to="18">Characteristic Polynomial</Link>.
3. From <Link to="20">LGV lemma</Link> to <Link to="22">Matrix-Tree theorem</Link>.

<div class="absolute top-2 right-2 text-xs">
  <SlideCurrentNo /> / <SlidesTotal />
</div>

<style> h1 { color: #2B90B6; } </style>

---
transition: fade
level: 2
---

# Vector Space

- A set of quantities that can be <u>added</u> and <u>scaled</u>.
- Abstracted from vectors in Euclidean space.

<div class="absolute top-2 right-2 text-xs">
  <SlideCurrentNo /> / <SlidesTotal />
</div>

<img src="/Coord_system_CA_0.svg" style="position: absolute; top: 180px; left: 100px; width: 300px; height: auto;">

<img src="/what-is-linear-algebra.webp" style="position: absolute; top: 50px; right: 50px; width: 450px; height: auto;">

<style> h1 { color: #2B90B6; } </style>

---

# Vector Space

- A [vector space](https://en.wikipedia.org/wiki/Vector_space) over a [field](https://en.wikipedia.org/wiki/Field_(mathematics)) $F$ is a set $V$ with two operations:
  - Addition $+ : V \times V \to V$.
  - Scalar multiplication $\cdot : F \times V \to V$.
- Satisfying the following axioms:
  - $(V,+)$ forms an [abelian group](https://en.wikipedia.org/wiki/Abelian_group).
  - Compatibility with scalar multiplication: $(\alpha\beta) \cdot v = \alpha \cdot (\beta \cdot v)$ for all $\alpha, \beta \in F$ and $v \in V$.
  - Two distributive properties:
    - $\alpha \cdot (v + w) = \alpha \cdot v + \alpha \cdot w$ for all $\alpha \in F$ and $v, w \in V$.
    - $(\alpha + \beta) \cdot v = \alpha \cdot v + \beta \cdot v$ for all $\alpha, \beta \in F$ and $v \in V$.

<div v-click>

- Two classical examples in OI:
  - Euclidean space $\mathbb{R}^n:=\{(x_1,x_2,\ldots,x_n) \mid x_i \in \mathbb{R}\}$ with $F = \mathbb{R}$.
  - $n$-bit numbers $\{0, 1, \ldots, 2^n-1\}$ over bitwise XOR. What are $F$ and scalar multiplication here?

</div>

<div class="absolute top-2 right-2 text-xs">
  <SlideCurrentNo /> / <SlidesTotal />
</div>

<style> h1 { color: #2B90B6; } </style>

---

# Linear Subspace

- A [linear subspace](https://en.wikipedia.org/wiki/Linear_subspace) of a vector space $V$ is a non-empty subset $W \subseteq V$ that is [closed](https://en.wikipedia.org/wiki/Closure_(mathematics)) under the operations.
  - The singleton set $\{0\}$ and the entire space $V$ are called the <u>trivial subspaces</u>.
- The [linear span](https://en.wikipedia.org/wiki/Linear_span) of a set $S$ of vectors is the smallest linear subspace containing $S$, denoted $\langle S \rangle$.
  - $\langle S\rangle=\left\{\sum_{s \in S} \alpha_s s \mid \alpha_s \in F{\color{#2B90B6}\text{ and }\alpha_s\ne 0 \text{ for finitely many } s}\right\}$.
  - The <u>finite</u> sum $\sum_{s\in S} \alpha_s s$ is called a [linear combination](https://en.wikipedia.org/wiki/Linear_combination) of $S$.

<div v-click>

- For a subset $S$ of $F$-vector space $V$:
  - $S$ is called a <u>spanning set</u> if $\langle S \rangle = V$.
  - $S$ is called [linearly independent](https://en.wikipedia.org/wiki/Linear_independence) if $\sum_{s \in S} \alpha_s s = 0$ implies $\alpha_s = 0$ for all $s \in S$.
  - $S$ is called a [basis](https://en.wikipedia.org/wiki/Basis_(linear_algebra)) if it is both a spanning set and linearly independent.
- Each vector of $V$ can be **uniquely** expressed as a linear combination of the basis vectors.
- $S$ is a minimal spanning set $\iff S$ is a basis $\iff S$ is a maximal linearly independent set.
- All vector space $V$ has a basis, and all bases of $V$ have the same [cardinality](https://en.wikipedia.org/wiki/Cardinality), called the [dimension](https://en.wikipedia.org/wiki/Dimension_(vector_space)) of $V$.

</div>

<div class="absolute top-2 right-2 text-xs">
  <SlideCurrentNo /> / <SlidesTotal />
</div>

<style> h1 { color: #2B90B6; } </style>

---

# Gauss-Jordan Elimination

- Given a finite set $S=\{v_1, \ldots, v_n\}\subseteq F^d$, we want to find a basis of $\langle S \rangle$.
  - The principle is that [elementary row operations](https://en.wikipedia.org/wiki/Elementary_matrix) do not change the linear span of the rows.
- The algorithm is as follows:
  1. Find the vector $v_i$ with the smallest non-zero coordinate $j$ in $S$, pick $j$ as the <u>pivot</u> coordinate.
  2. Use $v_i$ to eliminate the $j$-th coordinate of all other vectors (not only $S$).
  3. Remove $v_i$ from $S$ and add it to the basis. Return to step 1 if $S$ has non-zero vectors left.

<v-switch>
  <template #1>

- Take $F=\mathbb F_2$ as an example (XOR space):
$$
\begin{pmatrix}
  0 & 0 & 0 & 1 \\
  1 & 1 & 0 & 0 \\
  1 & 0 & 1 & 1 \\
  0 & 1 & 1 & 0
\end{pmatrix}
$$
  </template>
  <template #2>

- Take $F=\mathbb F_2$ as an example (XOR space): Swap Row 1 and Row 2,
$$
\begin{pmatrix}
  {\color{#2B90B6}1} & 1 & 0 & 0 \\
  0 & 0 & 0 & 1 \\
  1 & 0 & 1 & 1 \\
  0 & 1 & 1 & 0
\end{pmatrix}
$$
  </template>
  <template #3>

- Take $F=\mathbb F_2$ as an example (XOR space): Eliminate Column 1,
$$
\begin{pmatrix}
  {\color{#2B90B6}1} & 1 & 0 & 0 \\
  0 & 0 & 0 & 1 \\
  0 & 1 & 1 & 1 \\
  0 & 1 & 1 & 0
\end{pmatrix}
$$
  </template>
  <template #4>

- Take $F=\mathbb F_2$ as an example (XOR space): Swap Row 2 and Row 3,
$$
\begin{pmatrix}
  {\color{#2B90B6}1} & 1 & 0 & 0 \\
  0 & {\color{#2B90B6}1} & 1 & 1 \\
  0 & 0 & 0 & 1 \\
  0 & 1 & 1 & 0
\end{pmatrix}
$$
  </template>
  <template #5>

- Take $F=\mathbb F_2$ as an example (XOR space): Eliminate Column 2,
$$
\begin{pmatrix}
  {\color{#2B90B6}1} & 0 & 1 & 1 \\
  0 & {\color{#2B90B6}1} & 1 & 1 \\
  0 & 0 & 0 & 1 \\
  0 & 0 & 0 & 1
\end{pmatrix}
$$
  </template>
  <template #6>

- Take $F=\mathbb F_2$ as an example (XOR space): Eliminate Column 4, Finished.
$$
\begin{pmatrix}
  {\color{#2B90B6}1} & 0 & 1 & 0 \\
  0 & {\color{#2B90B6}1} & 1 & 0 \\
  0 & 0 & 0 & {\color{#2B90B6}1} \\
  0 & 0 & 0 & 0
\end{pmatrix}
$$
  </template>
  <template #7>
<div>

- The result matrix follows the [reduced row echelon form](https://en.wikipedia.org/wiki/Row_echelon_form).
  - The leading entry in each nonzero row is 1 (called a <u>leading 1</u>).
  - Each leading 1 is the <u>only</u> non-zero entry in its column.
  - The leading 1's columns are strictly increasing, and all zero vectors are at the bottom.

</div>
  </template>
</v-switch>

<div class="absolute top-2 right-2 text-xs">
  <SlideCurrentNo /> / <SlidesTotal />
</div>

<style> h1 { color: #2B90B6; } </style>

---

# Linear Basis

- Consider inserting a new element $v$ into $S$, we can still maintain the result of elimination.
  - Use the basis vectors to eliminate the pivot coordinates of $v$.
  - If $v\ne 0$, add it to the basis.
  - Adjust other vectors to maintain the reduced row echelon form.
- This data structure is called the [Linear Basis](https://www.luogu.com.cn/problem/P3812), with $O(d^2)$ time complexity for each insertion.

<div v-click>

- More tricks:
  - If you don't know "bitset", read any tutorial on it! (OI Wiki [Link](https://oi-wiki.org/lang/csl/bitset/))
  - Given a set $S$ of $n$-bit numbers, can you find the $k$-th smallest element of $\langle S\rangle$?
  - With some modifications, the linear basis can support deletion from $S$. Read [this blog](https://mem.ac/oi/algorithm/dynamic-linear-basis/) if interested.
</div>

<div class="absolute top-2 right-2 text-xs">
  <SlideCurrentNo /> / <SlidesTotal />
</div>

<style> h1 { color: #2B90B6; } </style>

---

# "Inner product" on vector space

- We define the "inner product" on $F^n$ as $(x|y):=\sum_{i=1}^n x_iy_i$.
  - We call $x$ and $y$ are [orthogonal](https://en.wikipedia.org/wiki/Orthogonality) if $(x|y)=0$.
  - It cannot be called a real inner product, as the positive-definite property may not be satisfied.
- For a subset $S\subseteq F^n$, we define the [orthogonal complement](https://en.wikipedia.org/wiki/Orthogonal_complement) of $S$ as:
  $$S^\perp:=\{x\in F^n \mid (x|y)=0 \text{ for all } y\in S\}.$$
  - $S^\perp$ is a subspace of $F^n$, and $S^\perp=\langle S\rangle^\perp$.
  - $\langle S\rangle\subseteq (S^\perp)^\perp$. It's a simple consequence of the definition.
  - $\dim\langle S\rangle+\dim S^\perp=n$ from the [rank–nullity theorem](https://en.wikipedia.org/wiki/Rank%E2%80%93nullity_theorem), thus $\langle S\rangle=(S^\perp)^\perp$.
- $S^\perp$ can be viewed as a representation of the linear span $\langle S\rangle$.
- If $\langle S\rangle$ is hard to deal with, try to use $(S^\perp)^\perp$ instead!

<div class="absolute top-2 right-2 text-xs">
  <SlideCurrentNo /> / <SlidesTotal />
</div>

<style> h1 { color: #2B90B6; } </style>

---

# Orthogonal Linear Basis

- Given a set $S$ of vectors in $F^n$, how to find a basis of $S^\perp$?
  - Find the basis of $\langle S\rangle$ as before, WLOG assume the leading 1s are in the top-left block of the matrix.
  - Let $B$ be the top-right block of the matrix.
  - Put $-B^\top$ in the bottom-left block, and the identity matrix in the bottom-right block.
- The bottom blocks is a basis of $S^\perp$, called the <u>orthogonal linear basis</u> of $S$.
  - Don't be confused with the [Orthogonal Basis](https://en.wikipedia.org/wiki/Orthogonal_basis) in the inner product space.

<img src="/CF1336E2.png" style="position: absolute; top: 300px; width: 250px; left: 350px; height: auto;">

<div class="absolute top-2 right-2 text-xs">
  <SlideCurrentNo /> / <SlidesTotal />
</div>

<style> h1 { color: #2B90B6; } </style>

---
transition: slide-up
level: 2
---

# Exercise?

- Since I haven't practiced OI for a long time, I don't have many problems to share...
  - It's your own responsibility to find problems to practice. 😊

<img src="/murasame.gif" style="position: absolute; top: 50px; right: 50px; width: 150px; height: auto;">

<v-switch>
  <template #1>
<div>

<img src="/cf.png" style="position: absolute; top: 285px; right: 20px; width: 180px; height: auto;">

- Select your favourite OJ, [search for problems](https://codeforces.com/problemset?tags=math,2300-2800) slightly more difficult than your level.
  - Choose a problem with a good title and work on it!
  - Use the [Immersive Translate](https://immersivetranslate.com/zh-Hans/) extension if reading English is a burden for you.
  - Use editorial as a reminder, e.g. when there's no progress for 0.5h, take a 5s glance at the editorial.
- If it feels too hard or too easy, adjust the difficulty.
  - "Too hard" means you have a hard time following the editorial.
  - "Too easy" means you have come up with the solution within 3 minutes several times.
- If you encounter a new technique, search for materials (including this slide) and do comparative reading.

</div>
  </template>
  <template #2>
<div>

- Here are some (possibly outdated) old problems with the linear basis:
  - [Luogu 4151](https://www.luogu.com.cn/problem/P4151) is a classic problem combining the linear basis and graph theory.
  - [CF1672G](https://codeforces.com/contest/1672/problem/G) is a problem related to $\mathbb F_2$ linear span.
  - [UOJ72](https://uoj.ac/problem/72) is a problem related to $\mathbb F_2$ inner product, may be a bit difficult to understand.
  - [UOJ138](https://uoj.ac/problem/138) is a counting problem on an undirected connected graph. Why is it here?
  - [UOJ453](https://uoj.ac/problem/453) is a problem that requires a linear basis that supports deletion.
    - Work on this problem only after you are familiar with matrices (multiplication, rank, etc...).
  - [Luogu 11620](https://www.luogu.com.cn/problem/P11620) is one of the few Ynoi series problems involving the linear basis.
  - As long as you know what the [FWT](https://www.luogu.com.cn/problem/P4717) is, try this [\*3500 problem](https://codeforces.com/contest/1336/problem/E2)! 😋

</div>
  </template>
</v-switch>

<div class="absolute top-2 right-2 text-xs">
  <SlideCurrentNo /> / <SlidesTotal />
</div>

<style> h1 { color: #2B90B6; } </style>

---

# Linear Map

A mapping that preserves the vector space structure.

- Given $F$-vector spaces $V$ and $W$, a [linear map](https://en.wikipedia.org/wiki/Linear_map) is a function $f: V \to W$ satisfying:
  - $f(v + w) = f(v) + f(w)$ for all $v, w \in V$.
  - $f(\alpha v) = \alpha f(v)$ for all $\alpha \in F$ and $v \in V$.
- If $f:V\to W$ and $g:U\to V$ are linear maps, the composition $fg: U \to W$ is also a linear map.
- If $f:V\to W$ is a bijection and linear map, $f^{-1}$ is also a linear map, and we call $f$ is an [isomorphism](https://en.wikipedia.org/wiki/Isomorphism).
  - $V$ and $W$ are equivalent when discussing the vector space structures.
  - Given a basis $(v_1, \ldots, v_n)$ of $V$, linear map $\varphi_\mathbf{v}: F^n \to V$ defined by $\varphi_\mathbf{v}(e_i) = v_i$ is an isomorphism.

<div v-click>

- Let $\mathrm{Hom}(V, W)$ be the set of all linear maps from $V$ to $W$, it's also a vector space:
  - Addition: $(f + g)(v) = f(v) + g(v)$ for all $v \in V$.
  - Scalar multiplication: $(\alpha f)(v) = \alpha f(v)$ for all $\alpha \in F$ and $v \in V$.
- What's the dimension and basis of $\mathrm{Hom}(V, W)$?

</div>

<div class="absolute top-2 right-2 text-xs">
  <SlideCurrentNo /> / <SlidesTotal />
</div>

<style> h1 { color: #2B90B6; } </style>

---

# Matrix = Linear Map on Basis

- Given a field $F$ and $m,n\in\mathbb Z_{\ge 1}$, let $\mathrm{M}_{m\times n}(F)$ be the set of all $m\times n$ [matrices](https://en.wikipedia.org/wiki/Matrix_(mathematics)) with entries in $F$.
  - Considering an $m\times n$ matrix as an $mn$-dimensional vector, $\mathrm{M}_{m\times n}(F)$ is also a vector space.
- Given a basis $(v_1, \ldots, v_n)$ of $V$ and $(w_1, \ldots, w_m)$ of $W$, we have the isomorphism:
  $$
  \begin{aligned}
  \mathcal{M}_\mathbf{v}^\mathbf{w}:\mathrm{Hom}(V, W) &\xrightarrow{\sim} \mathrm{M}_{m\times n}(F) \\
  f &\mapsto (a_{ij})_{i,j}, \text{ where } f(v_j) = \sum_{i\in[m]} a_{ij} w_i.
  \end{aligned}
  $$
  - If $W=F^m$ and $(w_1, \ldots, w_m)$ is the standard basis, we can write $A=(f(v_1) \mid \cdots \mid f(v_n))$.
  - The [matrix multiplication](https://en.wikipedia.org/wiki/Matrix_multiplication) corresponds to the composition of linear maps:
  $$
  fg(u_k)=f\left(\sum_j b_{jk} v_j\right)=\sum_j b_{jk} f(v_j)=\sum_j b_{jk} \sum_i a_{ij} w_i=\sum_i{\color{#2B90B6}\left(\sum_j a_{ij}b_{jk}\right)} w_i.
  $$

<div class="absolute top-2 right-2 text-xs">
  <SlideCurrentNo /> / <SlidesTotal />
</div>

<style> h1 { color: #2B90B6; } </style>

---

# Kernel, Image, and Rank

- Given a linear map $f:V\to W$, we define:
  - The [kernel](https://en.wikipedia.org/wiki/Kernel_(linear_algebra)) of $f$ as $\ker f:=\{v\in V \mid f(v)=0\}=f^{-1}(0)$.
  - The [image](https://en.wikipedia.org/wiki/Image_(mathematics)) of $f$ as $\operatorname{im} f:=\{w\in W \mid w=f(v) \text{ for some } v\in V\}$.
  - The [rank](https://en.wikipedia.org/wiki/Rank_(linear_algebra)) of $f$ as $\mathrm{rk}(f):=\dim(\operatorname{im} f)$.
- $\ker f$ is a subspace of $V$, and $\operatorname{im} f$ is a subspace of $W$.
- The rank $\mathrm{rk}(A)$ of $A\in\mathrm{M}_{m\times n}(F)$ is the rank of $A$ as a linear map $F^n \to F^m$.
- The [rank–nullity theorem](https://en.wikipedia.org/wiki/Rank%E2%80%93nullity_theorem) states that $\dim V = \mathrm{rk}(f) + \dim(\ker f)$.
  - Select a basis $(u_1, \ldots, u_k)$ of $\ker f$ and $(w_1, \ldots, w_m)$ of $\operatorname{im} f$.
  - Select $v_i\in V$ such that $f(v_i)=w_i$ for all $i\in[m]$.
  - Then $(u_1, \ldots, u_k, v_1, \ldots, v_m)$ is a basis of $V$.

<div class="absolute top-2 right-2 text-xs">
  <SlideCurrentNo /> / <SlidesTotal />
</div>

<style> h1 { color: #2B90B6; } </style>

---

# Change of Basis

- Given $f:V\to W$ and bases $\mathbf{v}, \mathbf{v}'$ of $V$ and $\mathbf{w}, \mathbf{w}'$ of $W$, how to express $\mathcal{M}_{\mathbf{v}'}^{\mathbf{w}'}(f)$ by $\mathcal{M}_{\mathbf{v}}^{\mathbf{w}}(f)$?
  - Let $P_{\mathbf{v}'}^{\mathbf{v}}:F^n\to F^n$ be the change of basis from $\mathbf{v'}$ to $\mathbf{v}$,
  - where $(x_1', \ldots, x_n') \mapsto (x_1, \ldots, x_n)$ is defined by $\sum_{i=1}^n x_iv_i=\sum_{i=1}^n x_i'v_i'$.
  - $P_{\mathbf{v}'}^{\mathbf{v}}=\varphi_{\mathbf{v}'}^{-1}\varphi_{\mathbf{v}}$, where $\varphi_{\mathbf{v}}:F^n\to V$ is the <Link to="12">basis isomorphism</Link>. $(P_{\mathbf{v}'}^{\mathbf{v}})^{-1}=P_{\mathbf{v}}^{\mathbf{v}'}$.
  - Conversely, given any isomorphism $P$ and a basis $\mathbf{v}'$, we can find $\mathbf{v}$ such that $P=P_{\mathbf{v}'}^{\mathbf{v}}$.
- $\mathcal{M}_{\mathbf{v}'}^{\mathbf{w}'}(f)=(P_{\mathbf{w}'}^{\mathbf{w}})^{-1} \mathcal{M}_{\mathbf{v}}^{\mathbf{w}}(f) P_{\mathbf{v}'}^{\mathbf{v}}$.

<div v-click>

- Given $m\times n$ matrices $A,B$, we call them [equivalent](https://baike.baidu.com/item/%E7%9B%B8%E6%8A%B5%E7%9F%A9%E9%98%B5/13678808) if $\exists$ isomorphisms $P$ and $Q$ such that $B=QAP$.
  - Equivalent matrices represent the same linear map in different bases.
  - Since all invertible matrices can be expressed as products of [elementary matrices](https://en.wikipedia.org/wiki/Elementary_matrix),  
    "Equivalence" is equivalent to $\exists$ a sequence of elementary operations that transforms $A$ into $B$.
- $A$ is equivalent to $D_r:=\operatorname{diag}(1_{r\times r},0_{(m-r)\times(n-r)})$, where $r:=\mathrm{rk}(A)$.
  - $A$ is equivalent to $B$ iff $\mathrm{rk}(A)=\mathrm{rk}(B)$.
- Given $n\times n$ matrices $A,B$, we call them [similar](https://en.wikipedia.org/wiki/Matrix_similarity) if $\exists$ an isomorphism $P$ such that $B=P^{-1}AP$.
  - Similar matrices represent the same [endomorphism](https://en.wikipedia.org/wiki/Endomorphism) in different bases.

</div>

<div class="absolute top-2 right-2 text-xs">
  <SlideCurrentNo /> / <SlidesTotal />
</div>

<style> h1 { color: #2B90B6; } </style>

---
transition: fade
level: 2
---

# Determinant

- The [determinant](https://en.wikipedia.org/wiki/Determinant) originated from the [Cramer's rule](https://en.wikipedia.org/wiki/Cramer%27s_rule) for solving linear equations.
  - Now the determinant is more about <u>signed volume</u> and [exterior algebra](https://en.wikipedia.org/wiki/Exterior_algebra).
- Let $v_1 \wedge \cdots \wedge v_n$ represent the signed volume of the [parallelotope](https://en.wikipedia.org/wiki/Parallelepiped#Parallelotope) spanned by $v_1, \ldots, v_n$.
  - For $V$ with $\dim V=n$, the $n$-th [exterior power](https://en.wikipedia.org/wiki/Exterior_algebra#Exterior_power) $\bigwedge^n(V)$ is the vector space spanned by these volumes.
- The wedge products satisfy the following properties:
  - Degeneration: If $v_1, \ldots, v_n$ are linearly dependent, $v_1 \wedge \cdots \wedge v_n = 0$.
  - Addition: $v_1 \wedge \cdots (v_i+v) \cdots \wedge v_n = v_1 \wedge \cdots v_i \cdots \wedge v_n + v_1 \wedge \cdots v \cdots \wedge v_n$.
  - Scalar multiplication: $v_1 \wedge \cdots (\alpha v_i) \cdots \wedge v_n = \alpha (v_1 \wedge \cdots \wedge v_n)$.

<div v-click>

- $\dim \bigwedge^n(V) = 1$, where $v_1\wedge\cdots\wedge v_n$ forms a basis for any basis $(v_1, \ldots, v_n)$ of $V$.
  - Given an endomorphism $f:V\to V$, it induces an endomorphism $\bigwedge^n(f):\bigwedge^n(V)\to\bigwedge^n(V)$ as
  $$v_1 \wedge \cdots \wedge v_n \mapsto f(v_1) \wedge \cdots \wedge f(v_n).$$
  - $\bigwedge^n(f)$ must be a scalar multiplication, the coefficient is called the [determinant](https://en.wikipedia.org/wiki/Determinant) of $f$, denoted $\det(f)$.
  - The determinant $\det(A)$ of $A\in\mathrm{M}_{n\times n}(F)$ is the determinant as a linear map $F^n\to F^n$.

</div>

<div class="absolute top-2 right-2 text-xs">
  <SlideCurrentNo /> / <SlidesTotal />
</div>

<style> h1 { color: #2B90B6; } </style>

---

# Determinant

- From the definition, we can prove the following properties:
  - [Leibniz formula](https://en.wikipedia.org/wiki/Determinant#Leibniz_formula): For $A=(a_{ij})_{i,j}\in\mathrm{M}_{n\times n}(F)$, we have:
  $$\det(A)=\sum_{\sigma\in\mathfrak S_n} \operatorname{sgn}(\sigma) \prod_{i=1}^n a_{i,\sigma(i)}.$$
  - Multiplicativity: $\det(AB)=\det(A)\det(B)$ for all $A,B\in\mathrm{M}_{n\times n}(F)$.
  - Calculated by [Gauss-Jordan elimination](https://www.luogu.com.cn/problem/P7112), with time complexity $O(n^3)$.
  - [Laplace expansion](https://en.wikipedia.org/wiki/Laplace_expansion): For $A=(a_{ij})_{i,j}\in\mathrm{M}_{n\times n}(F)$, let $M_{ij}$ be the [minor](https://en.wikipedia.org/wiki/Minor_(linear_algebra)) of $a_{ij}$, then:
  $$\det(A)=\sum_{j=1}^n (-1)^{i+j} a_{ij} M_{ij}=\sum_{i=1}^n (-1)^{i+j} a_{ij} M_{ij}.$$
- The [adjugate matrix](https://en.wikipedia.org/wiki/Adjugate_matrix) $A^\lor$ is the transpose of the cofactor matrix of $A$.
  - $AA^\lor=A^\lor A=\det(A)\cdot 1_{n\times n}$, and $A^{-1}=(\det(A))^{-1}A^\lor$ when $\det(A)$ is invertible.

<div class="absolute top-2 right-2 text-xs">
  <SlideCurrentNo /> / <SlidesTotal />
</div>

<style> h1 { color: #2B90B6; } </style>

---

# Characteristic Polynomial

- The determinant can be generalized to any commutative ring e.g. the polynomial ring $F[X]$.
- The [characteristic polynomial](https://en.wikipedia.org/wiki/Characteristic_polynomial) $\mathrm{Char}_A=\det(X\cdot 1_{n\times n}-A)$, where $X\cdot 1_{n\times n}-A\in\mathrm{M}_{n\times n}(F[X])$.
- Similar matrices have the same characteristic polynomial i.e. $\mathrm{Char}_{P^{-1}AP}=\mathrm{Char}_A$.
- [Cayley–Hamilton theorem](https://en.wikipedia.org/wiki/Cayley%E2%80%93Hamilton_theorem): For any $A\in\mathrm{M}_{n\times n}(F)$, we have $\mathrm{Char}_A(A)=0_{n\times n}$.
  - Proof omitted. It's trivial when you know what is [Frobenius normal form](https://en.wikipedia.org/wiki/Frobenius_normal_form).
- The roots $\lambda$ of the characteristic polynomial are the [eigenvalues](https://en.wikipedia.org/wiki/Eigenvalues_and_eigenvectors) of the matrix.
  - $\lambda\cdot 1_{n\times n}-A$ is not full rank, i.e. there exists a non-zero vector $v$ such that $Av=\lambda v$.
  - $V_\lambda := \ker(\lambda\cdot 1_{n\times n}-A)$ is called the $\lambda$-eigenspace. $V_\lambda\ne\{0\}\iff \lambda$ is an eigenvalue of $A$.
  - $A$ is [diagonalizable](https://en.wikipedia.org/wiki/Diagonalizable_matrix) i.e. similar to diagonal matrices $\iff$ the sum of dimension of eigenspaces $=n$.
- The characteristic polynomial can be calculated in time complexity $O(n^3)$. Check [QOJ59](https://qoj.ac/problem/59) for details.

<div class="absolute top-2 right-2 text-xs">
  <SlideCurrentNo /> / <SlidesTotal />
</div>

<style> h1 { color: #2B90B6; } </style>

---
transition: slide-up
level: 2
---

# Exercises

- [LOJ3626](https://loj.ac/p/3626) is a problem for computing determinants.
- [UOJ655](https://uoj.ac/problem/655) is an interactive puzzle game about determinants.
- [xmascon20-d](https://atcoder.jp/contests/xmascon20/tasks/xmascon20_d) is another problem for computing determinants.
- [CF923E](https://codeforces.com/problemset/problem/923/E) uses the diagonalization to optimize the power of a matrix.
- [UOJ646](https://uoj.ac/problem/646) is a problem of predicting a pseudo-random sequence. Why is it here?

<div class="absolute top-2 right-2 text-xs">
  <SlideCurrentNo /> / <SlidesTotal />
</div>

<style> h1 { color: #2B90B6; } </style>

---

# Lindström–Gessel–Viennot lemma

- Let $G$ be a [directed acyclic graph](https://en.wikipedia.org/wiki/Directed_acyclic_graph), each edge has a weight in a commutative ring.
  - For a path $P$, let the path weight $\omega(P)$ be the product of the edge weights along $P$.
  - For two vertices $u$ and $v$, let $\omega(u,v):=\sum_{P:u\to v}\omega(P)$ be the sum of $\omega(P)$ of all paths $P$ from $u$ to $v$.
- Given two tuples of vertices $(s_1, \ldots, s_n)$ and $(t_1, \ldots, t_n)$, we call $(P_1, \ldots, P_n)$ is an <u>$n$-path</u> if:
  - There <u>exists a permutation</u> $\sigma(P)\in\mathfrak S_n$ such that $P_i$ is a path from $s_i$ to $t_{\sigma(i)}$.
- We call an $n$-path is <u>non-crossing</u> if the paths do not have any common vertex.
  - Let $\omega(P):=\prod_{i=1}^n \omega(P_i)$ be the product of the weights of the $n$ paths.

<div v-click>

- Let the matrix $M:=(m_{ij})_{i,j}$, where $m_{ij}:=\omega(s_i,t_j)$.
  - The [LGV lemma](https://en.wikipedia.org/wiki/Lindstr%C3%B6m%E2%80%93Gessel%E2%80%93Viennot_lemma) states that $\det(M)$ is the sum of $\operatorname{sgn}(\sigma(P))\omega(P)$ over all non-crossing $n$-paths $P$.
- *Proof.* Let $P$ be any crossing $n$-path, smallest $(i,j)$ such that $P_i$ crosses $P_j$, and smallest crossing vertex $u$.
  - Let $P'$ be the $n$-path obtained by swapping the parts of $P_i$ and $P_j$ after $u$.
  - $\omega(P)=\omega(P')$ and the signs are opposite, so the terms cancel each other. *Q.E.D.*
- Be careful to <u>avoid end-point swaps</u> when applying the lemma.

</div>

<div class="absolute top-2 right-2 text-xs">
  <SlideCurrentNo /> / <SlidesTotal />
</div>

<style> h1 { color: #2B90B6; } </style>

---

# Cauchy–Binet formula

- Given $A\in\mathrm{M}_{n\times m}(F)$ and $B\in\mathrm{M}_{m\times n}(F)$, let $A_{[n],S}$ and $B_{S,[n]}$ be the submatrices of $A$ and $B$:
  $$\det(AB)=\sum_{|S|=n} \det(A_{[n],S})\det(B_{S,[n]}).$$
- *Proof Sketch.* Apply the LGV lemma to the 3-layer DAG.
- [LOJ3533](https://loj.ac/p/3533) is a direct application of the Cauchy–Binet formula.

<div class="absolute top-2 right-2 text-xs">
  <SlideCurrentNo /> / <SlidesTotal />
</div>

<style> h1 { color: #2B90B6; } </style>

---
transition: fade
level: 2
---

# Matrix-Tree theorem

- Given a simple undirected graph $G=(V,E)$ with edge weights $w:E\to F$.
- Let $A=(a_{ve})_{v,e}\in\mathrm{M}_{n\times m}(F)$ be the [incidence matrix](https://en.wikipedia.org/wiki/Incidence_matrix) of $G$, where:
  $$ a_{ve} := \begin{cases} \sqrt{w(e)}, & \text{if } v \text{ is the smaller endpoint of } e, \\ -\sqrt{w(e)}, & \text{if } v \text{ is the larger endpoint of } e, \\ 0, & \text{otherwise}. \end{cases}$$
- Let $B\in\mathrm{M}_{(n-1)\times m}(F)$ be the matrix obtained by removing the first row of $A$.
- Apply the Cauchy–Binet formula to $BB^\top$:
  $$\det(BB^\top)=\sum_{|S|=n-1} \det(B_{[n-1],S})^2.$$
- $BB^\top$ is a submatrix of the [Laplacian matrix](https://en.wikipedia.org/wiki/Laplacian_matrix) of $G$ and can be calculated easily.
- What does $\det(B_{[n-1],S})^2$ mean?

<div class="absolute top-2 right-2 text-xs">
  <SlideCurrentNo /> / <SlidesTotal />
</div>

<style> h1 { color: #2B90B6; } </style>

---

# Matrix-Tree theorem

- From the Leibniz formula, $\det(B_{[n-1],S})$ means enumerating a bijection between $V\setminus\{v_1\}$ and $S$.
  - Each corresponding vertex and edge must be adjacent.
- If $S$ does not contain a cycle i.e. forms a spanning tree:
  - The bijection is unique and $\det(B_{[n-1],S})^2$ is the product of edge weights of the spanning tree.
- If $S$ contains a cycle, choose any cycle $C$ in $S$:
  - For each bijection $\sigma$, reverse the order of the vertices in $C$ to get another bijection $\sigma'$.
  - If $|C|$ is odd, the signs are same, and the products of weights are opposite.
  - If $|C|$ is even, the signs are opposite, and the products of weights are same.
  - The contributions of $\sigma$ and $\sigma'$ cancel each other, $\det(B_{[n-1],S})=0$.
- In conclusion, we proved [the Matrix-Tree theorem](https://en.wikipedia.org/wiki/Kirchhoff%27s_theorem):
  - The sum of the product of edge weights of all spanning trees $=\det(BB^\top)$.

<div class="absolute top-2 right-2 text-xs">
  <SlideCurrentNo /> / <SlidesTotal />
</div>

<style> h1 { color: #2B90B6; } </style>

---

# Matrix-Tree theorem: directed version

- Given a directed graph $G=(V,E)$ with edge weights $w:E\to F$.
  - We want to find the sum of the product of edge weights of all <u>inner spanning trees</u> rooted at $v_1$.
- Let $A=(a_{ve})_{v,e}$ and $A'=(a'_{ve})_{v,e}$ be the modified incidence matrices of $G$, where:
  $$a_{ve} := \begin{cases} \sqrt{w(e)}, & \text{if } v \text{ is the head of } e, \\ -\sqrt{w(e)}, & \text{if } v \text{ is the tail of } e, \\ 0, & \text{otherwise}, \end{cases}$$
  $$a'_{ve} := \begin{cases} \sqrt{w(e)}, & \text{if } v \text{ is the head of } e, \\ 0, & \text{otherwise}. \end{cases}$$
- Let $B$ and $B'$ be the matrices obtained by removing the first row of $A$ and $A'$, respectively.
- $\det(BB'^\top)$ is what we want. Proof is left as an exercise.

<div class="absolute top-2 right-2 text-xs">
  <SlideCurrentNo /> / <SlidesTotal />
</div>

<style> h1 { color: #2B90B6; } </style>

---

# Matrix-Tree theorem: spanning forest

- Given a simple undirected graph $G=(V,E)$.
  - A $k$-spanning forest is an edge subset that contains $k$ connected components and no cycles.
  - The weight of a $k$-spanning forest is <u>the product of the size</u> of each connected component.
  - We want to find the sum of the weights of all $k$-spanning forests.
- Enumerate the roots of the connected components $S\subseteq V$.
  - The number of $k$-spanning forests is the principal minor of $L=AA^\top$ indexed by $V\setminus S$.
- The answer is the $k$-th order coefficient of $\mathrm{Char}_L\times(-1)^{n-k}$. 
  - For $k=1$, the number of spanning trees $=\frac 1n\prod_{k=1}^{n-1}\lambda_k$,
  - where $\lambda_1\ge\cdots\ge\lambda_{n-1}\ge \lambda_n=0$ are the eigenvalues of $L$.

<div class="absolute top-2 right-2 text-xs">
  <SlideCurrentNo /> / <SlidesTotal />
</div>

<style> h1 { color: #2B90B6; } </style>

---
transition: slide-up
level: 2
---

# Exercises

- [LOJ3409](https://loj.ac/p/3409) is a counting problem related to <span class="heimu">Cauchy–Binet formula</span>.
- [LOJ6759](https://loj.ac/p/6759) is a... maximum flow problem?
- [LOJ3630](https://loj.ac/p/3630) is a counting problem related to <span class="heimu">the LGV lemma</span>.
- [Gym102978A](https://codeforces.com/gym/102978/problem/A) is a Young tableaux counting problem.
- [Luogu5296](https://www.luogu.com.cn/problem/P5296) is an application of the Matrix-Tree theorem.
- [QOJ2073](https://qoj.ac/problem/2073) is a knowledge-oriented problem about:
  - The Matrix-Tree theorem, <span class="heimu">[Kronecker sum](https://mathworld.wolfram.com/KroneckerSum.html)</span>, and <span class="heimu">[resultant](https://en.wikipedia.org/wiki/Resultant)</span>.

<div class="absolute top-2 right-2 text-xs">
  <SlideCurrentNo /> / <SlidesTotal />
</div>

<style>
h1 { color: #2B90B6; }
.heimu, .heimu a, a .heimu, .heimu a.new {
  transition: color 0.13s linear;
  background-color: #252525;
  color: #252525;
  text-shadow: none;
}
.heimu:hover, .heimu:active,
.heimu:hover .heimu, .heimu:active .heimu {
  color: white !important;
}
.heimu:hover a, a:hover .heimu,
.heimu:active a, a:active .heimu {
  color: lightblue !important;
}
.heimu:hover .new, .heimu .new:hover, .new:hover .heimu,
.heimu:active .new, .heimu .new:active, .new:active .heimu {
  color: #BA0000 !important;
}
</style>

---

# Further Reading

- [Algebra textbooks](https://wwli.asia/index.php/zh/books-item-zh) written by [Wenwei Li](https://wwli.asia/index.php/zh/):
  - The reading order is [EAlg-Notes](https://wwli.asia/downloads/books/EAlg-Notes.pdf) → [Al-jabr-1](https://wwli.asia/downloads/books/Al-jabr-1.pdf) → [Al-jabr-2](https://wwli.asia/downloads/books/Al-jabr-2.pdf).
  - The first book is useful for the first year college math courses. Many of the narratives are OI-friendly.
  - The third book is very "hardcore". Read only if you have enough experience in related fields.
- Some old lecture notes I made, of poor quality and may be difficult to understand:
  - [Linear Algebra](http://www.gdfzoj.com:23380/post/813) in Oct 2021, [Selected Problems](http://www.gdfzoj.com:23380/post/845) in Mar 2022, [Selected Problems](http://www.gdfzoj.com:23380/post/864) in Jun 2022.
  - Contact the administrator (?) if you don't have access to the site.
- [Slides](http://www.gdfzoj.com:23380/post/1156) about the linear algebra made by [nealchen](https://codeforces.com/profile/nealchen).

<div v-click>

- Chinese Candidate Team Thesis in [this repository](https://github.com/enkerewpo/OI-Public-Library).
  - Read **all** the theses from the last 10 years, but mostly **skimming**.
  - Careful reading is for the topics that interest you or that you find necessary.
- Related theses of this slide:
  - 「两类递推数列的性质和应用」by 钟子谦 in 2019.
  - 「浅谈线性代数与图论的关系」by 潘佳奇 in 2021.

</div>

<div class="absolute top-2 right-2 text-xs">
  <SlideCurrentNo /> / <SlidesTotal />
</div>

<style> h1 { color: #2B90B6; } </style>

---
layout: center
class: text-center
---

# Thank you for listening!

[GitHub](https://github.com/pare1lel/slides) · [Source File](https://github.com/pare1lel/slides/blob/main/linear-algebra.md?plain=1)

<PoweredBySlidev mt-10 />

<div class="absolute top-2 right-2 text-xs">
  <a href="https://www.bilibili.com/video/BV1v5TuzJEid/" target="_blank"><SlideCurrentNo /></a> / <SlidesTotal />
</div>

<style>h1 { color: #2B90B6; }</style>
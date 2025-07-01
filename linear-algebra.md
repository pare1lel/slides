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
---

# Linear Algebra in OI

Dongwu Chen (PKU EECS)

<div @click="$slidev.nav.next" class="mt-12 py-1" hover:bg="white op-10">
  Press Space for next page <carbon:arrow-right />
</div>

<div class="absolute bottom-2 right-2 text-xs">
  {{ new Date().toLocaleDateString() }}
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

1. From Vector Space to Linear Basis.
2. From Linear Transformation to Characteristic Polynomial.
3. From LGV Lemma to Matrix-Tree Theorem.

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
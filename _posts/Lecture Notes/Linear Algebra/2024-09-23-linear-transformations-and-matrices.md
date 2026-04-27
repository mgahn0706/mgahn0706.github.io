---  
tags:  
  - linear-transformation  
  - vector-space  
share: "true"  
github_title: 2024-09-23-linear-transformations-and-matrices  
title: 2. Linear Transformations and Matrices  
date: 2024-09-23  
categories:  
  - Lecture Notes  
  - Linear Algebra  
math: "true"  
---  
## 1. Linear Transformations  
  
### Definition  
  
**[Def]** $T: V \rightarrow W$  
  
($\uparrow$ domain, $\uparrow$ co-domain)  
  
is a **linear transformation** if $V, W$ are vector spaces over $\mathbb{F}$ and for $x, y \in V, c \in \mathbb{F}$:  
  
1. $T(x+y) = T(x) + T(y)$ (addition in V $\rightarrow$ addition in W)  
      
2. $T(cx) = cT(x)$  
      
  
**Properties:**  
  
- $T(\vec{0}_V) = \vec{0}_W$  
      
    ($\because T(\vec{0}) = T(\vec{0}+\vec{0}) = T(\vec{0}) + T(\vec{0})$)  
      
- $T$ is linear $\iff T(cx+y) = cT(x) + T(y)$  
      
  
### Examples  
  
- **Ex.** $\mathbb{R}^2 \rightarrow \mathbb{R}^2$ rotation by $\theta$.  
      
- **Ex.** $T_{(x)}$: reflection about the x-axis  
      
    $x=(a_1, a_2) \Rightarrow T(x) = (a_1, -a_2)$  
      
- **Ex.** $T: P_n(\mathbb{R}) \rightarrow P_{n-1}(\mathbb{R})$  
      
    $f(x) \mapsto f'(x)$ "Linear" (derivative)  
      
- **Ex.** $V = C(\mathbb{R})$ the vector space of continuous real-valued functions on $\mathbb{R}$.  
      
    $T: V \rightarrow \mathbb{R}$  
      
    $f \mapsto \int_{a}^{b} f(t) dt \quad (a<b)$  
      
  
---  
  
## 2. Kernel and Range  
  
Let $T: V \rightarrow W$ be linear.  
  
- **$N(T)$** := null space (kernel) of T  
      
    $= \{ x \in V : T(x) = \vec{0} \}$  
      
- **$R(T)$** := range (image) of T  
      
    $= \{ T(x) : x \in V \}$  
      
  
### Theorem 2.1  
  
(a) $N(T)$ is a subspace of $V$. ($\rightarrow$ subset of V)  
  
(b) $R(T)$ is a subspace of $W$. ($\rightarrow$ subset of W)  
  
Proof)  
  
(a) $T(\vec{0}) = \vec{0} \Rightarrow \vec{0} \in N(T)$  
  
If $x, y \in N(T)$,  
  
$T(x+y) = T(x) + T(y) = \vec{0} + \vec{0} = \vec{0}$  
  
$\therefore x+y \in N(T)$  
  
(b) $T(\vec{0}) = \vec{0} \Rightarrow \vec{0} \in R(T)$  
  
If $x, y \in R(T)$,  
  
Let's write $x = T(v)$, $y = T(w)$ where $v, w \in V$.  
  
$T(v+w) = T(v) + T(w) = x + y$  
  
also in $R(T)$ ($\because v+w \in V$ vector space)  
  
### Theorem 2.2  
  
$V, W$: vector space, $T: V \rightarrow W$ linear  
  
(증명에 $span(\beta)=V$ 만 써서 $V=span(\beta)$ 일때도 써도 OK)  
  
If $\beta = \{v_1, ..., v_n\}$ is a basis for V,  
  
then $R(T) = Span(T(\beta)) = Span(\{T(v_1), ..., T(v_n)\})$  
  
Proof)  
  
$R(T) \supseteq Span(T(\beta))$ is clear.  
  
Show $R(T) \subseteq Span(T(\beta))$.  
  
Let $w \in R(T)$. Then $w = T(v)$ for some $v \in V$.  
  
$v = \sum_{i=1}^{n} a_i v_i$  
  
$w = T(\sum_{i=1}^{n} a_i v_i) = \sum_{i=1}^{n} a_i T(v_i) \in Span(T(\beta))$  
  
**Ex.** $T: P_2(\mathbb{R}) \rightarrow M_{2\times2}(\mathbb{R})$  
  
$f(x) \mapsto \begin{pmatrix} f'(0) & 0 \\ 0 & f(0) \end{pmatrix}$  
  
$R(T) = Span(T(\beta))$ where $\beta=\{1, x, x^2\}$  
  
$= Span(\{ T(1), T(x), T(x^2) \})$  
  
$= Span( \{ \begin{pmatrix} 0 & 0 \\ 0 & 1 \end{pmatrix}, \begin{pmatrix} 1 & 0 \\ 0 & 0 \end{pmatrix}, \begin{pmatrix} 0 & 0 \\ 0 & 0 \end{pmatrix} \} )$  
  
$\therefore \dim R(T) = 2$  
  
- $\dim N(T)$ = **nullity** of T  
      
- $\dim R(T)$ = **rank** of T  
      
  
### Theorem 2.3 (Dimension Theorem)  
  
$T: V \rightarrow W$ linear. $V$ finite-dim.  
  
Then, **nullity(T) + rank(T) = dim(V)**  
  
Proof)  
  
Let $\dim V = n$, $\dim N(T) = k$. ($k \le n$ because $N(T)$ is subspace of $V$)  
  
Let $\{v_1, ..., v_k\}$ be a basis for $N(T)$.  
  
Extend $\{v_1, ..., v_k\}$ to $\{v_1, ..., v_k, v_{k+1}, ..., v_n\}$ for $V$. (linearly indep, add more vectors to basis by Replacement Thm).  
  
$R(T) = Span(T(\beta)) = Span(\{ T(v_1), ..., T(v_k), T(v_{k+1}), ..., T(v_n) \})$  
  
Since $T(v_1)=...=T(v_k)=\vec{0}$,  
  
$R(T) = Span(\{ T(v_{k+1}), ..., T(v_n) \})$.  
  
**Claim:** $\{ T(v_{k+1}), ..., T(v_n) \}$ is linearly independent.  
  
**Why?** Suppose $\sum_{i=k+1}^{n} b_i T(v_i) = \vec{0}$.  
  
$T(\sum_{i=k+1}^{n} b_i v_i) = \vec{0} \Rightarrow \sum_{i=k+1}^{n} b_i v_i \in N(T)$  
  
This vector exists in $N(T)$, so it is a linear combination of the basis of $N(T)$.  
  
$\sum_{i=k+1}^{n} b_i v_i = \sum_{j=1}^{k} c_j v_j$  
  
$\Rightarrow \sum_{j=1}^{k} c_j v_j - \sum_{i=k+1}^{n} b_i v_i = \vec{0}$  
  
Since $\{v_1, ..., v_n\}$ is a basis ($\Rightarrow$ l.indep),  
  
$c_1 = ... = c_k = b_{k+1} = ... = b_n = 0$.  
  
$\therefore$ Coefficients $b_i$ are all 0.  
  
### Theorem 2.4  
  
$T: V \rightarrow W$ linear. $V, W$ vector space over $\mathbb{F}$.  
  
**$T$ is one-to-one (injective) $\iff N(T) = \{ \vec{0} \}$**  
  
Proof)  
  
($\Rightarrow$) If $x \in N(T)$, then $T(x) = \vec{0} = T(\vec{0})$. Since injective, $x = \vec{0}$.  
  
($\Leftarrow$) Suppose $T(x) = T(y)$.  
  
$T(x) - T(y) = \vec{0} \Rightarrow T(x-y) = \vec{0}$  
  
$\Rightarrow x-y \in N(T) = \{ \vec{0} \} \Rightarrow x-y = \vec{0} \Rightarrow x=y$.  
  
**Remark:**  
  
1. $V, W$ finite dim.  
      
    If $\dim V > \dim W$, then no linear transformation from $V$ to $W$ is injective.  
      
    **Proof)** $\dim N(T) = \dim V - \dim R(T) \ge \dim V - \dim W > 0$.  
      
    $N(T) \neq \{ \vec{0} \} \Rightarrow T$ not injective (by Thm 2.4).  
      
    (W의 모든게 대응해도 $\dim R(T) \le \dim W$)  
      
    (V가 다르면 W도 달라야 하는데 공간이 부족)  
      
2. $V, W$ finite-dim.  
      
    If $\dim V < \dim W$, then no linear transformation from $V$ to $W$ is surjective.  
      
    **Proof)** $\dim R(T) = \dim V - \dim N(T) \le \dim V < \dim W$  
      
    $\dim R(T) \neq \dim W \Rightarrow R(T) \neq W$.  
      
3. A homogeneous system of linear equations with more variables than equations has a nonzero solution.  
      
    $\begin{cases} a_{11}x_1 + ... + a_{1n}x_n = 0 \\ \vdots \\ a_{m1}x_1 + ... + a_{mn}x_n = 0 \end{cases}$ ($n > m$)  
      
    $T: \mathbb{F}^n \rightarrow \mathbb{F}^m$, $\begin{pmatrix} x_1 \\ \vdots \\ x_n \end{pmatrix} \mapsto \begin{pmatrix} \sum a_{1j}x_j \\ \vdots \\ \sum a_{mj}x_j \end{pmatrix}$  
      
    $\dim \mathbb{F}^n > \dim \mathbb{F}^m \Rightarrow N(T) \neq \{ \vec{0} \}$  
      
    (해가 $\vec{0}$이 되는 nonzero solution 적어도 하나 존재한다)  
      
  
### Theorem 2.5  
  
$V, W$ finite-dim. $T: V \rightarrow W$ linear.  
  
Suppose $\dim V = \dim W$.  
  
Then TFAE (The Following Are Equivalent):  
  
(a) $T$ is one-to-one (injective)  
  
(b) $T$ is onto (surjective)  
  
(c) rank(T) = dim(V)  
  
Proof)  
  
$(a) \iff N(T) = \{ \vec{0} \}$  
  
$\iff \dim N(T) = 0$  
  
$\iff \dim R(T) = \dim V = \dim W$ ((c))  
  
$\iff R(T) = W$ ((b)) ($\because$ subspace)  
  
**Ex.** Show for each poly $g \in P_n(\mathbb{R})$, there exists a polynomial $f \in P_n(\mathbb{R})$ s.t. $((x^2+5x+7)f)'' = g$.  
  
(finite 아니면 안됨!)  
  
Suppose $g \in P_n(\mathbb{R})$.  
  
Define $T: P_n(\mathbb{R}) \rightarrow P_n(\mathbb{R})$ by $f \mapsto ((x^2+5x+7)f)''$.  
  
$\dim P_n(\mathbb{R})$ is finite.  
  
Check $N(T) = \{ \vec{0} \}$?  
  
$((x^2+5x+7)f)'' = 0 \Rightarrow (x^2+5x+7)f = ax+b$.  
  
Only solution is $f=0$.  
  
$\therefore$ Injective.  
  
By Thm 2.5, it is surjective. $\rightarrow$ For any $g$, $f$ exists.  
  
### Theorem 2.6  
  
$V, W$ vector space over $\mathbb{F}$.  
  
$\{ v_1, ..., v_n \}$ basis for V.  
  
For $w_1, ..., w_n \in W$, there exists a **unique** linear transformation $T: V \rightarrow W$ s.t. $T(v_i) = w_i$ for $i=1, ..., n$.  
  
(basis에 대해 $T(v_i)$값인 $w_1...w_n$만 정해도 unique하게 T가 정해진다.)  
  
**Coro.** $V, W$ vector space. $V$ has finite basis $\{v_1, ..., v_n\}$.  
  
If $U, T: V \rightarrow W$ are linear & $U(v_i) = T(v_i)$ for all $i$, then $T=U$.  
  
Proof)  
  
Define $T: V \rightarrow W$.  
  
$x = \sum a_i v_i$ (basis rep unique) $\mapsto \sum a_i w_i$.  
  
(Defined a map. Let's check if it is linear)  
  
$T(u+v) = T(\sum b_i v_i + \sum c_i v_i) = T(\sum (b_i+c_i) v_i)$  
  
$= \sum (b_i+c_i) w_i = \sum b_i w_i + \sum c_i w_i = T(u) + T(v)$.  
  
$T$ is linear!  
  
**Uniqueness:** Suppose $U$ is linear and $U(v_i) = w_i$.  
  
If $x \in V$, then $U(x) = U(\sum a_i v_i) = \sum a_i U(v_i) = \sum a_i w_i = T(x)$.  
  
$\therefore U = T$.  
  
---  
  
## 3. Matrix Representation of Linear Transformations  
  
**[Def]** An **ordered basis** for $V$ is a basis for $V$ endowed with a specific order.  
  
**Ex.** $\{e_1, ..., e_n\}$: an ordered basis for $\mathbb{F}^n$.  
  
$\beta = \{u_1, ..., u_n\}$ ordered basis for $V$.  
  
$\forall x \in V, \exists! a_1, ..., a_n \in \mathbb{F}$ s.t. $x = \sum_{i=1}^{n} a_i u_i$.  
  
**[Def]** $[x]_\beta := \begin{pmatrix} a_1 \\ \vdots \\ a_n \end{pmatrix} \in \mathbb{F}^n$  
  
**Remark:** $[u_i]_\beta = e_i$ (standard basis vector).  
  
Map $V \rightarrow \mathbb{F}^n$, $x \mapsto [x]_\beta$ is the coordinate vector of x relative to $\beta$.  
  
**Ex.** $V = P_2(\mathbb{R})$, $\beta = \{1, x, x^2\}$.  
  
$f(x) = 4 + 6x - 7x^2 \Rightarrow [f]_\beta = \begin{pmatrix} 4 \\ 6 \\ -7 \end{pmatrix} \in \mathbb{R}^3$.  
  
$V, W$ finite-dim.  
  
$\beta = \{v_1, ..., v_n\}$ ordered basis for V.  
  
$\gamma = \{w_1, ..., w_m\}$ ordered basis for W.  
  
$T: V \rightarrow W$ linear map.  
  
For each $j=1, ..., n$, $T(v_j) \in W$, so $T(v_j) = \sum_{i=1}^{m} a_{ij} w_i$ (unique scalars).  
  
$\Rightarrow \exists! a_{ij} \in \mathbb{F}$ ($1 \le i \le m, 1 \le j \le n$) s.t. ...  
  
Define $A = [a_{ij}] = \begin{pmatrix} a_{11} & \cdots & a_{1n} \\ \vdots & & \vdots \\ a_{m1} & \cdots & a_{mn} \end{pmatrix} = [T]_\beta^\gamma$ (Matrix representation).  
  
**Remark:**  
  
1. If $[U]_\beta^\gamma = [T]_\beta^\gamma$, then $U=T$.  
      
2. ($j$-th column of A) $= [T(v_j)]_\gamma$.  
      
  
**Ex.** $T: P_3(\mathbb{R}) \rightarrow P_2(\mathbb{R})$, $f \mapsto f'$.  
  
$\beta = \{1, x, x^2, x^3\}$ ordered basis for $P_3(\mathbb{R})$.  
  
$\gamma = \{1, x, x^2\}$ ordered basis for $P_2(\mathbb{R})$.  
  
$T(1) = 0 \Rightarrow [T(1)]_\gamma = (0,0,0)^T$  
  
$T(x) = 1 \Rightarrow [T(x)]_\gamma = (1,0,0)^T$  
  
$T(x^2) = 2x \Rightarrow [T(x^2)]_\gamma = (0,2,0)^T$  
  
$T(x^3) = 3x^2 \Rightarrow [T(x^3)]_\gamma = (0,0,3)^T$  
  
$[T]_\beta^\gamma = \begin{pmatrix} 0 & 1 & 0 & 0 \\ 0 & 0 & 2 & 0 \\ 0 & 0 & 0 & 3 \end{pmatrix}$  
  
### Algebra of Linear Transformations  
  
$V, W$ vector spaces over $\mathbb{F}$. $T, U: V \rightarrow W$ maps.  
  
Define operations:  
  
- $(T+U)(x) = T(x) + U(x)$ (Vector addition in W)  
      
- $(aT)(x) = aT(x)$ (Scalar multiplication in W)  
      
  
### Theorem 2.7  
  
(a) $aT+U$ is linear.  
  
(b) Using two operations in (*), the set of all linear transformations from $V$ to $W$ is a vector space over $\mathbb{F}$.  
  
Proof)  
  
(a) $(aT+U)(cx+y) = aT(cx+y) + U(cx+y)$  
  
$= a[cT(x) + T(y)] + cU(x) + U(y)$  
  
$= c[aT(x) + U(x)] + [aT(y) + U(y)]$  
  
$= c(aT+U)(x) + (aT+U)(y)$  
  
(b) (8개 다 체크해야 함 - Must check all 8 axioms)  
  
**Def.** $\mathcal{L}(V, W) :=$ the vector space of all linear transformations from V to W.  
  
$\mathcal{L}(V)$ if $V=W$.  
  
### Theorem 2.8  
  
$T, U: V \rightarrow W$ linear.  
  
Then:  
  
(a) $[T+U]_\beta^\gamma = [T]_\beta^\gamma + [U]_\beta^\gamma$  
  
(b) $[aT]_\beta^\gamma = a[T]_\beta^\gamma$  
  
Proof)  
  
(a) Let $T(v_j) = \sum a_{ij} w_i$ and $U(v_j) = \sum b_{ij} w_i$.  
  
$(T+U)(v_j) = T(v_j) + U(v_j) = \sum (a_{ij} + b_{ij}) w_i$.  
  
So the $(i, j)$ entry is $a_{ij} + b_{ij}$.  
  
(b) similar.  
  
$\Phi: \mathcal{L}(V, W) \longrightarrow M_{m\times n}(\mathbb{F})$, $T \mapsto [T]_\beta^\gamma$  
  
This map depends on the choice of ordered basis.  
  
This map is **linear, injective, & surjective** (Isomorphism).  
  
- Injective (Uniqueness)  
      
- Surjective (Existence from Thm 2.6 Remark)  
      
    (이거 어케 엄밀히 증명하지 Thm 2.8?)  
      
  
### Composition & Matrix Multiplication  
  
$U: W \rightarrow Z$, $T: V \rightarrow W$.  
  
$V \xrightarrow{T} W \xrightarrow{U} Z$.  
  
$UT$: 합성함수 (composition).  
  
### Theorem 2.9  
  
$UT: V \rightarrow Z$ is linear.  
  
**Vector Multiplication (Matrix Multiplication)** $\alpha = \{v_1, ..., v_n\}$ ordered basis of $V$.  
  
$\beta = \{w_1, ..., w_m\}$ ordered basis of $W$.  
  
$\gamma = \{z_1, ..., z_p\}$ ordered basis of $Z$.  
  
Let $A = [U]_\beta^\gamma$, $B = [T]_\alpha^\beta$.  
  
Wanted: $[UT]_\alpha^\gamma = [U]_\beta^\gamma [T]_\alpha^\beta = AB$.  
  
$(UT)(v_j) = U(T(v_j)) = U(\sum_{k=1}^{m} B_{kj} w_k)$  
  
$= \sum_{k=1}^{m} B_{kj} U(w_k)$  
  
$= \sum_{k=1}^{m} B_{kj} (\sum_{i=1}^{p} A_{ik} z_i)$  
  
$= \sum_{i=1}^{p} (\sum_{k=1}^{m} A_{ik} B_{kj}) z_i$  
  
$= \sum_{i=1}^{p} C_{ij} z_i$  
  
where $C_{ij} = \sum_{k=1}^{m} A_{ik} B_{kj}$.  
  
This matches matrix multiplication definition.  
  
(이게 성립되도록 (합성이 잘 되도록) matrix multiplication를 정의)  
  
**Remark:** $TU \neq UT$, likewise  
  
$\begin{pmatrix}1&1\\ 0&0\end{pmatrix}\begin{pmatrix}0&1\\ 1&0\end{pmatrix} \neq \begin{pmatrix}0&1\\ 1&0\end{pmatrix}\begin{pmatrix}1\\ 0&0\end{pmatrix}$  
  
### Theorem 2.10  
  
$V$ vector space. $T, U_1, U_2 \in \mathcal{L}(V)$ (or operators).  
  
Then,  
  
(a) $T(U_1+U_2) = TU_1 + TU_2$  
  
(b) $T(U_1 U_2) = (TU_1)U_2$ (먼저하든 상관 X - Associativity)  
  
(c) $TI = IT = T$  
  
(d) $a(U_1 U_2) = (aU_1)U_2 = U_1(aU_2)$  
  
Similarly for right multiplication...  
  
### Theorem 2.12  
  
$A$ is $m \times n$ matrix. $B, C$ are $n \times p$ matrices. $D, E$ are $q \times m$ matrices.  
  
(a) $A(B+C) = AB + AC$  
  
(b) $a(AB) = (aA)B = A(aB)$  
  
(c) $I_m A = A = A I_n$  
  
$\begin{pmatrix} 1 & 0 & 0 \\ 0 & 1 & 0 \\ 0 & 0 & 1 \end{pmatrix}$  
  
### Theorem 2.13  
  
$A$ is $m \times n$ matrix. $B$ is $n \times p$ matrix.  
  
For $j=1, ..., p$, Let $u_j$ be the $j$-th column of $AB$.  
  
Then **$u_j = A v_j$** where $v_j$ is the $j$-th column of $B$.  
  
**Proof)** $u_j = (AB)_{\cdot j} = \begin{pmatrix} (AB)_{1j} \\ \vdots \\ (AB)_{mj} \end{pmatrix}$  
  
$= \begin{pmatrix} \sum_{k=1}^n A_{1k}B_{kj} \\ \vdots \\ \sum_{k=1}^n A_{mk}B_{kj} \end{pmatrix} = \sum_{k=1}^n B_{kj} \begin{pmatrix} A_{1k} \\ \vdots \\ A_{mk} \end{pmatrix}$  
  
$= A \begin{pmatrix} B_{1j} \\ \vdots \\ B_{nj} \end{pmatrix} = A(v_j)$  
  
**ex)** (entry wise or column wise)  
  
$= \sum_{k=1}^n B_{kj} (\text{k-th column of A})$  
  
($\Rightarrow$ row로도 할 수 있음)  
  
$j$-th column of $B$, $k$-th column of $A$  
  
$\begin{pmatrix}0&1&0&0\\ 0&0&0&0\\ 0&0&0&3\end{pmatrix}\begin{pmatrix}2\\ -4\\ 1\\ 3\end{pmatrix} = 2\begin{pmatrix}0\\ 0\\ 0\end{pmatrix} + (-4)\begin{pmatrix}1\\ 0\\ 0\end{pmatrix} + 1\begin{pmatrix}0\\ 2\\ 0\end{pmatrix} + 3\begin{pmatrix}0\\ 0\\ 3\end{pmatrix}$  
  
### Theorem 2.14  
  
$V, W$ finite-dim vector spaces. $\beta, \gamma$ ordered basis. $T: V \rightarrow W$ linear.  
  
Then **$[T(u)]_\gamma = [T]_\beta^\gamma [u]_\beta$** (나를 보고, T를 한뒤 나의 matrix를 보고 Matrix vector 곱하든, T와 곱하고 보든 같다.)  
  
**Proof)** Fix $u \in V$.  
  
Define $f: \mathbb{F} \rightarrow V$ linear by $a \mapsto au$.  
  
Define $g: \mathbb{F} \rightarrow W$ by $a \mapsto aT(u)$.  
  
Let $\alpha = \{1\}$ ordered basis for $\mathbb{F}$.  
  
Then $g = Tf$.  
  
$[g(1)]_\gamma = [T(u)]_\gamma = [g]_\alpha^\gamma$  
  
(coordinate vector of $g(1)$ matches matrix of $g$ since domain dim is 1)  
  
$= [Tf]_\alpha^\gamma = [T]_\beta^\gamma [f]_\alpha^\beta$  
  
Note $[f(1)]_\beta = [u]_\beta$.  
  
$\therefore [T(u)]_\gamma = [T]_\beta^\gamma [u]_\beta$.  
  
Let $A \in M_{m \times n}(\mathbb{F})$.  
  
$L_A: \mathbb{F}^n \rightarrow \mathbb{F}^m$ (**Left-multiplication transformation**)  
  
$x \mapsto Ax$  
  
### Theorem 2.15  
  
(a) $L_A$ is linear.  
  
(b) If $\beta, \gamma$ are standard ordered bases for $\mathbb{F}^n, \mathbb{F}^m$, then $[L_A]_\beta^\gamma = A$.  
  
(c) $L_A = L_B \iff A = B$.  
  
(d) $L_{A+B} = L_A + L_B$ and $L_{aA} = aL_A$.  
  
(e) If $T: \mathbb{F}^n \rightarrow \mathbb{F}^m$ is linear, then $\exists! C \in M_{m \times n}(\mathbb{F})$ s.t. $T = L_C$.  
  
(f) If $E \in M_{n \times p}(\mathbb{F})$, then $L_{AE} = L_A L_E$.  
  
(g) If $m=n$, then $L_{I_n} = I_{\mathbb{F}^n}$.  
  
**Proof)** (e) Let $C = [T]_\beta^\gamma$.  
  
(f) $j$-th column of $AE$ is $(AE)e_j$ (by Definition).  
  
Also $L_{AE}(e_j) = (AE)e_j$.  
  
$L_A L_E (e_j) = L_A (E e_j) = A(E e_j) = (AE)e_j$.  
  
$\therefore$ Same on basis, so equal.  
  
### Theorem 2.16  
  
$A, B, C$ matrices s.t. $A(BC)$ is defined.  
  
Then $(AB)C$ is defined & **$A(BC) = (AB)C$**.  
  
(size 비고)  
  
**Proof)** $L_{A(BC)} = L_A L_{BC} = L_A (L_B L_C) = (L_A L_B) L_C = L_{AB} L_C = L_{(AB)C}$.  
  
(Composition $(\cdot)$의 특징 $\Rightarrow$ Linear과 matrix가 연관이 깊다는 점을 이용함.)  
  
(What if nonlinear?)  
  
---  
  
## 4. Invertibility & Isomorphism  
  
$V, W$ vector spaces over $\mathbb{F}$. $T: V \rightarrow W$ linear.  
  
A function $U: W \rightarrow V$ is an **inverse** of $T$ if $TU = I_W$ and $UT = I_V$.  
  
If $T$ has an inverse, then $T$ is **invertible**.  
  
$V \xrightarrow{T} W \xrightarrow{U} V$ (Start $V \rightarrow$ Back to $V$)  
  
$W \xrightarrow{U} V \xrightarrow{T} W$ (Start $W \rightarrow$ Back to $W$)  
  
(같은 걸로 돌아옴)  
  
**Remark:**  
  
- If $T$ is invertible, then the inverse of $T$ is unique. (Denoted $T^{-1}$)  
      
    **Why?** Suppose $U_1, U_2$ are inverses.  
      
    $U_1 = U_1 I = U_1 (T U_2) = (U_1 T) U_2 = I U_2 = U_2$.  
      
- $(TU)^{-1} = U^{-1} T^{-1}$  
      
    **Why?** $(TU)(U^{-1}T^{-1}) = T(U U^{-1})T^{-1} = T I T^{-1} = T T^{-1} = I$.  
      
    Similarly for other side.  
      
- $(T^{-1})^{-1} = T$.  
      
    **Why?** Definition.  
      
- **Note:** $T$ is invertible $\iff T$ is one-to-one & onto (Bijective).  
      
    ($\Leftarrow$) $T: V \rightarrow W$.  
      
    $\forall w \in W, \exists! v \in V$ s.t. $T(v)=w$ ($\because$ onto & one-to-one).  
      
    Define $U: W \rightarrow V$ by $w \mapsto v$.  
      
    Check $TU(w) = T(v) = w$.  
      
    Check $UT(v) = U(w) = v$.  
      
    **Claim:** $UT(v) = v$.  
      
    **Why?** $T(UT(v)) = TU(T(v)) = (TU)(T(v)) = T(v)$.  
      
    Since $T$ is one-to-one, $UT(v)=v$.  
      
  
### Theorem 2.17 (Showing inverse is a linear map)  
  
$V, W$ vector spaces over $\mathbb{F}$. $T: V \rightarrow W$ linear & invertible.  
  
Then **$T^{-1}: W \rightarrow V$ is linear.**  
  
**Proof)** Let $y_1, y_2 \in W, c \in \mathbb{F}$.  
  
$\exists! x_1, x_2 \in V$ s.t. $T(x_1)=y_1, T(x_2)=y_2$.  
  
$T^{-1}(cy_1 + y_2)$ should be $cT^{-1}(y_1) + T^{-1}(y_2) = cx_1 + x_2$.  
  
$T(cx_1 + x_2) = cT(x_1) + T(x_2) = cy_1 + y_2$.  
  
Apply $T^{-1}$ to both sides:  
  
$cx_1 + x_2 = T^{-1}(cy_1 + y_2)$.  
  
$\therefore T^{-1}$ is linear.  
  
An $n \times n$ matrix $A$ is **invertible** if $\exists$ $n \times n$ matrix $B$ s.t. $AB = BA = I_n$.  
  
($B = A^{-1}$: inverse of A)  
  
**Lemma** $T: V \rightarrow W$ linear, invertible.  
  
$V$ is finite-dimensional $\iff W$ is finite-dimensional.  
  
In this case, **$\dim V = \dim W$**.  
  
**Proof)** ($\Rightarrow$) Let $\beta = \{x_1, ..., x_n\}$ basis for $V$.  
  
Then $Span(T(\beta)) = R(T) = W$ (since onto).  
  
$\rightarrow W$ is finite-dimensional.  
  
($\Leftarrow$) Use $T^{-1}$ instead of $T$.  
  
In this case ($V, W$ finite-dim),  
  
### Theorem 2.18  
  
(spanned by finite basis)  
  
$\text{nullity}(T) + \text{rank}(T) = \dim V$.  
  
Since $T$ invertible (one-to-one & onto), nullity $= 0$, rank $= \dim W$.  
  
$\therefore 0 + \dim W = \dim V \Rightarrow \dim V = \dim W$.  
  
$V, W$ finite-dimensional v-sp. $\beta, \gamma$ ordered bases. $T: V \rightarrow W$ linear.  
  
Then **$T$ is invertible $\iff [T]_\beta^\gamma$ is invertible.** Moreover, $([T]_\beta^\gamma)^{-1} = [T^{-1}]_\gamma^\beta$.  
  
**Proof)** ($\Rightarrow$) Let $\dim V = \dim W = n$.  
  
$[T]_\beta^\gamma$ is an $n \times n$ matrix.  
  
$[T^{-1}]_\gamma^\beta [T]_\beta^\gamma = [T^{-1} T]_\beta^\beta = [I]_\beta^\beta = I_n$.  
  
($\Leftarrow$) Let $[T]_\beta^\gamma = A$ be invertible.  
  
$\Phi: \mathcal{L}(V, W) \rightarrow M_{n \times n}(\mathbb{F})$ is an isomorphism.  
  
$\exists! U \in \mathcal{L}(W, V)$ s.t. $[U]_\gamma^\beta = A^{-1}$.  
  
Then $[UT]_\beta^\beta = [U]_\gamma^\beta [T]_\beta^\gamma = A^{-1} A = I_n$.  
  
$\Rightarrow UT = I_V$.  
  
Likewise $TU = I_W$.  
  
$\therefore T$ is invertible.  
  
**[Def]** $V, W$ vector spaces.  
  
$V$ is **isomorphic** to $W$ if $\exists$ linear transformation $T: V \rightarrow W$ that is invertible.  
  
(Note: "is isomorphic to" is an equivalence relation: $V \cong V$; $V \cong W \rightarrow W \cong V$; $V \cong W, W \cong Z \rightarrow V \cong Z$.)  
  
### Theorem 2.19  
  
$V, W$ finite dimensional.  
  
**$V$ is isomorphic to $W \iff \dim V = \dim W$.**  
  
**Proof)** ($\Rightarrow$) By Lemma.  
  
($\Leftarrow$) Let $\dim V = \dim W = n$.  
  
$\beta = \{v_1, ..., v_n\}$ basis for $V$.  
  
$\gamma = \{w_1, ..., w_n\}$ basis for $W$.  
  
Let's show $\exists$ invertible linear transformation $T: V \rightarrow W$.  
  
Define unique $T$ s.t. $T(v_i) = w_i$ (sends basis to basis).  
  
Then $[T]_\beta^\gamma = I_n$.  
  
Since $I_n$ is invertible, $T$ is invertible (by Thm 2.18).  
  
**Coro.** $V$ vector space over $\mathbb{F}$.  
  
Then **$V$ is isomorphic to $\mathbb{F}^n \iff \dim(V) = n$.**  
  
**Remark** Coro is important.  
  
ex) $V$ (abstract) $\leftrightarrow \mathbb{F}^n$ (concrete, compute).  
  
이게 가능.  
  
If $\beta$ is basis, $T(\beta)$ is also basis!  
  
여기가 쉬우니까, 여기 basis와 $T$ 알면 basis가 나온다.  
  
ex) $N(T)$를 알고 싶어...  
  
$\Rightarrow N(L_A)$를 구하고 $\phi_\beta^{-1}$를 하면 된다!  
  
$\rightarrow N(L_A)$를 어떻게 구하죠? Ch.3에서...!  
  
$\dim V = n$. $x \in V$.  
  
$\phi_\beta: V \rightarrow \mathbb{F}^n$, $x \mapsto [x]_\beta$.  
  
Check that this is isomorphism!  
  
$L_A \phi_\beta = \phi_\gamma T$.  
  
**Why?** $A [x]_\beta = [T(x)]_\gamma$.  
  
(This implies $[T]_\beta^\gamma [x]_\beta = [T(x)]_\gamma$, which is Thm 2.14).  
  
---  
  
## 5. The Change of Coordinate Matrix  
  
### Theorem 2.22  
  
$V$ finite-dimension. $\beta, \beta'$ ordered basis of $V$.  
  
Let's find $Q$ s.t. $Q = [I_V]_{\beta'}^\beta$.  
  
(a) $Q$ is invertible.  
  
(b) **$[v]_\beta = Q [v]_{\beta'}$** (changes the basis)  
  
(changes $\beta'$-coordinates into $\beta$-coordinates).  
  
**Remark 1:** $Q^{-1}$: changes $\beta$ to $\beta'$ coordinates.  
  
**Remark 2:** $\beta = \{x_1, ..., x_n\}$, $\beta' = \{x'_1, ..., x'_n\}$.  
  
($j$-th column of $Q$) $= [I_V(x'_j)]_\beta = [x'_j]_\beta$.  
  
### Theorem 2.23  
  
$V$ finite-dim. $T \in \mathcal{L}(V)$ (linear operator $T: V \rightarrow V$).  
  
$\beta, \beta'$ ordered bases.  
  
Let $Q = [I_V]_{\beta'}^\beta$.  
  
Then **$[T]_{\beta'} = Q^{-1} [T]_\beta Q$.**  
  
**Proof)** $[T]_{\beta'} = [T]_{\beta'}^{\beta'} = [I_V T I_V]_{\beta'}^{\beta'}$  
  
$= [I_V]_{\beta}^{\beta'} [T]_\beta^\beta [I_V]_{\beta'}^\beta$  
  
$= Q^{-1} [T]_\beta Q$.  
  
**Ex.** $T: \mathbb{R}^2 \rightarrow \mathbb{R}^2$ reflection about the line $y = 2x$.  
  
$T\begin{pmatrix}1\\ 2\end{pmatrix} = \begin{pmatrix}1\\ 2\end{pmatrix}$ (on the line, invariant)  
  
$T\begin{pmatrix}-2\\ 1\end{pmatrix} = -\begin{pmatrix}-2\\ 1\end{pmatrix}$ (orthogonal to line, flipped)  
  
Let $\beta' = \{ \begin{pmatrix}1\\ 2\end{pmatrix}, \begin{pmatrix}-2\\ 1\end{pmatrix} \}$.  
  
$[T]_{\beta'} = \begin{pmatrix} 1 & 0 \\ 0 & -1 \end{pmatrix}$.  
  
Let $\beta = \{ e_1, e_2 \}$ standard basis.  
  
Wanted: $[T]_\beta$.  
  
$[T]_\beta = Q [T]_{\beta'} Q^{-1}$ where $Q = [I]_{\beta'}^\beta = \begin{pmatrix} 1 & -2 \\ 2 & 1 \end{pmatrix}$.  
  
$Q^{-1} = \frac{1}{5} \begin{pmatrix} 1 & 2 \\ -2 & 1 \end{pmatrix}$.  
  
(Note: $\begin{pmatrix}a&b\\ c&d\end{pmatrix}^{-1} = \frac{1}{ad-bc}\begin{pmatrix}d&-b\\ -c&a\end{pmatrix}$)  
  
$[T]_\beta = \begin{pmatrix} 1 & -2 \\ 2 & 1 \end{pmatrix} \begin{pmatrix} 1 & 0 \\ 0 & -1 \end{pmatrix} \frac{1}{5} \begin{pmatrix} 1 & 2 \\ -2 & 1 \end{pmatrix}$  
  
$= \frac{1}{5} \begin{pmatrix} 1 & 2 \\ 2 & -1 \end{pmatrix} \begin{pmatrix} 1 & 2 \\ -2 & 1 \end{pmatrix}$  
  
$= \frac{1}{5} \begin{pmatrix} -3 & 4 \\ 4 & 3 \end{pmatrix}$.  
  
Check: $T\begin{pmatrix}a\\ b\end{pmatrix} = \frac{1}{5} \begin{pmatrix} -3 & 4 \\ 4 & 3 \end{pmatrix} \begin{pmatrix}a\\ b\end{pmatrix}$.  
  
**[Def]** $A, B \in M_{m \times n}(\mathbb{F})$.  
  
$B$ is **similar** to $A$ if $\exists$ invertible matrix $Q$ s.t. **$B = Q^{-1} A Q$**.  
  
**Ex. (proof)** $V$ vector space of dim $n$.  
  
$A \in M_{n \times n}(\mathbb{F})$ and $A$ is invertible.  
  
$\exists$ ordered bases $\beta, \gamma$ of $V$ s.t. $[I_V]_\beta^\gamma = A$.
---  
tags:  
  - vector-space  
share: "true"  
github_title: 2024-09-02-vector-space  
title: 1. Vector Space  
date: 2024-09-02  
categories:  
  - Lecture Notes  
  - Linear Algebra  
math: "true"  
---  
## Introduction  
  
$\rightarrow$ Friedberg & Done Right (Axler)  
  
- **Mid:** 10/24 목 18:00~20:30  
      
- **Final:** 12/12 목  
      
- Solution of linear equations.  
      
  
---  
  
## #1.2 Vector spaces  
  
### Set: $\mathbb{R}^{2}$  
  
- addition.  
      
- scalar multiplication.  
      
  
### Definition  
  
A vector space $V$ over a field $F$ (usually $\mathbb{R}$ or $\mathbb{C}$) is a non-empty set $V$ equipped with two operations (addition & scalar multiplication) satisfying the following axioms:  
  
- Addition: $\forall x, y \in V, x+y \in V$  
      
- Scalar multiplication: For each $a \in F, x \in V, ax \in V$  
      
  
### Axioms  
  
- **(VS1)** $\forall x, y \in V, x+y = y+x$ (교환)  
      
- **(VS2)** $\forall x, y, z \in V, (x+y)+z = x+(y+z)$ (결합)  
      
- **(VS3)** $\exists 0 \in V$ s.t. $x+0=x$ for all $x \in V$.  
      
- **(VS4)** $\forall x \in V, \exists y \in V$ s.t. $x+y=0$.  
      
- **(VS5)** $\forall x \in V, 1x=x$  
      
- **(VS6)** $\forall a, b \in F, \forall x \in V, (ab)x = a(bx)$  
      
- **(VS7)** $\forall a \in F, \forall x, y \in V, a(x+y) = ax + ay$  
      
- **(VS8)** $\forall a, b \in F, \forall x \in V, (a+b)x = ax + bx$  
      
  
$\hookrightarrow$ 이걸 만족하면 V.S.로 가정하고 나중에 쓸 수 있음. (thm, Coro...)  
  
### Examples  
  
**Ex.** $M_{m \times n}(F) = \{ \begin{pmatrix} a_{11} & \dots & a_{1n} \\ \vdots & & \vdots \\ a_{m1} & \dots & a_{mn} \end{pmatrix} : a_{ij} \in F \}$  
  
- addition: $(A+B)_{ij} = A_{ij} + B_{ij}$  
      
- s-mult: $(cA)_{ij} = cA_{ij}$  
      
    $\rightarrow$ 모두 VS axiom 만족 $\rightarrow$ Vector Space 이다.  
      
  
**Ex)**  
  
- non empty set $S$  
      
- field $F$  
      
- Vector spaces over $F$.  
      
- $F(S, F) =$ the set of functions from $S$ to $F$.  
      
    - $(f+g)(s) = f(s) + g(s)$  
          
    - $(cf)(s) = c(f(s))$  
          
  
**Not ex.**  
  
- $C(\mathbb{R}) =$ the set of continuous functions $\mathbb{R} \to \mathbb{R}$  
      
- $S = \{(a_1, a_2) : a_1, a_2 \in \mathbb{R}\}$  
      
    - $(a_1, a_2) + (b_1, b_2) = (a_1+b_1, a_2+b_2)$  
          
    - $c(a_1, a_2) = (ca_1, a_2)$  
          
- **VS1, VS2, VS8 fail.**  
      
  
### Theorem 1.1  
  
$V \rightarrow$ vector space, $x, y, z \in V$.  
  
If $x+z = y+z$, then $x=y$.  
  
proof)  
  
$\exists v \in V$ s.t. $z+v=0$ (VS4)  
  
$x = x+0$ (VS3)  
  
$= x+(z+v)$  
  
$= (x+z)+v$ (VS2)  
  
$= (y+z)+v$  
  
$= y+(z+v)$  
  
$= y+0$  
  
$= y$  
  
Coro 1. The zero vector $0$ is unique.  
  
Coro 2. The vector $y$ in [VS4] (additive inverse) is unique (denoted $-x$).  
  
Ex) Polynomial with coefficients from $F$.  
  
$f(x) = a_n x^n + a_{n-1} x^{n-1} + \dots + a_1 x + a_0$  
  
$P(F)$: the set of polynomials.  
  
$P_n(F) =$ the set of all polynomials having degree $\le n$.  
  
(Zero function degree $-\infty$ 라 하면 $P_n(F) \subseteq P(F)$).  
  
### Theorem 1.2  
  
Vector space $V$, $\forall x \in V$, $\forall a \in F$  
  
(a) $0 \cdot x = 0$  
  
(b) $(-a)x = -(ax) = a(-x)$  
  
(c) $a \cdot 0 = 0$  
  
---  
  
## #1.3 Subspaces  
  
$V$ vector space over $F$.  
  
$W \subseteq V$  
  
### Definition  
  
$W$ is a subspace of $V$ if $W$ is a Vector space over $F$ with the operations on $V$.  
  
Trivial) $\{0\} \subseteq V$, $V \subseteq V$.  
  
$\rightarrow$ A subset $W$ of $V$ is a subspace iff:  
  
1. $\forall x, y \in W, x+y \in W$  
      
2. $\forall x \in W, \forall c \in F, cx \in W$  
      
3. $W$ should have a zero vector (to satisfy VS3).  
      
4. Each vector in $W$ has an additive inverse in $W$ (to satisfy VS4).  
      
    ($\hookrightarrow$ 나머지는 $V$ subset 이라 자동 만족).  
      
  
### Theorem 1.3  
  
$V$ vector space over $F$. $W \subseteq V$.  
  
Then $W$ is a subspace of $V$ iff:  
  
1. $0 \in W$  
      
2. $x+y \in W$ whenever $x, y \in W$ (Closed under addition)  
      
3. $cx \in W$ whenever $c \in F, x \in W$ (Closed under scalar mult)  
      
  
pf) ($\Rightarrow$)  
  
$0 \dots$  
  
$\exists 0_W \in W$ s.t. $x+0_W = x, \forall x \in W$  
  
$x+0_W = x = x+0_V$ (in $V$, also in $W$)  
  
$0_W = 0_V$ (by Thm 1.1)  
  
($\Leftarrow$)  
  
(4) 부분만 증명하면 됨.  
  
If $x \in W$, then $(-1)x \in W$.  
  
$(-1)x = -x$  
  
Closed under scalar multiplication (since $-1 \in F$).  
  
닫혀있기때문 ($-1$이 $F$에 있으면)  
  
**Ex**  
  
- $W = \{A \in M_{n \times n}(F) : A^t = A\}$ (Symmetric matrices)  
      
    - $A^t$ is transpose of $A$.  
          
    - $(A^t)_{ij} = A_{ji}$ 라 하자.  
          
    - $W$ is a subspace of $V = M_{n \times n}(F)$.  
          
  
---  
  
## #1.4 Linear combination & System of linear equations  
  
In $\mathbb{R}^2$, $z = sx + ty$.  
  
### Definition: Linear combination  
  
A vector $v \in V$ is a Linear combination of vectors of $S$ if there exist a finite number of vectors $u_1, \dots, u_n \in S$ and scalars $a_1, \dots, a_n \in F$ such that:  
  
$v = a_1 u_1 + \dots + a_n u_n$  
  
Ex) $v = \begin{pmatrix} 3 \\ 4 \\ 5 \end{pmatrix} \in \mathbb{R}^3$.  
  
$u_1 = \begin{pmatrix} 1 \\ 1 \\ 1 \end{pmatrix}, u_2 = \begin{pmatrix} 1 \\ 2 \\ 3 \end{pmatrix}, u_3 = \begin{pmatrix} 0 \\ 1 \\ 2 \end{pmatrix}$.  
  
Is $v$ a linear comb of $u_1, u_2, u_3$?  
  
$v = a_1 u_1 + a_2 u_2 + a_3 u_3$  
  
$\begin{pmatrix} 3 \\ 4 \\ 5 \end{pmatrix} = \begin{pmatrix} a_1 + a_2 \\ a_1 + 2a_2 + a_3 \\ a_1 + 3a_2 + 2a_3 \end{pmatrix}$  
  
$\rightarrow \begin{cases} a_1 + a_2 = 3 \\ a_1 + 2a_2 + a_3 = 4 \\ a_1 + 3a_2 + 2a_3 = 5 \end{cases}$  
  
Result: $0=0$.  
  
$a_1 = a_3+2$  
  
$a_2 = -a_3+1$  
  
Ex 2) $v = \begin{pmatrix} 3 \\ 4 \\ 7 \end{pmatrix}?$  
  
System leads to $0=2$ (Contradiction).  
  
$\rightarrow$ Not a linear combination.  
  
### Definition: Span  
  
$S$: nonempty subset of $V$.  
  
The span of S ($span(S)$) is the set of all linear combinations of the vectors in $S$.  
  
($span(S)$ is always subspace?)  
  
### Theorem 1.5  
  
The span of any subset $S$ of $V$ is a subspace of $V$.  
  
Any subspace $W$ of $V$ that contains $S$ must contain $span(S)$.  
  
($span(S)$ is the smallest subspace which contains $S$).  
  
**Proof)**  
  
1. Since $S \neq \emptyset$, $\exists z \in S$.  
      
    $0z = 0 \in span(S)$.  
      
2. Let $x, y \in span(S)$.  
      
    $x = a_1 u_1 + \dots + a_m u_m, \quad u_i \in S$  
      
    $y = b_1 v_1 + \dots + b_n v_n, \quad v_i \in S$  
      
    $x+y = a_1 u_1 + \dots + a_m u_m + b_1 v_1 + \dots + b_n v_n \in span(S)$  
      
3. $cx = (ca_1)u_1 + \dots + (ca_m)u_m \in span(S)$.  
      
  
Claim: $span(S) \subseteq W$.  
  
Let $w \in span(S)$.  
  
$w = c_1 w_1 + \dots + c_k w_k$ where $w_i \in S \subseteq W$.  
  
Since $W$ is a subspace, $c_i w_i \in W$ and their sum is in $W$.  
  
$\therefore w \in W$.  
  
### Definition: Generating Set  
  
A subset $S$ of $V$ **generates** (or spans) $V$ if $span(S) = V$.  
  
Ex) $S = \{ \begin{pmatrix} 1 \\ 0 \end{pmatrix}, \begin{pmatrix} 1 \\ 1 \end{pmatrix}, \begin{pmatrix} 0 \\ 1 \end{pmatrix} \}$  
  
Isn't it redundant?  
  
l-dep!  
  
Spans $\mathbb{R}^2$.  
  
---  
  
## #1.5 Linear dependence and linear independence  
  
$\mathbb{R}^2 = span(S) = span \{v_1, v_2, v_3\}$.  
  
"Let's find linear comb of $v_1, v_2, v_3$ that is zero (can be removed!)."  
  
(Smallest set!)  
  
$(-1)v_1 + (-1)v_2 + (1)v_3 = 0$.  
  
(non-trivial!)  
  
### Definition  
  
$S$ is Linearly dependent if there exist finitely many distinct vectors $u_1, \dots, u_n \in S$ and scalars $a_1, \dots, a_n$ not all zero s.t.  
  
$a_1 u_1 + \dots + a_n u_n = 0$.  
  
Otherwise, $S$ is Linearly independent.  
  
$\Rightarrow a_1 u_1 + \dots + a_n u_n = 0 \Rightarrow a_1 = \dots = a_n = 0$ (Only trivial solution exists).  
  
(0를 만드려면 trivial 밖에 없다.)  
  
Ex) If $u \neq 0$, then $\{u\}$ is linearly independent. (Note: $\{0\}$ is l-dep).  
  
Why? 대우 증명.  
  
$\{u\}$ linearly dependent $\rightarrow au=0$ with $a \neq 0$.  
  
$a^{-1}(au) = a^{-1}0 \Rightarrow 1u = 0 \Rightarrow u=0$.  
  
### Theorem 1.6  
  
Let $S_1 \subseteq S_2 \subseteq V$.  
  
1. If $S_1$ is linearly dep, then so is $S_2$.  
      
2. If $S_2$ is linearly indep, then so is $S_1$.  
      
  
Ex  
  
$(-1)\begin{pmatrix} 0 \\ 1 \\ 0 \end{pmatrix} + 2\begin{pmatrix} 0 \\ 0 \\ 0 \end{pmatrix} + \dots = 0$.  
  
### Theorem 1.7  
  
$S \subseteq V$, $S$ linearly indep.  
  
Then $S \cup \{v\}$ is linearly dependent iff $v \in span(S)$.  
  
pf)  
  
($\Rightarrow$)  
  
$S \cup \{v\}$ is l-dep.  
  
$\exists u_1, \dots, u_n \in S \cup \{v\}$ s.t. $a_1 u_1 + \dots + a_n u_n = 0$ for some non-zero scalars.  
  
$\exists i \in \{1, \dots, n\}$ s.t. $u_i = v$ ($S$가 l-indep이라 살아있어야함).  
  
$a_1 v + a_2 u_2 + \dots + a_n u_n = 0$ ($a_1 \neq 0$).  
  
$v = -a_1^{-1} (a_2 u_2 + \dots + a_n u_n) \in span(S)$.  
  
($\Leftarrow$)  
  
$v \in span(S)$.  
  
$v = b_1 v_1 + \dots + b_m v_m$ with $v_i \in S$.  
  
(distinct. 같으면 합쳐지니까)  
  
$b_1 v_1 + \dots + b_m v_m + (-1)v = 0$.  
  
So $\{v_1, \dots, v_m, v\}$ is linearly dependent.  
  
By Thm 1.6, $S \cup \{v\}$ is l-dep.  
  
**Remark:** $span(S) = span(S \cup \{v\})$ (if $v \in span(S)$).  
  
---  
  
## #1.6 Basis and dimension  
  
### Definition: Basis  
  
A **basis** for a vector space $V$ is a linearly independent subset of $V$ that generates $V$.  
  
Ex 1) $\{ (1, 0, \dots, 0), \dots, (0, \dots, 0, 1) \} = \{e_1, \dots, e_n\}$ is a basis for $F^n$.  
  
Ex 3) $\{1, x, x^2, \dots \}$ is a basis for $P(F)$.  
  
### Theorem 1.8  
  
Let $\beta = \{u_1, \dots, u_n\}$ be a basis for $V$.  
  
Then each $v \in V$ can be uniquely expressed as a linear combination of vectors in $\beta$.  
  
Pf)  
  
($\Rightarrow$) Existence: $V = span(\beta)$, so $v = a_1 u_1 + \dots + a_n u_n$.  
  
Uniqueness:  
  
Suppose $v = a_1 u_1 + \dots + a_n u_n$ and $v = b_1 u_1 + \dots + b_n u_n$.  
  
$0 = v-v = (a_1-b_1)u_1 + \dots + (a_n-b_n)u_n$.  
  
Since $u_i$ are l-indep, $a_i - b_i = 0 \Rightarrow a_i = b_i$.  
  
($\Leftarrow$)  
  
Every $v \in span(\beta)$.  
  
(l-indep unique 하기 때문에?)  
  
### Theorem 1.9  
  
If $V$ is generated by a finite set $S$, then $\exists \beta \subseteq S$ such that $\beta$ is a basis for $V$. (Hence $V$ has a finite basis).  
  
pf)  
  
If $V = \{0\}$, $\beta = \emptyset$.  
  
Otherwise, $u_1 \in S, u_1 \neq 0$. $\{u_1\}$ is linearly independent.  
  
Add vectors $u_2, \dots, u_k \in S$ as many as possible with the property that $\{u_1, \dots, u_k\}$ is linearly indep. ($S$가 finite 이라 가능).  
  
Let $\beta = \{u_1, \dots, u_k\}$.  
  
Claim: $S \subseteq span(\beta)$.  
  
$span(S) \subseteq span(\beta) \subseteq V$, so $V = span(\beta)$.  
  
For $v \in S$:  
  
If $v \in \beta$, then $v \in span(\beta)$.  
  
Otherwise, $v \notin \beta$, then $\beta \cup \{v\}$ is l-dep. ($\because$ 앞에서 넣을만큼 다 넣어서)  
  
$\rightarrow v \in span(\beta)$ (by Thm 1.7).  
  
Example:  
  
$S = \{ \begin{pmatrix} 2 \\ -3 \\ 5 \end{pmatrix}, \begin{pmatrix} 8 \\ -12 \\ 20 \end{pmatrix}, \begin{pmatrix} 1 \\ 0 \\ -2 \end{pmatrix}, \begin{pmatrix} 0 \\ 2 \\ -4 \end{pmatrix}, \dots \}$  
  
$\beta = \{ \begin{pmatrix} 2 \\ -3 \\ 5 \end{pmatrix}, \begin{pmatrix} 1 \\ 0 \\ -2 \end{pmatrix}, \begin{pmatrix} 0 \\ 2 \\ -4 \end{pmatrix} \}$ is a basis for $V$.  
  
### Theorem 1.10 (Replacement Theorem)  
  
$G, L \subseteq V$.  
  
$V = span(G)$, $G$ has $n$ vectors.  
  
$L$ is linearly indep, $L$ has $m$ vectors.  
  
Then $m \le n$ and $\exists H \subseteq G$ s.t. $\#H = n-m$ and $V = span(L \cup H)$.  
  
Coro 1:  
  
($G$를 대체할 수 있다.)  
  
$V$ a vector space having a finite basis $\beta$.  
  
Then every basis $\gamma$ for $V$ contains the same number of vectors. ($= \text{dimension}$).  
  
pf)  
  
$\#\gamma \le \#\beta$ (by Replacement theorem).  
  
$\#\beta \le \#\gamma$  
  
$\therefore \#\beta = \#\gamma$.  
  
Proof of Replacement Theorem  
  
proof) Induction on $m$.  
  
1. **$m=0$**: $L = \emptyset$, and $H=G$ works.  
      
2. Suppose the thm is true for $m \ge 0$.  
      
    We want to show that it is true for $m+1$.  
      
    $L = \{v_1, \dots, v_m, v_{m+1}\}$  
      
    $L' = \{v_1, \dots, v_m\}$  
      
    By induction hypothesis, $m \le n$ & $\exists H' = \{u_1, \dots, u_{n-m}\} \subseteq G$ s.t. $V = span(L' \cup H')$.  
      
    So, $v_{m+1} = a_1 v_1 + \dots + a_m v_m + b_1 u_1 + \dots + b_{n-m} u_{n-m}$.  
      
    Note: $n-m \ge 1$ (otherwise $L$ would be dependent) and some $b_i \neq 0$.  
      
    $-b_i u_i = a_1 v_1 + \dots + a_m v_m + (-1)v_{m+1} + \dots$  
      
    $\Rightarrow u_i \in span(L \cup \{u_1, \dots, u_{i-1}, u_{i+1}, \dots, u_{n-m}\})$.  
      
    Then $L' \cup H' \subseteq span(L \cup H)$ where $H = H' \setminus \{u_i\}$.  
      
    $span(L' \cup H') \subseteq span(L \cup H)$.  
      
    $\Rightarrow V = span(L \cup H)$.  
      
  
Coro 1: $V$ a vector space having a finite basis.  
  
Then every basis for $V$ contains the same number of vectors.  
  
$\#\beta = \text{dimension } V = \dim V$.  
  
Otherwise, it is infinite-dimensional.  
  
**Ex**  
  
1. $\dim \{0\} = 0$  
      
2. $\dim F^n = n$  
      
3. $\dim M_{m \times n}(F) = mn$  
      
4. $\dim P_n(F) = n+1$  
      
5. $P(F)$ is infinite-dimensional.  
      
6. $\mathbb{C}$ is vector space over $\mathbb{C} \rightarrow \dim \mathbb{C} = 1$.  
      
    $\mathbb{C}$ is a vector space over $\mathbb{R} \rightarrow \dim \mathbb{C} = 2$.  
      
    (Field 에 따라 달라진다.)  
      
  
Coro 2. $V$ is a vector space with $\dim V = n$. $S \subseteq V$ (finite).  
  
(a) If $span(S) = V$, then $\#S \ge n$.  
  
If $span(S) = V$ & $\#S = n$, then $S$ is a basis for $V$.  
  
(b) If $S$ is linearly indep, then $\#S \le n$.  
  
If $S$ is linearly indep & $\#S = n$, then $S$ is a basis for $V$.  
  
(c) Every linearly indep subset of $V$ can be extended to a basis for $V$.  
  
pf)  
  
(a) $\exists T \subseteq S$ s.t. $T$ is a basis for $V$ (by Thm 1.9).  
  
$\#T = n \implies T=S$ if $\#S=n$.  
  
(c) $\beta$ is a basis for $V$.  
  
$\exists T \subseteq \beta$ s.t. $\#T = n - \#S$ & $span(S \cup T) = V$ (Replacement theorem).  
  
$n \le \#(S \cup T) \le n$.  
  
$\Rightarrow S \cup T$ is a basis for $V$.  
  
(b) $S$ can be extended to a basis $\gamma$ for $V$.  
  
$n = \#S \le \#\gamma = n$.  
  
$\therefore S = \gamma \Rightarrow S$ is a basis for $V$.  
  
### Theorem 1.11  
  
$V$ is finite-dimensional. $W$ subspace of $V$.  
  
Then $W$ is finite-dimensional & $\dim(W) \le \dim(V)$.  
  
Moreover, if $\dim(W) = \dim(V)$, then $W=V$.  
  
proof $n = \dim(V)$.  
  
If $W = \{0\}$, then (v).  
  
Otherwise, $W$ contains a nonzero vector $x_1$.  
  
$\{x_1\}$ linearly indep.  
  
$S = \{x_1, x_2, \dots, x_k\} \rightarrow$ stops at finite point $k$ ($k \le n$).  
  
($\because V$ is finite dimensional $\rightarrow$ has limited l-indep vectors).  
  
$span(S) \subseteq W \dots$ (1)  
  
$\forall v \in W$:  
  
If $v \in S$, done.  
  
If $S \cup \{v\}$ is l-dep $\Rightarrow v \in span(S)$.  
  
$\therefore W \subseteq span(S) \dots$ (2)  
  
(1), (2) $\Rightarrow W = span(S)$.  
  
$\therefore \dim W = k \le n = \dim V$.  
  
If $\dim(W) = n$, then a basis $\beta$ for $W$ is linearly indep, $\#\beta = \dim V = n$.  
  
$\Rightarrow \beta$ is a basis for $V$ (by Thm 1.10 (b)).  
  
### Lagrange Interpolation formula  
  
$P_n(F)$.  
  
$f_i(x) = \frac{(x-c_0)(x-c_1)\dots(x-c_{i-1})(x-c_{i+1})\dots(x-c_n)}{(c_i-c_0)(c_i-c_1)\dots \dots (c_i-c_n)}$  
  
($c_i$ 제외한 $x$들).  
  
$f_i(c_j) = \begin{cases} 0 & (i \neq j) \\ 1 & (i = j) \end{cases}$  
  
Claim: $\beta = \{f_0, f_1, \dots, f_n\}$ is linearly indep.  
  
Why? $a_0 f_0 + \dots + a_n f_n = 0$  
  
($c_i$ 대입). $a_i = 0$.  
  
$\therefore a_i = 0, \forall i = 0, \dots, n$.  
  
$\beta$ has $n+1$ vectors (and $\dim P_n(F) = n+1$) $\rightarrow \beta$ generates $P_n(F) \rightarrow \beta$ is a basis.  
  
Find $g \in P_n(F)$ s.t. $g(c_i) = b_i, \forall i = 0, \dots, n$.  
  
$g = b_0 f_0 + \dots + b_n f_n$.  
  
$g$ is unique (basis에 의한 표현은 unique 하니까).  
  
$\Rightarrow$ **Lagrange Interpolation formula.**
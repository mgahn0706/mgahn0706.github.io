---  
tags:  
  - matrix  
  - linear-equation  
share: "true"  
github_title: 2024-09-23-linear-transformations-and-matrices  
title: 2. Linear Transformations and Matrices  
date: 2024-09-23  
categories:  
  - Lecture Notes  
  - Linear Algebra  
math: "true"  
---  
# Elementary Matrix Operations & System of Linear Equations  
  
**[Def]** $A \in M_{m \times n}(\mathbb{F})$  
  
Example:  
  
$x + 2y + 3z = 5$  
  
$-x + y - z = -3$  
  
$0x + 3y + 0z = 8$  
  
이렇게 하는 걸 Matrix 로 배운다.  
  
**Elementary Row Operations:**  
  
1. **Type 1:** Interchange any two rows of A.  
      
2. **Type 2:** Multiply any row of A by a nonzero scalar.  
      
3. **Type 3:** Add any scalar multiple of a row of A to another row.  
      
  
Ex: $(\begin{matrix}1&2&3\\ 4&5&6\end{matrix}) \xrightarrow{R_1 \leftrightarrow R_2} (\begin{matrix}4&5&6\\ 1&2&3\end{matrix})$  
  
$(\begin{matrix}2&4&6\\ 4&5&6\end{matrix})$  
  
$(\begin{matrix}1&2&3\\ 6&9&12\end{matrix})$  
  
"Elementary row operation"  
  
(also in column operation!)  
  
**[Def]** An $n \times n$ **elementary matrix** is a matrix obtained by applying an elementary operation on $I_n$.  
  
### Thm 3.1  
  
Let $A \in M_{m \times n}(\mathbb{F})$.  
  
If $B$ is obtained from $A$ by applying an elementary row operation, and $E$ is obtained from $I_m$ by the same elementary row operation,  
  
Then $B = EA$.  
  
(Note: If column operation, $B = AE$ where $E$ is from $I_n$)  
  
Proof) (Case: Type 3)  
  
Suppose $r \ne s$. Add $c$ times row $s$ to row $r$.  
  
$E_{ik} = \begin{cases} 1 & i=k \\ c & i=r, k=s \\ 0 & \text{otherwise} \end{cases}$ (This represents $I_m$ modified)  
  
$(EA)_{ij} = \sum_{k=1}^{n} E_{ik} A_{kj} = \begin{cases} A_{ij} & i \ne r \\ A_{rj} + c A_{sj} & i = r \end{cases}$  
  
This is exactly the same as $B_{ij}$!  
  
### Thm 3.2  
  
Elementary matrices are invertible, and the inverse of an elementary matrix is an elementary matrix of the same type.  
  
($E^{-1}$ exists and is elementary).  
  
Proof) $E \bar{E} = I_n$  
  
Define $\bar{E}$ as the matrix of the reverse operation.  
  
(단순 Thm 3.1의 연장선)  
  
Since $E \bar{E} = I_n$, $E$ and $\bar{E}$ are invertible.  
  
(사실 $AB=I_n \Rightarrow BA=I_n$)  
  
[Def] $A \in M_{m \times n}(\mathbb{F})$.  
  
$L_A: \mathbb{F}^n \rightarrow \mathbb{F}^m$, $x \mapsto Ax$.  
  
rank A $:= \text{rank } L_A$.  
  
### Thm 3.3  
  
$V, W$ finite dimensional, $\beta, \gamma$ ordered basis.  
  
$T: V \rightarrow W$ linear.  
  
Then $\text{rank}(T) = \text{rank}([T]_\beta^\gamma)$.  
  
Note: $V, W$ finite-dimensional.  
  
$T: V \rightarrow W$ isomorphism.  
  
$V_0$: subspace of V.  
  
Then $T(V_0) = \{ T(x) : x \in V_0 \}$ is a subspace of W, and $\dim(V_0) = \dim(T(V_0))$.  
  
Why? $T|_{V_0}: V_0 \rightarrow W$ given by $x \mapsto T(x)$.  
  
$R(T|_{V_0}) = T(V_0)$.  
  
Since $T$ is isomorphism (injective), $T|_{V_0}$ is injective.  
  
$\therefore T|_{V_0}: V_0 \rightarrow T(V_0)$ is an isomorphism. So $\dim(V_0) = \dim(T(V_0))$.  
  
Proof of Thm 3.3  
  
$T: V \rightarrow W$. Let $A = [T]_\beta^\gamma$.  
  
Diagram:  
  
$V \xrightarrow{T} W$  
  
$\phi_\beta \downarrow \quad \quad \downarrow \phi_\gamma$  
  
$\mathbb{F}^n \xrightarrow{L_A} \mathbb{F}^m$  
  
Note $\phi_\beta, \phi_\gamma$ are isomorphisms.  
  
$\text{rank}(T) = \dim(R(T)) = \dim(T(V)) = \dim(\phi_\gamma(T(V)))$  
  
$= \dim(L_A(\phi_\beta(V)))$ (since diagram commutes)  
  
$= \dim(L_A(\mathbb{F}^n))$  
  
$= \text{rank}(L_A)$  
  
$= \text{rank}(A) = \text{rank}([T]_\beta^\gamma)$.  
  
Remark  
  
$\text{nullity}(T) = \text{nullity}(L_A)$ (by Dimension Theorem).  
  
$A \in M_{n \times n}(\mathbb{F})$.  
  
Then $A$ is invertible $\iff \text{rank}(A) = n$.  
  
### Thm 3.4  
  
$A \in M_{m \times n}(\mathbb{F})$.  
  
$P \in M_{m \times m}(\mathbb{F})$ invertible matrix.  
  
$Q \in M_{n \times n}(\mathbb{F})$ invertible matrix.  
  
Then:  
  
(a) $\text{rank}(AQ) = \text{rank}(A)$  
  
(b) $\text{rank}(PA) = \text{rank}(A)$  
  
(c) $\text{rank}(PAQ) = \text{rank}(A)$  
  
Proof)  
  
(a) $R(L_{AQ}) = R(L_A L_Q) = L_A(L_Q(\mathbb{F}^n))$.  
  
Since $Q$ is invertible, $L_Q$ is surjective ($L_Q(\mathbb{F}^n) = \mathbb{F}^n$).  
  
$= L_A(\mathbb{F}^n) = R(L_A)$.  
  
$\therefore \text{rank}(AQ) = \text{rank}(A)$.  
  
Corollary.  
  
Elementary row operations on a matrix are rank-preserving.  
  
$A \xrightarrow{\text{Elementary row op.}} EA$.  
  
$\text{rank}(EA) = \text{rank}(A)$ (since $E$ is invertible).  
  
### Thm 3.5  
  
The rank of a matrix $A \in M_{m \times n}(\mathbb{F})$  
  
= the dim. of the subspace spanned by its columns  
  
= the maximal number of its linearly independent columns.  
  
($\rightarrow$ 이거 증명하기)  
  
Proof)  
  
$\beta = \{e_1, ..., e_n\}$ standard ordered basis for $\mathbb{F}^n$.  
  
$R(L_A) = \text{Span}(L_A(\beta)) = \text{Span}(\{ L_A(e_1), ..., L_A(e_n) \})$.  
  
$L_A(e_j) = A e_j = j\text{-th column of } A$.  
  
$\therefore \text{rank}(A) = \dim(\text{Span}(\{\text{columns of } A\}))$.  
  
### Thm 3.6  
  
$A$ is $m \times n$ matrix of rank $r$.  
  
Then $r \le m, r \le n$.  
  
By means of a finite number of elementary row & column operations, A can be transformed into the matrix  
  
$D = \begin{pmatrix} I_r & O_1 \\ O_2 & O_3 \end{pmatrix}$  
  
where $O_1, O_2, O_3$ are zero matrices.  
  
Ex.  
  
$A = (\begin{matrix}1&2&1\\ 1&0&3\\ 1&1&2\end{matrix}) \sim (\begin{matrix}1&2&1\\ 0&-2&2\\ 0&-1&1\end{matrix}) \sim (\begin{matrix}1&0&0\\ 0&-2&2\\ 0&-1&1\end{matrix}) \sim (\begin{matrix}1&0&0\\ 0&1&-1\\ 0&-1&1\end{matrix}) \sim (\begin{matrix}1&0&0\\ 0&1&0\\ 0&0&0\end{matrix})$  
  
**Proof)** Induction on $\text{rank}(A) = r$.  
  
1. $\text{rank}(A) = 0 \Rightarrow A$ is the Zero matrix.  
      
2. $r = \text{rank}(A) \ne 0 \Rightarrow A_{ij} \ne 0$ for some $i, j$.  
      
    By means of at most three operations, $A \sim \begin{pmatrix} 1 & \cdots \\ \vdots & B \end{pmatrix}$.  
      
    Using row/col operations to clear the first row and column:  
      
    $A \sim \begin{pmatrix} 1 & 0 \\ 0 & C \end{pmatrix}$.  
      
    Rank of this matrix is $1 + \text{rank}(C)$. So $\text{rank}(C) = r - 1$.  
      
    By induction hypothesis, $C \sim D' = \begin{pmatrix} I_{r-1} & O \\ O & O \end{pmatrix}$.  
      
    So $A \sim \begin{pmatrix} 1 & 0 \\ 0 & D' \end{pmatrix} = \begin{pmatrix} I_r & O \\ O & O \end{pmatrix}$.  
      
  
Corollary 1.  
  
$A \in M_{m \times n}(\mathbb{F})$. A has rank $r$.  
  
There exist invertible matrices $B, C$ s.t. $BAC = \begin{pmatrix} I_r & O_1 \\ O_2 & O_3 \end{pmatrix}$.  
  
Proof)  
  
$D = E_p \cdots E_1 A G_1 \cdots G_q$.  
  
Let $B = E_p \cdots E_1$ (invertible).  
  
Let $C = G_1 \cdots G_q$ (invertible).  
  
Corollary 2.  
  
For $A \in M_{m \times n}(\mathbb{F})$,  
  
(a) $\text{rank}(A^t) = \text{rank}(A)$  
  
(b) ...  
  
(c) Spanned by rows...  
  
Proof of Coro 2  
  
$D = BAC$.  
  
$D^t = C^t A^t B^t$.  
  
Check $(AB)^t = B^t A^t$.  
  
$B, C$ invertible $\Rightarrow B^t, C^t$ invertible.  
  
$\text{rank}(D^t) = \text{rank}(C^t A^t B^t) = \text{rank}(A^t)$ (by Thm 3.4).  
  
Also $\text{rank}(D^t) = \text{rank}(D) = r = \text{rank}(A)$.  
  
Since $D = \begin{pmatrix} I_r & 0 \\ 0 & 0 \end{pmatrix}$, $D^t = \begin{pmatrix} I_r & 0 \\ 0 & 0 \end{pmatrix}$.  
  
$\therefore \text{rank}(A^t) = \text{rank}(A)$.  
  
Corollary 3.  
  
Every invertible matrix is a product of elementary matrices.  
  
Proof) $A$ invertible $n \times n$ matrix $\Rightarrow \text{rank}(A) = n$.  
  
$A \sim I_n$.  
  
$I_n = E_p \cdots E_1 A$.  
  
$A = E_1^{-1} \cdots E_p^{-1} I_n = E_1^{-1} \cdots E_p^{-1}$.  
  
These inverses are also elementary matrices.  
  
### Thm 3.7  
  
$V, W, Z$ finite-dimension.  
  
$T: V \rightarrow W$, $U: W \rightarrow Z$.  
  
$A, B$ matrices & $AB$ is defined.  
  
(a) $\text{rank}(UT) \le \text{rank}(U)$  
  
(b) $\text{rank}(UT) \le \text{rank}(T)$  
  
(c) $\text{rank}(AB) \le \text{rank}(A)$  
  
(d) $\text{rank}(AB) \le \text{rank}(B)$  
  
(직접해보기)  
  
Finding the Inverse Matrix  
  
$A$ invertible $n \times n$ matrix.  
  
Augmented matrix $(A | I_n)$.  
  
Ex) $A = (\begin{matrix} 0 & 1 \\ 1 & 1 \end{matrix})$. $(A | I_2) = (\begin{matrix} 0 & 1 & 1 & 0 \\ 1 & 1 & 0 & 1 \end{matrix})$.  
  
$A^{-1}(A | I_n) = (A^{-1}A | A^{-1}I_n) = (I_n | A^{-1})$.  
  
$A^{-1}$ is the product of elementary matrices, say $E_p \cdots E_1$.  
  
(... elementary operation을 하면 $A^{-1}$를 구할 수 있다.)  
  
Then $E_p \cdots E_1 (A | I_n) = (I_n | A^{-1})$.  
  
Apply row operations to $(A | I_n)$ to turn the left side into $I_n$. The right side becomes $A^{-1}$.  
  
Summary:  
  
By applying a finite number of elementary row operations,  
  
$(A | I_n) \sim (I_n | A^{-1})$.  
  
Note: $(A | I_n) \sim (I_n | B)$ for some $B \in M_{n \times n}(\mathbb{F})$.  
  
$E_p \cdots E_1 (A | I_n) = (I_n | B)$.  
  
Let $M = E_p \cdots E_1$.  
  
$M(A | I_n) = (MA | M) = (I_n | B)$.  
  
$\Rightarrow MA = I_n$ and $M = B$.  
  
Since $M$ is invertible & $MA = I_n$, $B = M = A^{-1}$.  
  
If $A$ is not invertible, then $\text{rank}(A) < n$.  
  
$\Rightarrow (A | I_n)$ cannot be row reduced to $(I_n | B)$.  
  
(Elementary row ops don't change rank!)  
  
Ex 1. $A = (\begin{matrix} 0 & 2 & 4 \\ 2 & 4 & 2 \\ 3 & 3 & 1 \end{matrix})$  
  
$(A | I_3) = (\begin{matrix} 0 & 2 & 4 & 1 & 0 & 0 \\ 2 & 4 & 2 & 0 & 1 & 0 \\ 3 & 3 & 1 & 0 & 0 & 1 \end{matrix})$  
  
$\sim (\begin{matrix} 2 & 4 & 2 & 0 & 1 & 0 \\ 0 & 2 & 4 & 1 & 0 & 0 \\ 3 & 3 & 1 & 0 & 0 & 1 \end{matrix})$  
  
$\sim (\begin{matrix} 1 & 2 & 1 & 0 & 1/2 & 0 \\ 0 & 2 & 4 & 1 & 0 & 0 \\ 0 & -3 & -2 & 0 & -3/2 & 1 \end{matrix})$  
  
... (Process continues to find inverse)  
  
Ex 2. $A = (\begin{matrix} 1 & 2 & 1 \\ 2 & 1 & -1 \\ 1 & 5 & 4 \end{matrix})$  
  
$\text{rank}(A) \ne 3$. $A$ is not invertible!  
  
Ex 3. $T: P_2(\mathbb{R}) \rightarrow P_2(\mathbb{R})$  
  
$f(x) \mapsto f(x) + f'(x) + f''(x)$  
  
Basis $\beta = \{1, x, x^2\}$.  
  
$[T]_\beta = \begin{pmatrix} 1 & 1 & 2 \\ 0 & 1 & 2 \\ 0 & 0 & 1 \end{pmatrix}$.  
  
Is $T$ invertible? Is $[T]_\beta$ invertible? Yes (Upper triangular with 1s on diagonal).  
  
$[T]_\beta^{-1} = \begin{pmatrix} 1 & -1 & 0 \\ 0 & 1 & -2 \\ 0 & 0 & 1 \end{pmatrix} = [T^{-1}]_\beta$.  
  
So, $[T^{-1}(a_0 + a_1 x + a_2 x^2)]_\beta = [T^{-1}]_\beta \begin{pmatrix} a_0 \\ a_1 \\ a_2 \end{pmatrix} = \begin{pmatrix} a_0 - a_1 \\ a_1 - 2a_2 \\ a_2 \end{pmatrix}$.  
  
$\therefore T^{-1}(a_0 + a_1 x + a_2 x^2) = (a_0 - a_1) + (a_1 - 2a_2)x + a_2 x^2$.  
  
Diagram:  
  
$P_2(\mathbb{R}) \xrightarrow{T} P_2(\mathbb{R})$  
  
$\phi_\beta \downarrow \quad \quad \uparrow \phi_\beta^{-1}$  
  
$\mathbb{R}^3 \xrightarrow{[T]_\beta} \mathbb{R}^3$  
  
### §3.3 System of linear equations  
  
(S)  
  
$a_{11}x_1 + \cdots + a_{1n}x_n = b_1$  
  
$\vdots$  
  
$a_{m1}x_1 + \cdots + a_{mn}x_n = b_m$  
  
$m$ linear equations, $n$ unknowns over $\mathbb{F}$.  
  
$A = (a_{ij})$: coefficient matrix.  
  
$x = (x_j)^t$, $b = (b_i)^t$.  
  
$Ax = b$  
  
A solution to the System (S) is $s = (s_1, \dots, s_n)^t \in \mathbb{F}^n$ s.t. $As = b$.  
  
Solution set: $K = \{ s \in \mathbb{F}^n : As = b \}$.  
  
System S is consistent if the solution set is non-empty. Otherwise, it is inconsistent.  
  
A system $Ax=b$ is homogeneous if $b = \vec{0}$. Otherwise non-homogeneous.  
  
### Thm 3.8  
  
The solution set $K_H = \{ s \in \mathbb{F}^n : As = \vec{0} \}$  
  
$= N(L_A)$  
  
Subspace of $\mathbb{F}^n$ of dimension $n - \text{rank}(L_A)$.  
  
### Thm 3.9  
  
Dim $= n - \text{rank}(A)$.  
  
$K$: the solution set of $Ax = b$.  
  
$K_H$: the solution set of $Ax = \vec{0}$ (homogeneous system corresponding to $Ax=b$).  
  
Then for any solution to $Ax=b$,  
  
(하나만 $s$ 찾고 $K_H$ 더해서 solution set을 찾을 수 있음)  
  
$K = \{s\} + K_H = \{ s + k : k \in K_H \}$  
  
Proof)  
  
($\subseteq$) If $w \in K$, then $Aw = b$. Also $As = b$.  
  
$\Rightarrow A(w-s) = Aw - As = b - b = \vec{0}$.  
  
$\therefore w-s \in K_H$.  
  
$\exists k \in K_H$ s.t. $w-s = k \Rightarrow w = s+k$.  
  
($\supseteq$) DIY.  
  
### Thm 3.10  
  
$Ax = b$: a system of $n$ linear eq. in $n$ unknowns.  
  
Then $A$ is invertible $\iff$ the system has exactly one solution.  
  
Proof)  
  
($\Rightarrow$) $A$ invertible $\Rightarrow A^{-1}$ exists.  
  
$Ax = b \Rightarrow x = A^{-1}b$ (unique solution).  
  
($\Leftarrow$) Suppose exactly one solution.  
  
$K_H = \{ \vec{0} \}$ (if there were non-zero $k \in K_H$, $s+k$ would be another solution).  
  
$\Rightarrow N(L_A) = \{ \vec{0} \} \Rightarrow L_A$ is injective.  
  
$L_A: \mathbb{F}^n \rightarrow \mathbb{F}^n$.  
  
$\therefore L_A$ is invertible $\Rightarrow A$ is invertible.  
  
### Thm 3.11  
  
The system is consistent $\iff \text{rank}(A) = \text{rank}(A|b)$.  
  
Proof) The system is consistent $\iff \exists s, As=b$  
  
$\iff b \in \text{Span}(\{a_1, a_2, ..., a_n\})$ ($\leftarrow$ span of column vectors)  
  
$\iff \text{Span}(\{a_1, ..., a_n\}) = \text{Span}(\{a_1, ..., a_n, b\})$  
  
(since $(a_1, ..., a_n) \begin{pmatrix} s_1 \\ \vdots \\ s_n \end{pmatrix} = b \Rightarrow b = s_1 a_1 + \dots + s_n a_n$)  
  
$\iff \text{rank}(A) = \text{rank}(A|b)$ (by Thm 3.5).  
  
Two systems of linear equations are "equivalent" if they have the same solution set.  
  
### Thm 3.13  
  
$Ax=b$: system of $m$ linear eq, $n$ unknowns.  
  
$C$: invertible $m \times m$ matrix.  
  
Then the system $(CA)x = Cb$ is equivalent to $Ax=b$.  
  
Proof)  
  
$K = \{ x \in \mathbb{F}^n : Ax=b \}$  
  
$K' = \{ x \in \mathbb{F}^n : (CA)x=Cb \}$  
  
Claim: $K = K'$.  
  
1. $K \subseteq K'$ (Clear: $Ax=b \Rightarrow C(Ax)=Cb \Rightarrow (CA)x=Cb$)  
      
2. $K' \subseteq K$:  
      
    If $w \in K'$, $(CA)w = Cb$.  
      
    Multiply by $C^{-1}$: $C^{-1}(CA)w = C^{-1}Cb \Rightarrow Aw = b$.  
      
    $\therefore w \in K$.  
      
  
Coro.  
  
$Ax=b$.  
  
If $(A|b) \sim (A'|b')$ by a finite number of elementary row operations,  
  
then $A'x=b'$ is equivalent to $Ax=b$.  
  
Proof)  
  
$E_p \cdots E_1 (A|b) = (A'|b')$.  
  
$E_p \cdots E_1$ is an invertible matrix $C$.  
  
So $(CA|Cb) = (A'|b')$.  
  
By Thm 3.13, equivalent.  
  
Ex:  
  
$3x_1 + 2x_2 + 3x_3 - 2x_4 = 1$  
  
$x_1 + x_2 + x_3 = 3$  
  
$x_1 + 2x_2 + x_3 - x_4 = 2$  
  
$(\begin{matrix}3&2&3&-2&1\\ 1&1&1&0&3\\ 1&2&1&-1&2\end{matrix}) \xrightarrow[\text{elementary row ops}]{\text{forward pass}} (\begin{matrix}1&2&1&-1&.\\ 0&1&.&.&.\\ 0&0&.&.&1\end{matrix}) \xrightarrow[\text{Gaussian Elimination}]{\text{backward pass}} (\begin{matrix}1&0&1&0&1\\ 0&1&0&0&2\\ 0&0&0&1&3\end{matrix})$  
  
(1 이외엔 Zero)  
  
(a) Any row containing a nonzero entry precedes any row in which all the entries are zero.  
  
(b) The first nonzero entry in each row is the only nonzero entry in its column.  
  
(c) The first nonzero entry in each row is 1, it occurs in a column to the right of the first nonzero entry in the preceding row.  
  
$\Rightarrow$ A matrix is in reduced row echelon form.  
  
### Thm 3.14  
  
Gaussian elimination transforms any matrix into its reduced row echelon form.  
  
$x_1 + x_3 = 1$  
  
$x_2 = 2$  
  
$x_4 = 3$  
  
Let $x_3 = t$.  
  
$\begin{pmatrix} x_1 \\ x_2 \\ x_3 \\ x_4 \end{pmatrix} = \begin{pmatrix} 1-t \\ 2 \\ t \\ 3 \end{pmatrix} = \begin{pmatrix} 1 \\ 2 \\ 0 \\ 3 \end{pmatrix} + t \begin{pmatrix} -1 \\ 0 \\ 1 \\ 0 \end{pmatrix}$.  
  
$\begin{pmatrix} -1 \\ 0 \\ 1 \\ 0 \end{pmatrix}$ is a basis for the corresponding homo. system ($Ax=0$).  
  
Ex: $(A|b) \sim \begin{pmatrix} 1&0&2&0&-2&3\\ 0&1&-1&0&1&-1\\ 0&0&0&1&-2&2\\ 0&0&0&0&0&0 \end{pmatrix}$  
  
$\Rightarrow x_1 + 2x_3 - 2x_5 = 3$  
  
$x_2 - x_3 + x_5 = -1$  
  
$x_4 - 2x_5 = 2$  
  
(Variables with pivots: $x_1, x_2, x_4$. Free variables: $x_3=t_1, x_5=t_2$)  
  
$\begin{pmatrix} x_1 \\ x_2 \\ x_3 \\ x_4 \\ x_5 \end{pmatrix} = \begin{pmatrix} -2t_1 + 2t_2 + 3 \\ t_1 - t_2 - 1 \\ t_1 \\ 2t_2 + 2 \\ t_2 \end{pmatrix} = \begin{pmatrix} 3 \\ -1 \\ 0 \\ 2 \\ 0 \end{pmatrix} + t_1 \begin{pmatrix} -2 \\ 1 \\ 1 \\ 0 \\ 0 \end{pmatrix} + t_2 \begin{pmatrix} 2 \\ -1 \\ 0 \\ 2 \\ 1 \end{pmatrix}$.  
  
Note: $\{ \begin{pmatrix} -2 \\ 1 \\ 1 \\ 0 \\ 0 \end{pmatrix}, \begin{pmatrix} 2 \\ -1 \\ 0 \\ 2 \\ 1 \end{pmatrix} \}$ is a basis for the solution set of homogeneous system.1  
  
$\begin{pmatrix} 3 \\ -1 \\ 0 \\ 2 \\ 0 \end{pmatrix} \leftarrow$ particular solution.2  
  
**Note:** Solutions exist $\iff$ In the reduced row echelon form we do not obtain the following $\rightarrow (\begin{matrix} * & * \\ 0 \cdots 0 & 1 \end{matrix})$.  
  
### Thm 3.15  
  
$Ax=b$, $r$: nonzero equations in $n$ unknowns.  
  
$\text{rank}(A) = \text{rank}(A|b)$ (has solution, consistent!)  
  
& $(A|b)$ is in reduced row echelon form.  
  
It expresses an arbitrary solution $s$ of $Ax=b$ in terms of $n-r$ parameters.  
  
$s = s_0 + t_1 u_1 + \cdots + t_{n-r} u_{n-r}$.  
  
(a) $\text{rank}(A) = r$.  
  
(b) If the general solution is of the form $s = s_0 + t_1 u_1 + \cdots + t_{n-r} u_{n-r}$, then $\{u_1, ..., u_{n-r}\}$ is a basis for the system $Ax=0$ and $s_0$ is a solution to the original system.  
  
Proof)  
  
$s_0 \in K = \{ x | Ax=b \}$  
  
$K_H = \{ x | Ax=0 \}$  
  
We know $K = \{s_0\} + K_H$.  
  
$\therefore K_H = K - \{s_0\} = t_1 u_1 + \cdots + t_{n-r} u_{n-r} = \text{Span}(\{u_1, \dots, u_{n-r}\})$.  
  
Because $\dim(K_H) = \dim N(L_A) = n - \dim(R(L_A)) = n - r$.  
  
(Basis size must be $n-r$).  
  
$(\begin{matrix} 2 & 3 & 1 \\ 1 & 1 & 1 \\ 1 & 1 & 1 \end{matrix}) \begin{matrix} 4 & -9 & 17 \\ 1 & -3 & 6 \\ 2 & -5 & 8 \end{matrix}$  
  
$\downarrow$  
  
$(\begin{matrix} 1 & 0 & 2 & 0 & -2 & 3 \\ 0 & 1 & -1 & 0 & -1 & 2 \\ 0 & 0 & 0 & 1 & -2 & 2 \\ 0 & 0 & 0 & 0 & 0 & 0 \end{matrix})$  
  
(쉽게 l-dep 여부와 rank 판별가능)  
  
$A$: $m \times n$ matrix with columns $a_1, ..., a_n$. $A = (a_1 \cdots a_n)$.  
  
$B$: reduced row echelon form of $A$. $B = (b_1 \cdots b_n)$.  
  
$\text{rank}(A) = r = \text{rank}(B)$.  
  
$B = (\begin{matrix} 1 & * & 0 & * & 0 \\ 0 & \cdots & 1 & \cdots & 0 \\ \vdots & & \vdots & & 1 \\ 0 & \cdots & 0 & \cdots & 0 \end{matrix}) \} \to \text{rank}$.  
  
Columns: $b_1, b_2, b_3, \dots$.  
  
So $e_1, ..., e_r$ must occur among the columns of $B$.  
  
Let $b_{j_k} = e_k$.  
  
Then $a_{j_1}, ..., a_{j_r}$ are linearly independent.  
  
($\hookrightarrow$ corresponding columns of A).  
  
Why? $B = MA$ where $M$ is invertible ($E_p \cdots E_1$).  
  
Then $M a_{j_1}, ..., M a_{j_r}$  
  
$\downarrow \quad \quad \quad \quad \downarrow$  
  
$e_1 \quad \dots \quad e_r$ (l-indep).  
  
Apply $M^{-1} \rightarrow a_{j_1}, ..., a_{j_r}$ l-indep.  
  
A column of $B$ has the form $\begin{pmatrix} d_1 \\ \vdots \\ d_r \\ 0 \\ \vdots \end{pmatrix} = d_1 e_1 + \cdots + d_r e_r$.  
  
Apply $M^{-1} \rightarrow$ $M^{-1} \begin{pmatrix} \vdots \end{pmatrix} = d_1 a_{j_1} + \cdots + d_r a_{j_r}$.  
  
LHS is corresponding column of A.  
  
**Corollary.** Reduced row echelon form of a matrix is **unique**.  
  
$A = \begin{pmatrix} * & \dots \\ * & \\ \vdots & \\ * & \end{pmatrix}$  
  
nonzero? zeros?  
  
2번째 column이...  
  
$\rightarrow$ l-indep $B = \begin{pmatrix} 1 & 0 \\ 0 & 1 \\ 0 & 0 \end{pmatrix}$  
  
$\rightarrow$ l-dep $B = \begin{pmatrix} 1 & 2 \\ 0 & 0 \\ 0 & 0 \end{pmatrix}$  
  
(A의 첫 column들로 B 결정가능)  
  
즉, column끼리 l-indep이면 B도 l-indep이다.  
  
A에 따라 B가 결정되고, 이 idea로 증명하자.  
  
Proof)  
  
$A \in M_{m \times n}(\mathbb{F})$.  
  
$\rightarrow$ Induction on $n$.  
  
i) $n=1$. $A = \begin{pmatrix} A_{11} \\ \vdots \\ A_{m1} \end{pmatrix}$. $B = \begin{pmatrix} 0 \\ \vdots \\ 0 \end{pmatrix}$ or $\begin{pmatrix} 1 \\ 0 \\ \vdots \\ 0 \end{pmatrix}$.  
  
ii) $n > 1$. column vector.  
  
$A = (a_1 \ a_2 \ \dots \ a_{n-1} \ a_n)$  
  
$B = (b_1 \ b_2 \ \dots \ b_{n-1} \ b_n)$  
  
$A' = (a_1 \ \dots \ a_{n-1})$  
  
$B' = (b_1 \ \dots \ b_{n-1})$ ($B'$ is reduced row echelon form of $A'$).  
  
$B'$ is determined by $A'$. Unique by induction hyp.  
  
$\Rightarrow$ Show $b_n$ is determined by $A_n$.  
  
$A = (A' | a_n)$  
  
$B = (B' | b_n)$  
  
$\{ x \in \mathbb{F}^n : A'x = a_n \} = \{ x \in \mathbb{F}^n : B'x = b_n \}$  
  
($B=MA$, $M$ invertible, solution sets must be same).  
  
1. $A'x = a_n$ is inconsistent.  
      
    $B'x = b_n$ is inconsistent.  
      
    ex) $b_n = \begin{pmatrix} 0 \\ \vdots \\ 1 \\ \vdots \end{pmatrix}$. $\therefore B' = \begin{pmatrix} 1 & * & 0 & * \\ 0 & \dots & 0 & 0 \\ & & \end{pmatrix} \begin{pmatrix} * \\ * \\ 1 \\ 0 \end{pmatrix}$  
      
    ($r'+1$) entry, where $r'$ is the rank of $A'$.  
      
2. $\exists x_0 \in \mathbb{F}^n$ s.t. $A' x_0 = a_n$  
      
    $\Rightarrow B' x_0 = b_n$.  
      
    $b_n$ is determined by $A$ and $B'$.  
      
  
Ex:  
  
$S = \{ 2+x+2x^2+3x^3, 4+2x+4x^2+6x^3, 6+3x+8x^2+7x^3, 2x+5x^3, 4+x+9x^3 \}$  
  
generates a subspace $V$ of $P_3(\mathbb{R})$.  
  
Find a subset of $S$ that is a basis for $V$.  
  
Proof)  
  
$\beta: \{1, x, x^2, x^3\}$, $P_3(\mathbb{R}) \rightarrow \mathbb{R}^4$, $f(x) \mapsto [f(x)]_\beta$.  
  
$A = \begin{pmatrix} 2 & 4 & 6 & 0 & 4 \\ 1 & 2 & 3 & 2 & 1 \\ 2 & 4 & 8 & 0 & 0 \\ 3 & 6 & 7 & 5 & 9 \end{pmatrix} \sim B = \begin{pmatrix} 1 & 2 & 0 & 4 & 0 \\ 0 & 0 & 1 & -1 & 0 \\ 0 & 0 & 0 & 0 & 1 \\ 0 & 0 & 0 & 0 & 0 \end{pmatrix}$  
  
(Pivots at col 1, 3, 5 $\rightarrow$ l-indep).  
  
$V \rightarrow \phi_\beta(V)$.  
  
$\{a_1, a_3, a_5\}$ is a basis for $\phi_\beta(V)$.  
  
$\phi_\beta^{-1}\{a_1, a_3, a_5\}$ is a basis for $V$.  
  
$= \{f_1, f_3, f_5\}$.  
  
Ex:  
  
$V = \{ (x_1, ..., x_5) \in \mathbb{F}^5 : x_1 + 7x_2 + 5x_3 - 4x_4 + 2x_5 = 0 \}$  
  
$S = \{ (-2, 0, 0, -1, -1), (1, 1, -2, -1, -1), (-5, 1, 0, 1, 1) \}$  
  
is linearly indep subset of $V$.  
  
Extend $S$ to a basis for $V$. (근데 어떻게 extend 하지?)  
  
$\begin{pmatrix} x_1 \\ x_2 \\ \vdots \\ x_5 \end{pmatrix} = \begin{pmatrix} -7t_1 - 5t_2 + 4t_3 - 2t_4 \\ t_1 \\ t_2 \\ t_3 \\ t_4 \end{pmatrix} = t_1 \begin{pmatrix} -7 \\ 1 \\ 0 \\ 0 \\ 0 \end{pmatrix} + t_2 \begin{pmatrix} -5 \\ 0 \\ 1 \\ 0 \\ 0 \end{pmatrix} + t_3 \begin{pmatrix} 4 \\ 0 \\ 0 \\ 1 \\ 0 \end{pmatrix} + t_4 \begin{pmatrix} -2 \\ 0 \\ 0 \\ 0 \\ 1 \end{pmatrix}$  
  
Basis for $V$.  
  
$A = \begin{pmatrix} -2 & 1 & -5 & -7 & -5 & 4 & -2 \\ 0 & 1 & 1 & 1 & 0 & 0 & 0 \\ 0 & -2 & 0 & 0 & 1 & 0 & 0 \\ -1 & -1 & 1 & 0 & 0 & 1 & 0 \\ -1 & -1 & 1 & 0 & 0 & 0 & 1 \end{pmatrix} \sim B \begin{pmatrix} 1 & 0 & 0 & 1 & 1 & 0 & -1 \\ 0 & 1 & 0 & -\frac{1}{2} & 0 & 0 & 0 \\ 0 & 0 & 1 & -\frac{1}{2} & 0 & 0 & 0 \\ 0 & 0 & 0 & 0 & 1 & -1 \\ 0 & 0 & 0 & 0 & 0 & 0 & 0 \end{pmatrix}$  
  
$\rightarrow \{a_1, a_2, a_3, a_5\}$ is a basis for $V$.
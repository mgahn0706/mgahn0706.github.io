---  
tags:  
  - vector-space  
share: "true"  
github_title: 2024-06-09-vector-spaces  
title: 1-1. Vector Spaces  
date: 2024-06-09  
categories:  
  - Lecture Notes  
  - Linear Algebra  
math: "true"  
---  
## Vector Spaces  
  
**정의**.  
$V$  : a **vector space** over $\mathbb{F}$ where  
- addition + : $V$ x $V \to V$  $(x, y) \mapsto x+y$  
- 상수배: $\mathbb{F} \times V \to V, f(a, v) := av$  
---  
It satisfies  
	$\forall \; x, y, z \in V, \forall \; a, b, c, \in \mathbb{F}$  
1.  $x + y = y + x$ (교환법칙)  
2.  $(x+y)+z = x+(y+z)$ (결합법칙)  
3. $\exists 0 \in V \text{ such that } x + 0 = x$ (항등원)  
4. $\forall x\in V \;  \exists y \in V  \text{ such that } x+y=0$  (역원)  
for vector addition, and  
5. $1x = x$  
6. $(ab)x = a(bx)$ (상수끼리의 곱과 벡터의 상수배가 서로 영향을 주지 않는다.)  
7. $a(x+y) = ax + by$ (상수곱과 덧셈이 서로 영향을 주지 않는다.)  
8. $(a+b)x = ax + bx$  
for scalar multiplication  
  
Vector space임을 보이려면 위의 8가지 조건이 hold하는지 아닌지를 판단해야합니다.  
왜 프리드버그 책에서 위의 8개의 조건을 모두 증명에 넣지 않고 덧셈과 스칼라배만 vector space 내에서 정의되는지만 확인하는 이유는  
[여기](https://math.stackexchange.com/a/3364305) 의 답변이 도움이 되었습니다.  
  
Vector space는 vector만이 아닌, field, addition, scalar multiplication의 quadraple이며 vecotr space를 다룰 때 항상 같이 논의되어야합니다.  
  
---  
  
> Thm. 1.1 (Cancellation Law)  
> ${x+y=y+z}$    ( ${x, y, z, \in V}$)  
> ${\to x = y }$  
  
proof idea) ${z}$에 더해서 항등원(0)이 되는 벡터 ${v}$를 잡고, 결합법칙을 이용하면 된다.  
  
> Coro. 1   
> ${ \mathbf{0}}$ is unique.  
  
proof idea) 영벡터의 성질을 만족하는 두 영벡터를 가정하고, 두 영벡터가 위의 정리에 의해 같음을 보인다.  
  
> Coro. 2  
> ${\forall \; x \in V}$, ${ !\exists y \in V  \text{ such that } x+y=0 }$  
  
---  
  
> Thm. 1.2   
> ${V}$ , a vector space over ${\mathbb{R}}$ (or, ${\mathbb{C}}$)  
>   
> (a) ${0x=\mathbf{0}}$  
> (b) (-a)${x}$ = -(${ax}$)=a(${-x}$)   
> (c) ${a\mathbf{0}=\mathbf{0}}$  
  
proof)  
(a) ${0x + 0x = (0+0)x = 0x + \mathbf{0}}$  
(b) ${ax+(-a)x = (a+(-a))x = 0x = \mathbf{0}}$  
(c) ${a \mathbf{0} + a \mathbf{0} = a(\mathbf{0}+\mathbf{0}) = a\mathbf{0} + \mathbf{0}}$ (similar with (a))  
  

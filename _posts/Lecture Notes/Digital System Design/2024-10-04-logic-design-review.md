---  
tags:  
  - digital-logic  
share: "true"  
github_title: 2024-10-04-logic-design-review  
title: Logic Design Review  
date: 2024-10-04  
categories:  
  - Lecture Notes  
  - Digital System Design  
---  
# Digital Circuits  
  
input을 주면 functional spec과 timing spec(delay등)에 따라 output을 내는 network  
  
node = 각 element를 잇는 곳, 또는 input, output anode  
  
### Types of Digital Circuits  
  
1. Combinational Circuits  
      
    현재 값의 조합으로만 output을 낸다.  
      
    memoryless  
      
2. Sequential Circuits  
      
    input sequence에 따라 값이 달라진다. 즉, 이전 값과 현재 값이 모두 영향을 준다.  
      
    Memory가 있다.  
      
  
---  
  
### Boolean equation  
  
### Minterm & Maxterm  
  
(1) Minterm  
  
모든 input variable을 포함한 product (literal이 한번씩만 모두 나타난다)  
  
ex) ABC  
  
(2) Maxterm  
  
모든 input variable을 포함한 sum (위와 동일)  
  
ex) A+B+C  
  
### Canonical Form  
  
A truth table with N inputs contains 2^n rows  
  
SoP - Sum of Product ⇒ minterm들로 나타내면 canonical  
  
Pos - Product of Sum ⇒ maxterm ‘’  
  
SoP, PoS 형식으로 쓰여졌어도 canonical하지 않을 수 있으며 이는 아직 optimized되지 않았다는 의미이다. power를 더 먹는다!  
  
### 왜 Minterm / Maxterm 인가  
  
(1) Sum of Minterm  
  
ex) AB + AB  
  
하나의 term만 true여도 전체 식이 true가 된다. (OR has minimum satisfiability)  
  
→ SoP를 true로 만들기 위한 최소힌의 조건  
  
(2) Product of Maxterm  
  
ex) (A+B)(A+B)  
  
모든 term이 true여야만 전체 식이 true가 된다. (AND ahs maximum satisfiability)  
  
→ PoS를 true로 만들기 위한 최대 조건  
  
---  
  
## Boolean Algebra  
  
결국 우리는 가장 간단한 식을 찾기 위해 boolean algebra를 써야함  
  
### Duality  
  
axioms and theorems → duality의 원칙을 따름  
  
0 ↔ 1 AND ↔ OR 를 모두 바꾸면 정리가 성립함.  
  
|T1|B&1=B|Identity|  
|---|---|---|  
|T2|B&0=0|Null Element|  
|T3|B^B=B|Idempotency|  
|T4|!(!B))=B|Involution|  
|T5|B^~B = 0|Complements|  
|T6|B&C = C&B|Communiativity|  
|T7|(B&C)&D = B&(C&D)|Associativity|  
|T8|(B&C)|(B&D) = B& (C|  
|T9|B&(B|C) = B|  
|T10|(B&C)|(B&!C) = B|  
|T11|(B&C)|(~B&D)|  
|T12|!(A&B&C&D&…) = (~A|…)|  
  
→ Simple booldean equation을 만들자!  
  
Prime Implicant : 다른 implicant들과 묶여서 더이상 literal이 줄어들지 않는 경우이다.  
  
Essential Prime Implicant: 필수적인 prime implicant. 반드시 포함되어야하는 implicant이다.  
  
[[Karnaugh Map] Essential Prime Implicants](https://blastic.tistory.com/195)  
  
여기 참고.  
  
어떤 케이스들은 하나의 implicant에만 포함되어있다. 이 경우 해당 implicant를 essential prime implicant라고 한다.  
  
그런데 Boolean Algebra로만 어떻게 최소인지 알텐가. 너무 어렵지 않은가?  
  
K-map을 그리자.  
  
---  
  
## K-Map  
  
- Gray coding으로 각 row와 column을 쓴다  
- 2의 제곱이 되는 직사각형을 만든다. → each rect is implicant!  
  
---  
  
## Combinational Building Blocks  
  
### Decoder  
  
N inputs and 2^N outputs  
  
input의 값으로 어떤 output을 내보낼지 결정할 수 있다.  
  
→ 적절히 output의 값을 설정한다면 모든 logic gate를 만들 수 있다! AND, OR, XNOR 등…  
  
---  
  
## X’s and Z’s  
  
(1) X: illegal value  
  
- Unknown or Illegal value.  
- 1과 0을 동시에 assign한 경우.  
- initialize가 안된 경우도 해당.  
  
(2) Z: Floating value  
  
- 0도 1도 아닌 상태.  
- floating, or High impedence  
- 회로가 끊김  
  
---  
  
# Sequential Circuit  
  
메모리가 존재하는 circuit.  
  
## Building Block of Memory  
  
→ Bistable element!  
  
![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/bdc23bea-49ed-413d-9b14-ccfb1b348d92/b113182c-8154-48c1-9161-3891ce495822/image.png)  
  
이렇게 하면 Q, ~Q 상태 2개가 있지 않은가?  
  
심지어 stable하다. 이것이 기본적인 메모리가 될 것이다.  
  
→ N stable한 상태가 있다면, log_2N bits의 information을 처리할 수 있을 것!  
  
ex) 여기서는 2개의 stable한 상태라 1 bit의 정보를 저장할 수 있음.  
  
## Latches and Flip-flops  
  
근데 위의 element는 상태를 못바꾸잖아? 안될거야 아마.  
  
Latch와 Flip-flop은 상태를 바꿀 수 있는 bi-state element이다.  
  
### Latches  
  
- storage elements that operate with signal levels  
    - 0, 1의 여부로 상태가 변한다.  
  
### Flip-flops  
  
- clock transition에 따라 상태를 변화시킨다.  
    - 즉, posedge, negedge 등 edge triggered된다.  
  
---  
  
## SR Latch (Set-Reset)  
  
NOR gate 2개를 서로 연결한 모습.  
  
(inverter는 input이 없어? 그럼 input 2개짜리 만들면되지)  
  
이때의 truth table을 보자.  
  
set이 1이면 P도 1.  
  
reset이 1이면 P도 0.  
  
둘다 0이면 기존 값을 유지한다.  
  
→ 근데 둘 다 1이면???  
  
Q와 ~Q가 둘다 0이된다. 가능은 하지만, 이건 의도된 값이 아니다.  
  
→ 그럼, `state가 무엇인지` 와, `언제 state를 바꿀지` 를 나누자!  
  
---  
  
## D Latch  
  
오른쪽은 SR Latch와 같고, E에 따라서 데이터가 들어갈지 안들어갈지가 정해진다.  
  
E (교재에서는 CLK)이 0이면, 둘다 값을 유지하고(Latch처럼 행동),  
  
CLK이 1일때만 D의 값이 투명해지면서 값이 설정되는 것을 볼 수 있다.  
  
위에서 우려했던 1, 1이 오는 경우는 이제 없어졌다!  
  
즉, CLK이 1이면 transparent해지고, CLK이 0이면 opaque해진다.  
  
<aside> 📖  
  
이정도면 괜찮은 거 같은데, Flip-flop을 만든 이유가 무엇일까? →  
  
[What are the advantages and differences between a D-Latch and a D Flip-Flop?](https://www.quora.com/What-are-the-advantages-and-differences-between-a-D-Latch-and-a-D-Flip-Flop)  
  
</aside>  
  
---  
  
## D Flip Flop  
  
2개의 D latch를 붙이고, 서로 다른 CLK input을 준다.  
  
  
- CLK이 0이 될때, D의 값이 N1 node로 이동.  
- CLK이 1이 될 때 비로소, Q로 D가 이동함.  
  
→ edge triggered!  
  
위의 그림은 posedge.  
  
negedge로 바꾸려면 inverter 하나 제거. (또는 방향 바꾸기)  
  
---  
  
### Trade-off of Latch and Flip-Flop  
  
(1) Latch  
  
- power 소모가 적음  
- 빠름. 성능이 좋음.  
- 간단함.  
  
(2) Flip-flop  
  
- edge triggered되기 때문에 input 변화로 data가 오염될 일이 적음.  
- control하기가 쉽다.  
  
---  
  
### Registers  
  
N개의 D Flip flop을 쭉 연결해서 각 비트별로 연결하면, register!  
  
CLK의 posedge마다 인풋의 값을 저장.  
  
---  
  
## Synchoronous / Asynchoronous  
  
(1) Synchornous  
  
Clock이 특정 edge일 때만 상태가 변함.  
  
→ Clock에 synchornous된 상태임.  
  
- finite state machine이 이에 속함.  
  
(2) Asynchornous  
  
CLK에 상관없이 값을 바로바로 계산해줘야하는 경우가 있음.  
  
ex) ring oscillator  
  
<aside> 📖  
  
Clock 신호를 이걸로 만드나?  
  
→ oscillator가 맞긴 한데, 이런식으로는 안만들고 저항과 축전기를 이용해서 만든다.  
  
[What Are Clock Signals in Digital Circuits, and How Are They Produced?](https://www.symmetryelectronics.com/blog/what-are-clock-signals-in-digital-circuits-and-how-are-they-produced-symmetry-blog/)  
  
</aside>  
  
---  
  
## Finite State Machine  
  
k개의 register로 2^k개의 상태를 만들어 상태를 제어하는 것.  
  
(1) Moore Machine  
  
현재 상태만이 output에 영향을 줌.  
  
ex) 신호등 처리에서는 현재 S0, S1인지에 따라 output이 정의되었음.  
  
- 직관적  
  
(2) Mealy Machine  
  
현재 상태와 input이 같이 output에 영향을 줌.  
  
- 상태의 개수가 적음  
  
→ output logic에 input이 쓰이느냐 안쓰이느냐의 차이.  
  
[디지털 논리회로 / Moore FSM과 Mealy FSM의 장단점](https://se-jung-h.tistory.com/entry/%EB%94%94%EC%A7%80%ED%84%B8-%EB%85%BC%EB%A6%AC%ED%9A%8C%EB%A1%9C-Moore-FSM%EA%B3%BC-Mealy-FSM%EC%9D%98-%EC%9E%A5%EB%8B%A8%EC%A0%90)  
  
<aside> 📖  
  
TODO: lab 4의 상태 설계를 Mealy machine으로 해보시오.  
  
</aside>  
  
<aside> 📖  
  
TODO: Digital Design and Computer Architecture 교재를 다운하고 1, 2, 3챕터를 읽어보시오. 애매한 부분은 위의 노션에 추가하시오.  
  
</aside>
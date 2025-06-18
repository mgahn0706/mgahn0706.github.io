---  
tags:  
  - verilog  
  - structural  
share: "true"  
github_title: 2024-10-21-structural-modeling  
title: 6. Structural Modeling  
date: 2024-10-21  
categories:  
  - Lecture Notes  
  - Digital System Design  
---  
모듈을 간단한 primitive module로 나타내고, 그것의 연결을 바탕으로 모듈을 기술하자.  
  
## Gate primitives  
  
- and, or, xor  
- buf, not  
- bufif / notif gates  
    - three state (0,1,z) 게이트이다.  
    - signal이 1이면 게이트가 끊겨서 z가 됨 (active low)  
    - buffer if 1, not if 0 등으로 이해하면 좋다.  
  
---  
  
### Gates  
  
and, or는 c에서 체크하는거와 동일하게 감.  
  
- 하나가 0이면 무조건 and 0, 1이면 무조건 or는 1.  
  
---  
  
### Tri-state buffer  
  
```verilog  
module two_to_one_mux_tristate(input x, input y, input s, output f);  
tri f; // tri-state 임을 지정  
  
	bufif0(f, x, s);  
	bufif1(f, y, s);  
	  
endmodule  
```  
  
---  
  
## Array of instance  
  
```verilog  
wire [3:0] a, b, c;  
nand nand1 [3:0] (out, a, b, c);  
```  
  
이것은 vector가 아니라 단순 bitwise로 계산하는 것이다.  
  
---  
  
### 9-bit parity generator  
  
even parity = 1의 개수가 짝수가 되도록 만들어주는 parity  
  
odd parity = 1의 개수가 홀수가 되도록 만들어주는 parity  
  
ep = x[0] ^ x[1] ^ … ^ x[8]; 즉 ep = ^x;  
  
→ 이 경우에는 right to left로 serial하게 진행되기 때문에 시간이 오래걸린다.  
  
---  
  
## Net types  
  
### wire and tri  
  
multiple driver인 경우에는 0, 1일 때 x  
  
z, 0일 때 0임을 잘 확인하면 좋다.  
  
z, 1은 1이다.  
  
### Wired nets  
  
gate 수 줄이기 위한 것.  
  
  
  
위와 같이 하여 (b)에서 필요한 8개의 CMOS를…  
  
  
  
이렇게 하면 nmos 4개로 줄일 수 있다. 근데 이러면 delay와 에너지 소비는 늘지 않나? 몰루.  
  
요즘은 gate 크기가 워낙 작아서 wire 최적화하는게 더 중요하다.  
  
---  
  
```verilog  
module open_drain(input w, x, y, z, output f);  
  
wand f;  
  
nand n1(f, w, x);  
nand n2(f, y, z);  
endmodule  
```  
  
이렇게 wand, wor를 쓰면 어떤 지점에서 wire처럼 작동하지만, 값을 넣어줄 때 and, or의 동작을 따른다는 의미이다. 즉, 0과 1이 온 지점에는 tri, wire는 x가 오지만 wand는 0, wor는 1이 온다.  
  
tri1, tri0이라는 것도 있다. 이것도 wired net에서 쓰는데,  
  
기본값을 지정해주는 것이라고 보면 된다.  
  
tri1 ⇒ 기본적으로 아무것도 drive가 안되면 이 값은 1이다. 즉, z와 z가 연결된 경우에만 1이된다.  
  
tri0 ⇒ 위와 같지만, z , z일 때 tri처럼 z가 아니라 0으로 된다.  
  
---  
  
## Delays  
  
### Inertial delay  
  
소자 내의 RC delay로 인해 해당 delay보다 짧은 신호는 output으로 propagate되지 않음.  
  
```verilog  
wire a;  
and #4 (b, x, y); // inertial delay 4ns  
```  
  
### Transport delay  
  
모든 signal event가 output으로 전달됨.  
  
```verilog  
wire #5 a;  
and #4 (a, x, y);  
```  
  
위의 경우에서 a의 신호는 inertial 4초 + transport 5초 = 9초부터 적용되기 시작한다.  
  
### Delay Speicifcation  
  
(1) rise delay: 1 from 0, x, z  
  
(2) fall delay : 0 from 1, x, z  
  
(3) turn-off delay: z from 0, 1, x  
  
- gate delay only : and1 #3 and(a, x, y); → 모든 delay에 3이 적용  
- rise and fall: and1 #(10: 15) → rising 10, falling 15, turn-off = min(10, 15) = 10  
- rise and fall and turn-off: and1 #(10:12:15) and(a, x, y) → rising 10, falling 12, turn off 15  
  
[Verilog Gate Delay](https://www.chipverify.com/verilog/verilog-gate-delay)  
  
---  
  
## Hazard  
  
output을 결정하는 2개 이상의 path가 다른 delay를 가진다면 값이 stable되기 전에 튈 수 있음  
  
- Glitch: unwanted short pulse  
- transient time: 해당 glitch의 지속시간  
  
static hazard와 dynamic hazard로 나뉜다.  
  
### Static hazard  
  
원래는 0이나 1로 지속되어야하는데, 잠깐동안 튀는 경우.  
  
즉, 1 - 0 - 1 (static - 1 - hazard)  
  
  
→ K-map에서 인접한 1들이 하나의 term으로 묶이지 않은경우 hazard가 발생함.  
  
P와 Q가 (1,1)인 상태에서 R이 바뀌면 다른 term으로 바로 넘어갈 때, or이 01에서 10으로 바뀌며 값이 유지되어야하는데, 하나가 늦게오면 값이 유지되지 않을 수 있음.  
  
그렇다면, 11일 때는 무조건 켜주게 하면 (즉, 인접한 1을 새로운 term으로 묶어주면)  
  
static hazard를 방지할 수 있다.  
  
### Dynamic Hazard  
  
output이 3번 이상 바뀌는 경우.  
  
즉, output을 결정하는 path가 3개 이상인 경우.  
  
<aside> 📖  
  
이거 signal ppt걸로 한번 연습해보자.  
  
</aside>
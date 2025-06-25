---  
tags:  
  - cpu  
  - architecture  
  - digital-logic  
share: "true"  
github_title: 2025-03-07-introduction  
title: 1. Introduction  
date: 2025-03-07  
categories:  
  - Lecture Notes  
  - Computer Architecture  
---  
## What makes a computer a computer?  
  
**폰 노이만 구조** : 메모리에 `데이터`와 `프로그램`이 동시에 저장되어 있는 구조. (ex. 덧셈과 1이 같이 들어있음)  
  
<aside> 💡  
  
Is GPU non-von newmann architecture?  
  
No! GPU는 동일하게 여러 번 반복되는 연산(프로그램)에 대해 메모리에서 한 번만 꺼내와서 여러 개의 값들에 연산을 수행한다. 따라서 폰 노이만 구조의 정의에 따라서 GPU도 폰 노이만 구조를 따른다. 단, bus의 크기가 무지막지하게 커지지 않아서 폰 노이만 아키텍쳐의 ( )한 한계점을 보완할 수 있다.  
  
</aside>  
  
  
  
---  
  
## Logic gates  
  
모든 디지털 회로는 여러 개의 스위치로 이루어져 있다. Gate에 1을 주면 전류가 흐르고 0을 주면 안흐르는, 이정도의 추상화 레벨에서 배웠을 것이다.  
  
아래에서는 여러가지 gate의 트랜지스터 구조를 다룬다. ~~논설실에서도 보고 디시설에서도 보고 시프에서도 보고 컴조에서도 보고 본거 또보고 또보고 또보고~~  
  
### Inverters  
  
PMOS와 NMOS를 직렬로 연결시키면 not gate 완성  
  
### NAND Gates  
  
Vdd 쪽은 적어도 하나만 0이어도 들어옴에 반해, GND의 값이 나가는 경우는 둘 다 1일 때이다.  
  
### NOR Gates  
  
NAND와 반대이다.  
  
### Memory  
  
Inverter 2개를 연결하면, Bi-stable한 상태가 되는데, 이를 이용해 메모리를 만들 수 있다.  
  
강한 신호를 주면 값이 바뀌는데, 이를 이용해 레지스터와 메모리를 만든다.  
  
## Transistor-level implementation  
  
### NMOS transistor  
  
gate에 특정 수준 이상의 전압을 걸어주면, p로 도핑되어있는 반도체 위쪽에 (+)전하가 모인다. 이로 인해 전위 차가 줄어들게 되고, source → drain으로 전류가 흐르게 된다.  
  
### I-V characteristics  
  
three modes  
  
(1) Cutoff  
  
Threshold voltage보다 낮은 전압이 걸리면,, 전류가 흐르지 않는다.  
  
(2) Linear  
  
drain과 source 사이에 걸린 전압이 현재 gate에 걸린 전압 - threshold 값보다 충분히 작으면 linear하다. (옴의 법칙)  
  
(3) Saturation  
  
drain과 source 사이에 걸린 전압이 너무 크면, saturated되어 전압이 높아져도 전류가 유지된다.  
  
### CMOS Layout for NAND gate  
  
위 그림과 같이 위쪽은 PMOS(동그라미가 있는, n에 p형 반도체를 넣은 것. (0)를 주어야 전류가 흐름)가 병렬로 연결되어있고, 아래 NMOS들은 직렬 연결되어있다.  
  
짧게 연결된건 B(Body terminal)인데,  
  
- **NMOS의 경우:** 보통 바디는 GND에 연결되어, 바디 효과를 최소화하고 임계 전압을 안정적으로 유지합니다.  
  
형성된 채널로 인해 IV 특성이 왜곡되는걸 막아준다.  
  
- **PMOS의 경우:** 바디는 일반적으로 VDD에 연결되어 같은 목적을 달성합니다.  
      
    VDDV_{\mathrm{DD}}  
      
  
---  
  
## Moore’s Law  
  
<aside> 💡  
  
2년마다 칩에 들어가는 트랜지스터의 수(집적도)가 2배가 된다.  
  
</aside>  
  
## Dennard Scaling  
  
<aside> 💡  
  
트랜지스터가 작아져도 power density는 유지해야한다. 파워를 적게 써야하므로 전압과 전류가 낮아진다.  
  
</aside>  
  
1. CPU 성능은 Hz(클락 주파수)를 올림으로 달성할 수 있다.  
2. 거리가 작아졌으므로 주파수를 올릴 수 있다. 단, 이러면 전압이 높아져야해서 전력이 증가하고, 열이 발생하게 된다.  
3. 따라서 전력 밀도를 유지하기 위해서는 전압(과 전류, capacity)을 낮게 해야한다. 그 비율은 1/k이다.  
4. 하지만 이는 물리적 한계와 누설 전류로 인해 더이상 전압을 줄이는게 힘들어졌다. (트랜지스터 자체 문제)  
5. 따라서 발열 문제를 해결하기 위해, 더이상 클락 주파수를 높이긴 힘들며 CPU 성능도 정확히 2배씩 증가하지 않는다.  
6. 즉, 엔지니어들은 주파수를 더 올리기보다는 멀티코어 프로세서 등 주파수가 상대적으로 높은 프로세서들을 여러개 연결하는 등 다른 방식으로 CPU의 성능을 올리고 있다.  
  
---
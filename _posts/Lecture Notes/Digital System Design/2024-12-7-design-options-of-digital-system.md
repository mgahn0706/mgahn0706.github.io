---  
tags:  
  - FPGA  
  - ASIC  
share: "true"  
github_title: 2024-12-7-design-options-of-digital-system  
title: 10. Design options of Digital System  
date: 2024-12-07  
categories:  
  - Lecture Notes  
  - Digital System Design  
---  
## Digital system의 option  
  
- ASIC: 특정 알고리즘에 특화  
- micro processor / DSP: 일반적인 이용  
- Field-programmable devices  
    - PLD, FPGA  
  
---  
  
## Design Alternatives of Digital Systems  
  
- Total Cost = NRE cost + Unit cost * Volume  
  
→ `NRE Cost` : Non-recurring cost로 제품을 개발할 때 1번만 쓰이는 비용. (개발 비용, 디자인 비용 등)  
  
→ `Unit Cost`: 하나의 유닛을 만드는 데 드는 비용  
  
---  
  
## FPGA vs ASIC  
  
- FPGA 장점  
      
    - Low cost  
    - low time to market.  
    - low Process complexity  
    - low NRE cost : ASIC은 수 억대라고 함.  
    - simplicity  
- ASIC 장점  
      
    - Design flexibility  
    - Density  
    - Speed  
    - low unit cost  
  
---  
  
### 결론  
  
**ASIC**: High NRE cost, complex but fast. design flexible. Low unit cost  
  
**FPGA**: Slow, but low NRE cost. High unit cost. Easy to use. Low time to make  
  
→ 특정 개수 이하로는 FPGA가 이득, 그 이후로는 ASIC이 이득  
  
`PLD` < `FPGA` < `Gate Array` < `Cell-based ASIC` < `Full custom ASIC`  
  
순으로 비싸고 빠르다.  
  
<aside> 📖  
  
What is the main advantage of ASIC over FPGA?  
  
</aside>  
  
---  
  
# ASIC  
  
- 가장 좋은 에너지 효율과 성능을 보여줌.  
    - 특정 알고리즘에 특화되어있음.  
- 매우 높은 fabrication cost (거의 수억원)  
- long turnaround time (한번 파운더리에 submit하고 돌아오는 시간)  
- 디버그 불가능; 칩을 새로 만들어야함  
  
→ 근데 대부분의 제품은 단순한 기능을 요구하는데 말이야  
  
## Full-custom ASIC  
  
- Start from scratch. need to design layout of every transistor and wire  
- Best performance, but HIGH NRE cost.  
  
## Semi-custom ASIC  
  
- Gate-array based ASIC  
      
    - 배열로다가 p와 n 트랜지스터가 fabricated되어있음  
    - metal layer로 연결되어있으며, NAND나 NOR 게이트를 형성하고 있음. → metal layer만 변경하면 된다.  
- Standard Cell Based ASIC  
      
    - Use Predeisgned logic cell (AND/OR, FF)  
    - Fixed height, variable-width.  
  
---  
  
### Standard Cell Library  
  
- For most process, standard cell library is provided  
  
→ 하나하나 트랜지스터를 짜지 않고로 해당 게이트들을 이용해 나만의 회로를 구현할 수 있다.  
  
- Behavior model  
- SPICE model  
- Delay info  
- Physical Layout  
- Abstract Model  
  
---  
  
## Field-Programmable Device  
  
→ One-time programmable (or erasable)  
  
- FPGA  
- PLD & CPLD  
  
### PLD (Programmable Logic Device)  
  
- 2개의 레벨 (AND-OR)로 이루어진 배열을 사용한다.  
- SOP를 위한 programmable block으로 사용한다.  
  
→ 각 array를 연결을 시키거나 끊음으로써 프로그래밍한다.  
  
(1) Read-only memory (ROM)  
  
- AND array는 모든 minterm을 만들도록 고정되어있다. (ex. ABC, A’BC, AB’C, ABC’, A’B’C, A’BC’ …)  
- OR gate는 프로그램 가능하다.  
  
→ 안쓰는 minterm들이 너무 많다.  
  
(2) Programmable Logic Array (PLA)  
  
- AND OR array 모두 프로그램 가능하다.  
  
→ 이러니 or을 잘 안쓰게 된다. 고정시키자.  
  
<aside> 📖  
  
왜 OR을 잘 안쓰게 되는가 → 굳이 AND로 이미 다 설정이 되어서 OR에서 커스텀 안해도 된다.  
  
</aside>  
  
(3) Programmable Array Logic (PAL)  
  
- OR array 고정, AND를 프로그래밍.  
  
→ Fuse 방식으로 이미 연결된 것을 끊어가며 프로그래밍할 수 있고,  
  
Anti-Fuse 방식으로 연결해가며 할 수도 있다.  
  
---  
  
## ROM Structure  
  
- n개의 인풋과 m개의 아웃풋.  
  
n개의 인풋을 decoder를 이용해 AND array처럼 사용한다.  
  
→ n개의 variable.  
  
예시)  
  
|A1, A0|O1, O0|  
|---|---|  
|00|01|  
|01|10|  
|10|00|  
|11|11|  
  
→ O1은 1 (01)과 3(11)에서 켜야하고. O0는 0, 3에서 켜야한다.  
  
해당 값에만 회로를 연결하여 OR gate로 넘겨준다.  
  
---  
  
## PLA structure  
  
AND와 OR가 모두 programmable하다.  
  
→ 안쓰는 minterm을 줄이기 위해 없앴다보니, implicant 개수가 한정되어있다.  
  
- Boolean Algebra로 최대한 minterm을 줄여 SOP form을 만들자.  
  
<aside> 📖  
  
Draw a scheme for y, xy, w’y’z , xyz’ to PLA structure. with outputs are f1, f1+f2, f2, f3  
  
</aside>  
  
---  
  
## PAL structure  
  
AND만 program 가능  
  
→ 장점  
  
- Less expensive than PLA. Only AND array is programmable.  
      
- Combinational PALs → Implement comb logic  
      
- Registered PALs → Implement seq. logic  
      
- When designing PAL, logic should be simplified.  
      
    - AND terms cannot be shared. (minterm을 여러군데 사용할 수 없다)  
    - OR gate가 한정되어있다.  
  
---  
  
## Complex Programmable Logic Device  
  
Combine many PALs with programmable interconnects.  
  
---  
  
## FPGA  
  
- 구성요소  
    - Configurable logic block (CLB)  
    - Programmable Interconnection  
    - I/O block  
  
→ Can implement any logic function! (but slow..)  
  
- CPLD와 비슷하나, 각각의 로직블럭은 더 단순하다. (CLB)  
      
- 여기서 CLB는 lookup table (LUT)과 FF을 말한다.  
      
- Modern FPGA는 디지털 신호 처리 (DSP) 슬라이스와 BRAM을 갖는다.  
      
- FPGA는 천개 이상의 lut로 scale-up이 가능하다.  
      
  
---  
  
### Look-up table  
  
logic gate를 Program 하자.  
  
→ A & B이면 truth table을 작성할 수 있다.  
  
0 0 - 0  
  
0 1 - 0  
  
1 0 - 0  
  
1 1- 1  
  
이에 맞게 MUX와 1-bit wide SRAM을 이용하여 각 주소 0, 1, 2, 3에 0 , 0, 0, 1을 저장해놓으면 AND Gate가 완성된다.  
  
---  
  
## FPGA Architecture  
  
(a) Matrix type  
  
→ More flexible (좀 더 확장 가능)  
  
(b) Row type  
  
→ faster (붙어 있으니까)  
  
![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/bdc23bea-49ed-413d-9b14-ccfb1b348d92/6ac911d4-2b5f-4f23-802d-be2e96761e8e/image.png)  
  
각 사각형은 CLB를 나타냄.  
  
---  
  
## CLB  
  
Lookup table과 FF로 구성.  
  
→ 2개의 4-input LUT, 1개의 3-input LUT, 2개의 FF  
  
또는 2개의 4인풋 함수, 5인풋 함수로도 프로그래밍 가능하다. ex) 0_1111 1_0000 → 앞 1 bit를 MUX select bit로 넣는 방식.  
  
---  
  
### Programmable Interconnect  
  
Route signal between CLB.  
  
→ long line with some skipping.  
  
- Programmable switch matrix  
    - Six pass transistor로 연결  
  
---  
  
### IO Block  
  
- provide interface between IO pads and internal logic  
  
---  
  
### Modern FPGA  
  
- Device Capacity is measured as ‘logic cells”  
  
→ Lookup table 개수가 아니라, 4-input LUT로 계산했을 때의 기준. (Slice = 6 input LUT 4개 정도)  
  
### Slice  
  
- Each slice have four 6-input LUTs and 8 ffs.  
- `SLICEM` : can be configured as SRAM, shift reg. or comb.  
- `SLICEL` : can only be configured as comb.  
  
---  
  
## Modern FPGA Slice  
  
(1) 7 Series SLICEL  
  
→ 4개의 논리 함수를 만든다.  
  
→ 8개의 저장공간도 있다.  
  
→ Carry-logic이 있다!  
  
(2) DSP48 SLice  
  
- ALU가 embedded되어있다.  
- P=B*(A+D)+C 의 로직을 수행할 수 있다.  
  
(3) Block RAM (BRAM)  
  
- 36 Kbits data를 저장 가능.  
    - 2개를 따로따로 쓸 수 있고, 아니면 한번에 쓸수도 있다. 따로 쓰면 18kbit이겠죠  
  
---  
  
## Designing with FPGA  
  
- Used for prototyping  
    - Much faster than software simulation  
    - Enable system lebel verification  
    - Limited capacity.  
- Now many products uses  
    - Huge reduction in design cost  
    - Energy efficiency comparable to ASIC  
    - Still better performnace than PLD  
  
---  
  
## FPGA compared to ASIC  
  
장점  
  
- manufacturing time 감소  
- 프로토타이핑 cost 감소  
- correct design으로 고치거나 스펙 바꿀 때의 비용 감소  
- design iteration을 돌리기 쉽고 빠름  
- 몇개 안만들거면 더 싸다.  
- 에너지 소모 적음  
  
단점  
  
- Less dense  
- Programmability를 달성하기 위해 많은 리소스가 필요하다  
- 성능이 더 낮음  
- FPGA는 많이 만들면 더 비싸다. (unit cost가 커서)
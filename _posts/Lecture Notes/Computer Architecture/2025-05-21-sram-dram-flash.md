---  
tags:  
  - memory  
share: "true"  
github_title: 2025-05-21-sram-dram-flash  
title: 19. SRAM DRAM Flash  
date: 2025-05-21  
categories:  
  - Lecture Notes  
  - Computer Architecture  
---  
## SRAM  
  
Static Random Access memory  
  
Cache에서 충분히 정리한 것 같지만… 짧게 리뷰해보자면  
  
  
1. Address decode  
2. Drive row select  
3. Select bit-cells drive bitlines  
4. Diff. sensing, column select (precharge된 게 1이었으면 1 유지, 0이었음 빠르게 떨어져서 차이 감지)  
5. 다시 Precharge  
  
### Why Precharge?  
  
그냥 row select에 0을 넣어서 읽으면, 0이면 0 유지하나, 1이면 큰 금속 막대의 전압을 아주 조금 올릴 것이다. (어렵고 오래걸림).  
  
아주 조금 올릴 것이기 때문에 차이 감지가 매우 어려움.  
  
---  
## DRAM  
  
Bits stored as charge in capacitor  
  
→ 시간이 지나면서 점차 discharge. → Need to refresh.  
  
반면 SRAM은 FLIP-FLOP기반 strong storage이고 dynamic power consumption이 아니기 떄문에 따로 필요 없음.  
  
이렇게 올라가고 줄어드는 것을 감지하는 sense amp가 있다. 이건 SRAM인데, 캐시와 비슷한 역할을 한다.  
  
row buffer = sense amp  
  
⇒ 즉, 4KB (Page 크기)일때가 제일 좋음  
  
---  
  
## Clock skewing and SDRAM  
  
clk이 DRAM Chip마다 다르면 안정성 이슈. 거리를 잘 재서 최대한 같게 만드는게 중요함.  
  
### DDR (Double Data Rate)  
  
⇒ 2x data transfer per command (using both rising and falling edge)  
  
거의 뭐 2배의 bandwidth를 낼 수 있지. (2-bit prefetch)  
  
### DDR2, DDR3…  
  
- DDR2  
    - Doubling IO Bus and data bus clocks (4-bit prefetch)  
    - (4x bandwidth over SDRAM)  
- DDR3  
    - Doubling IO bus and data bus clocks (8-bit prefetch)  
    - Power consumption decreased. (over 30% due to 1.8V → 1.5V)  
  
---  
  
## Flash (NAND)  
  
Electrical modifiable, non-volatile storage  
  
- Transistor with a second ‘floating gate’  
- Floating gate can trap electrons.  
- Results in detectable change in Vt  
- FG에 전자가 있으면 0, 없으면 1  
  
---  
  
|Case|Source|Drain|Control Gate|비고|  
|---|---|---|---|---|  
|Erasing (0→1)|Open|+12V|0V|FG에 있던 전자들이 양자 터널링에 의해 빠져나옴|  
|Writing (1→0)|0V|+12V|+12V|gate에 전압이 크게 걸려서 trap|  
|Reading|sensing (I_on at low or hight voltage?)|0V(GND)|+5V|더 높은 Source 전압에서 켜지만 더 작은 전류 → 0으로 처리|  
  
### NOR Model  
  
- Byte level의 random access  
- 읽기가 빠르고 고성능임. (word level)  
- 비쌈 ㅋㅋ  
- 매우 느린 쓰기와 지우기 (block level…)  
- ROM 프로그래밍에 사용 (EPROM, ROM…)  
  
### NAND Model  
  
- Sequential. Block-level programming.  
- 셀 크기를 더 작게할 수 있기 떄문에 density 높음  
- 빠른 쓰기와 지우기  
- 느린 읽기 (하나의 라인을 일단 다 통과해야함)  
- 큰 용량의 저장장소에 사용, 순차적 wordline에 유리  
  
---
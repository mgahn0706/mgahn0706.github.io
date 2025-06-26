---  
tags:  
  - virtual-memory  
  - memory  
  - TLB  
share: "true"  
github_title: 2025-05-07-virtual-memory-2  
title: 16. Virtual Memory (2)  
date: 2025-05-07  
categories:  
  - Lecture Notes  
  - Computer Architecture  
---  
## Translation Look-aside Buffer  
  
- 모든 사용자 메모리는 code든 data든 translation을 필요로 한다.  
- 매번 translation을 기다릴 수는 없는 노릇이다.  
  
TLB: `cache` of most recently used translations!  
  
- VPN → PTE  
- TLB Entry  
    - Tag: address tag (of VA), PID  
    - PTE: PPN + protection bits  
    - Misc: Valid, dirty … 캐시에서 배운 그것.  
  
### Direct-mapped TLB  
  
collision 나면 망함. 다른 프로세스의 것도 한 곳으로 매핑될 수 있기 때문에. collision 나는 순간 망한다.  
  
---  
  
## Designing TLB!  
  
### Capacity  
  
L1 I-Cache가 64KB라면, I-TLB size는 왜 64KB여야 하는가?  
  
- should cover the same 64KB footprint, why?  
- Minimum of 16 TLB entires * some safety factor  
  
TLB-miss는 성능상 매우 안좋음.  
  
→ L1-명령어 가져올때마다 collision으로 miss난다면? L1 Cache hit이 중요한데 아무 의미 없어지잖슴~  
  
### Block size  
  
사실 page table 하나가 거의 4KB라 그 다음 VPN을 같이 쓸 일이 거의 없음. locality가 덜 중요함.  
  
- 보통은 TLB entry 하나당 하나만 mapping함.  
- MIPS는 2개  
  
### Associativity  
  
어떻게 해야 충돌이 덜 날까. 충돌 한번 나면 난리난다.  
  
fully-associative (=CAM)으로 만들던 시절이 있다.  
  
요즘은 여러 translation을 지원하기 위해 2~4 way associative cache가 일반적이다.  
  
---  
  
근데… 언제 translation 하지? TLB는 몇 level의 cache로 설정해야하지?  
  
L1 cache까지는 virtual로 쓰면 되지 않느냐?  
  
→ 다만 문제가 있어용…  
  
### Virtual Cache has problems  
  
(1) Homonyms (=same sound, different meaning. 동음이의어)  
  
- Same EA (in different process) points to different PAs.  
- 사실 다른 놈인데 cache에 덮어씌워져버림.  
    - Context switching 마다 cache flush하기 (멀티스레딩에서 성능 똥망)  
    - PID를 cache tag에 포함시키기. (캐시 나눠쓰는건데 이것도 성능 똥망)  
  
(2) Synonyms (=different sound, same meaning. 유의어)  
  
- Different EAs,… but same PA  
- PA could cached twice under different EAs → Updating only one cached copy not reflect other cached copy!  
  
→ Make synonym cannot co-exist in the cache… but how?  
  
### Hybrid: VIPT (virtually indexed, physically tagged)  
  
C≤(Page size * associativity) … cache index 는 Page offset에서만 나옴. 즉, Page offset에서 적절히 cache처리해서 나온 physical tag를 처리하고, VPN는 TLB 처리해서 나온 PPN으로 처리해서 비교한다.  
  
다만, C > (page size * associativity) 이면,  
  
Associativity가 너무 작으면 set 수가 늘어나고, index로 쓸 비트 수가 page offset 범위를 넘는다.  
  
이때 VA의 상위 비트(VPN)가 index에 포함되면, **서로 다른 VA가 같은 PA를 가리킬 때** 다른 캐시 set에 저장되어 **중복 캐시 entry**, 즉 `s**ynonym` 문제가 발생한다.**  
  
해결법?  
  
- a를 크게 하거나 (associativity가 증가하여 set 개수 감소. IDX에 쓰는 비트 수 감소.)  
- page size를 크게 하거나 (PO 자체가 커짐)  
- Cache size를 줄이거나 (IDX에 쓸 비트 수 자체가 감소)  
- MIPS R10K의 Virtually index Cache를 쓴다.  
    - 2비트 정도는 VPN에서 더 갖다가 쓴 형태. (캐시 크게 만드려고)  
    - 단, VPN[1:0] 자체가 L2의 tag 역할을 함.  
    - L1 miss가 나서 (같은 물리주소이지만, VPN가져와서 달라져서 miss) L2로 내려옴. 다만, L2는 모두 physical address.  
    - PA가 match인데 VPN[1:0] 자체가 달랐네? → synonym! L1의 VA를 강제로 evict하고 VB를 refill해준다.
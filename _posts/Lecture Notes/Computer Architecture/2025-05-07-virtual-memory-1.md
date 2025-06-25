---  
tags:  
  - virtual-memory  
  - memory  
  - page-table  
share: "true"  
github_title: 2025-05-07-virtual-memory-1  
title: 15. Virtual Memory (1)  
date: 2025-05-07  
categories:  
  - Lecture Notes  
  - Computer Architecture  
---  
- Each Process need a large, continuous memory segment without holes!  
- Each memory space should be private  
  
→ Virtual memory! (address translation)  
  
---  
  
## Base and bound  
  
Base: 프로세스의 메모리 주소의 시작 주소  
  
bound: 프로세스 메모리 주소의 끝 주소  
  
→ EA (effective address)는 0~size  
  
PA = EA + base, if PA < bound, ok.  
  
---  
  
## Segmented Address space  
  
base and bound has some problems!  
  
(1) Fragmentation: Free spaces can be fragmented, large contiguous space is hard to come.  
  
(2) Sharing: How to share memory space for two spaces?  
  
→ Let’s give a user `multiple` memory segments. Each segment is contiguous, and base-bound pair.  
  
---  
  
### Translation  
  
[SN][ SO ]  
  
- SN부분은 segment table의 index를, SO는 해당 segment에서의 offset을 말한다.  
- 물론 invalid한지 확인도 한다.  
  
---  
  
### Paged Address Space  
  
[ EPN ][ PO ]  
  
- PO : Page offset (페이지 내에서 몇번째인지. 페이지는 4KB (2^12)이므로 12비트 고정  
- EPN: 20bit. 즉, 32비트 체계에서는 2^20개의 페이지.  
  
---  
  
### Fragmentation  
  
External fragmentation: 크기가 일정하지 않아 빈공간들이 생겨서 공간 낭비되는 이슈  
  
Internal fragmentation: segment가 실사용 크기에 비해 너무 크게 먹어서 사실상 낭비됨. → malloc에서도 열심히 없앴던 기억이..납니다.  
  
---  
  
### Demand Paging  
  
Use main memory and swap disk →memory hierarchy처럼 작동  
  
---  
  
## Page Tables  
  
A page table is an array of page table entries (PTE) that maps VP → PP  
  
- Page hit: VP 바탕으로 page table을 봤는데 DRAM에 올라와있음.  
- page fault: page table 가봤는데 invalid임 (disk에 있다)  
  
그래서 Page table이 얼마나 크냐고?  
  
→ 64비트면 2^(64-12) = 2^52 entries… 그리고 각각은 4바이트 정도.  
  
캬 배보다 배꼽이 더 크자나?  
  
그렇다면 다 track하지말자. 안쓰는 애들은 굳이 매핑 안해도 되잖아?  
  
1. Hierarchy를 만들던가  
2. Hashed (inverted)를 하여  
  
최대한 크기를 줄여보자.  
  
### Hierarchical Page Tables  
  
[VA 31:22]로 L1 table 찾아감.  
  
[VA 21:12]로 L2 table 찾아감…  
  
[VA 11:0]은 원래 PO  
  
모든 unused subtree can be avoided.  
  
장점:  
  
1. unused subtree can be avoided → Space efficiencyy. for sparse memory use.  
2. Scalability  
3. Can find memory in fixed n-time DRAM access.  
  
단점:  
  
1. n-level Page table이라면 DRAM에 n번 접근 → 느림  
2. TLB miss penalty  
3. OS need to manage multiple page tables, page fault → Complexity. Memory size is affected by OS.  
  
### Inverted Page tables  
  
VPN(과 PID)에 hash를 걸면 hashed page table의 index가 나온다. Inverted page table은 물리 주소를 가상 주소로 매핑한 구조이기 때문에 해시된 가상 주소에서 Physical address를 찾는다.  
  
해시된 가상메모리 주소가 같다면 면 같은 pte를 가질거라고 확신하고 가는거지.  
  
장점:  
  
1. DRAM 접근이 1 (~2) 번안에 가능. (common case에서 빠름)  
2. page table의 크기가 DRAM의 크기에 비례하기 때문에 VM 사이즈에 영향 없음  
3. 더 간단한 구현  
  
단점:  
  
1. Worst-case에는 multi-level page table보다 더 많은 search 시간이 필요함  
2. 실제 물리 메모리를 점유하고 있는 가상 메모리만을 매핑하고 있음. 즉, backup page table로 디스크에 있는지 여부를 확인해야함.  
3. Hash를 쓸 경우 hash collision 문제, CAM을 쓸 경우 파워와 비용 문제  
  
Collision 시에는 probing or linked list 방식. (자료구조때 많이 배웠죠?)  
  
Page table을 모두 훑어야하는데 이러면 O(N)의 시간이 걸림.  
  
→ 그래서 CAM으로 한번에 읽을 수 있긴한데 비용과 파워 문제가 있음. 따라서 Hash로 O(1)의 search 시간을 어느정도 구현해서 CAM처럼 동작하도록 만든다. 물론 hash collision떄문에 무진장 느려질 수 있지…
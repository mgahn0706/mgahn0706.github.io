---  
tags:  
  - cache  
  - memory  
  - coherence  
share: "true"  
github_title: 2025-05-14-cache-coherence  
title: 17. Cache Coherence  
date: 2025-05-14  
categories:  
  - Lecture Notes  
  - Computer Architecture  
---  
실제로는 멀티 프로세싱을 하고 있다.  
  
하지만 아키텍쳐적으로는 동일한 shard-memory를 사용하는 것처럼 보여야함,  
  
어떻게 해야하지?  
  
## Snooping Bus Multiprocessor  
  
Bus의 조건  
  
1. 순서가 같다  
2. 하나만 버스 위로 들어간다  
3. latency가 모두 같다  
4. 모두가 볼 수 있다. (broadcasting)  
  
Processors are split from memories (UMA)  
  
→ common, easy to implement  
  
## Scalable Multiprocessor  
  
point-to-point network based  
  
1. No broadcasting  
2. latency differs by member  
3. Can communicate in same time  
  
Processor + Memory + router is one block (NUMA)  
  
→ Scalable, Glueless MP, Can be arbitarily Large, Parallelism.  
  
---  
  
MP → has each private cache, which can violate cache coherency…  
  
## Solutions to Cache Coherence (..?)  
  
### 1. No Caching for shard variables  
  
캐시 안쓰면 되지롱 ㅋㅋ  
  
### 2. Allow multiple copies, but make sure they have same value  
  
- Updates to one copy must be visible to other copies.  
- Multiple readers and writers.  
- 만들기 어려움  
  
### 3. Allow only one copy of a mem location at a time  
  
- 하나의 캐시에 저장이 되었으면 다른 캐시꺼는 꺼버림 (invalid)  
- 다른 프로세서는 누가 최신 값을 가지고있는지 알아야함.  
- one reader / one writer  
  
---  
  
## Multiple Identical Copies Protocol  
  
Based on `write-through` scheme  
  
Cache line is either valid or invalid  
  
- Cache issue read transaction  
- All writes are write-through; cache is coheren with memory  
- All caches snoop the bus for other’s write transaction  
    - 매번 write snoop하고 있다가 새로운 값을 쓰게 되면  
        - 지워버리거나 (invalidate 신호)  
        - 값을 해당 값으로 update (update 신호)  
  
간단하죠?  
  
---  
  
## One-copy at All time  
  
Write-back cache.  
  
Cache lines are either modified or invalid  
  
All caches snoop the bus for other “read” transactions.  
  
- If a cache observes a request, it response and mark its copy ‘invalid’ (더이상 내가 독점하고 있지 않기 때문에.)  
- 일단 메모리에 쓰고 retry하라고 알려줄 수도 있음  
  
→ Why caches dont need to snoop write-back transactions?  
  
“Write back하는 순간에는 어차피 그 캐시가 M 상태이고 그 캐시가 최신 값 (혼자만의 값)이라는게 보장되기 때문이다.” → 나머지는 어차피 Invalid하다.  
  
읽기-sharing이 안되니 망한다.  
  
---  
  
### Multiple copies…with write back?  
  
Mutual exclusion - owner cache는 맘대로 업데이트 가능  
  
Sharing - data read도 여럿이서 가능, 하지만 write하려면 오너십 필요  
  
→ read miss가 나면 누가 최신인지 (메모리인지…아님 다른 캐시가 있는지…) 확인해야하며, 메모리 또한 업데이트해줘야한다.  
  
## MSI Protocol  
  
Read miss → Read transaction  
  
Write miss → Read-with-intend-to-modify  
  
Write-hit, but shared → Invalidate transaction  
  
Evicting Modified → Memory write  
  
---  
  
## Directory Coherence Protocol  
  
Directories: non-broadcast coherence protocol  
  
- Owner: which processor has a dirty copy (M state)  
- Sharers: has a clean copies (S state)  
  
### Centralized Directory  
  
Single directory contains a copy of cache tag from all nodes  
  
Pros:  
  
- Send invalidate and update only to nodes that have copies  
- Central serialization point: easy to get memory consistency  
  
Cons:  
  
- Not scalale, 1000 nodes?!  
- Directory size changes with number of nodes  
- Single point of failure  
  
### Distribute directory  
  
- Memory block = Coherence block  
- Home node → node with directory entry  
- Scalable!  
- Directory can no longer serialize, so memory consistency becomes responsibility of CPU  
  
---  
  
(1) Bit vector-based directory CC: N-bit directory Info (=bit vector) added to cache state bits for N CPU system.  
  
(ex. [10010110] CPU 1, 4, 6, 7 are sharing the block)  
  
→ 128node이면 128 bits, 비트 수를 많이 잡아 먹음. 대부분 cache sharing하는 경우가 많이 없어 낭비가 심함. 예외처리 필요없음.  
  
(2) For too many nodes, Pointer-based Directory CC can be used  
  
(ex. [1001 0110] CPU 9 and CPU 6 are sharing blocks)  
  
→ 2개만 valid하도록 유지. 이러면 돌아는 가지만 성능에 악영향. 개수를 초과하는 경우에는 fallback 등 추가 처리 필요. 공간복잡도는 낮음.
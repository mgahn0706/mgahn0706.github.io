---  
tags:  
  - network  
  - network-layer  
share: "true"  
github_title: 2024-11-30-network-layer-router  
title: 12. Network Layer - Router  
date: 2024-11-30  
categories:  
  - Lecture Notes  
  - Data Communication Network  
---  
Network Layer  
  
- Data plane  
    - Network models  
    - forwarding vs routing  
    - How router works?  
  
→ This is the main bottleneck  
  
---  
  
## Network Layer  
  
- Transports segment from host to host.  
- encapsulates datagram!  
  
---  
  
### Network Layer 기능  
  
(1) Forwarding  
  
- Move packet from router input to appropriate router output  
  
(2) Routing  
  
- Determine route taken by packet from source to dest.  
  
→ We assume shortest path is the best, however congestion happens when all cars recommended to same path.  
  
→ We need load balancing system (which is not in dijkstra)  
  
---  
  
### Data plane  
  
- local, per router function  
- determine how datagram comes and goes  
- forwarding function  
  
### Control plane  
  
- Network-wide logic  
- determines how datagram routed  
    - Traditional Routing algorithm  
        - Implemented in routers!  
    - Software-defined Networking (SDN)  
        - Implemented in servers  
  
Basically, traditional routing algorithm is decentralized. (we cannot make god-like algorithm!) Dijkstra runs in local and it converges in total algorithm.  
  
↔ Google data center can be centralized. May be more useful.  
  
We should consider `fairness` and `performance` .  
  
→ we should make controlled unfairness for performance.  
  
---  
  
## Network service model  
  
→ What model should we use?  
  
(1) For individual datagram  
  
- guarantee delivery and delay  
      
    → there is no single authority, it cannot be guaranteed. (use TCP)  
      
  
(2) For a flow of datagram  
  
- in-order datagram delivery  
- guarantee minimum bandwidth! (penalty other flow)  
- restrict interchange packet (by buffer)  
  
---  
  
### Examples  
  
- Internet: based on scalability, cheaper.  
  
Bandwidth가 낮을 때에는, 싸게 만들고 link의 bandwidth를 늘리는게 중요했음. 현재는 Link 자체의 속도를 희생하고 router에 지능을 넣는게 좋음. 즉, 일반 인터넷 아키텍쳐보다 ATM 같은 아키텍쳐에 여러 모델을 올리는게 더 중요해짐.  
  
→ congestion control를 할 수도 있고, loss, order, timing등을 보장할 수 있는 서비스 모델들이 출시됨. 이는 bandwidth가 높아져서 이런 요소들이 bottleneck이 되고 있기 때문임.  
  
공학에서는 이런 compute bound와 memory buffer bound가 번갈아가면서 bottleneck을 야기하고 트렌드가 자꾸 바뀐다.  
  
---  
  
## Router architecture  
  
high-speed switching fabric. → nanosecond 즉, bottleneck이 됨.  
  
### Input port functions  
  
( Line termination, ADC) → (link layer protocol, Ethernet) → (Lookup and forwarding, queuing) → Switch fabric  
  
Queuing in input port look up IP address by line speed.  
  
If switch fabric is fast, output queue will be large. If switch fabric is slow, input queue will be large.  
  
- destination-based forward: Only IP address  
- Generalized forwarding: All field values  
  
---  
  
## Destination-based forwarding  
  
원래는 모든 IP 하나하나 mapping해주는게 맞지만… 그러면 2^32 만큼의 port가 필요하고 memory가 16GB가 된다.  
  
→ nano second내에 이루어지려면 더 많은 용량이 필요하다.  
  
즉, destination address가 잘 분리되어야한다.  
  
하지만 저 range안에 없고 여러개의 range에 걸쳐있으면 어떨까  
  
---  
  
### Longest Prefix matching  
  
→ 가장 긴 부분이 매칭되는 것을 찾도록.  
  
→ It provides compressed memory table than 1-1 matching, but provides more speciality than range-based method  
  
If table has N rows, it will take O(N).  
  
→ Make O(1) ?  
  
---  
  
### TCAM  
  
using ternary value (0, 1, x) content addressable meories  
  
→ TCAM에 address를 올림. table row수에 관계없이 1 cycle 만에 결과를 얻음.  
  
단, table 수가 많아지면 그만큼 TCAM 수가 많아지고, area와 energy consumption이 증가한다. TCAM 자체도 열과 에너지를 많이 먹는 소자이다. 즉, 열과 비용이 증가한다. 1M까지만 할 수 있다.  
  
---  
  
## Switching Fabric  
  
적절한 input이 들어왔을 때 적절한 output buffer로 보내는 역할  
  
- memory  
- bus  
- crossbar  
  
등을 쓸 수 있다.  
  
---  
  
### Memory  
  
copy packet into system memory  
  
→ low-cost implementation  
  
→ use memory bandwidth twice, 2 bus crossings per datagram.  
  
→ speed limit due to meomory bandwidth, and bottleneck!  
  
---  
  
### BUS  
  
use shared bus  
  
→ switching speed limited by bus bandwidth  
  
No place to store data.  
  
`Bus contention` can be occurred  
  
How to solve?  
  
- Arbitration (중재) 기법: 각 장치가 버스를 사용할 수 있는 우선순위를 정해 충돌을 줄이는 방법입니다. Fixed Priority Arbitration과 Dynamic Priority Arbitration이 있으며, Dynamic Priority는 상황에 따라 우선순위를 조정해 효율적으로 대기 시간을 줄입니다.  
- Bus Segmentation (버스 분할): 여러 개의 독립된 버스를 만들어, 각 버스가 서로 다른 장치를 담당하도록 하여 병목 현상을 줄이는 방법입니다.  
- Time-Multiplexing (시간 분할 방식): 특정 시간 동안 한 장치만 버스를 사용하도록 하여 충돌을 줄입니다.  
  
[bus contention](https://velog.io/@agnusdei1207/bus-contention)  
  
Bus에서는 N * M의 bandwidth가 필요  
  
- N, M은 각각 Input, output port 수  
  
---  
  
### Crossbar  
  
bandwidth limitation을 해결하고자 나옴.  
  
congestion problem 해결 가능.  
  
Increase effective bandwidth  
  
→ Multiple input-output handling  
  
Crossbar는 congestion problem을 해결하지만, 한 포트에만 몰리면 bus와 다를게 없음.  
  
→ highest speed여야함.  
  
→ we may need arbitary management in network mapping, prevent congestion in the output port.  
  
---  
  
## Input port queuing  
  
if fabric switching is slower than packet arrival, queue might occur  
  
`Head of the Line` : blocking. queued datagram blocks the next queues to move forward.  
  
→ long queue will cost more. it requires high speed, so it is very expensive in network layer.  
  
→ have more queues? it will have N^2 queues when we have each queue for each output.  
  
We may have more queue for popular outputs  
  
N^2 → b * N  
  
---  
  
### Congestion controlling in Network Layer  
  
congestion control in fabric.  
  
→ inform sender not to exceed `output queue` size! (If routing is poor and need to wait in output)  
  
If routing is well-distributed, no aggregate in one port.  
  
So, Switch cost will affected by `network topological design` and `congestion control-like mechanism`  
  
If TCP is too aggressive, it can peak packet arrival even though the router was free enough about 1ms ago.  
  
⇒ Due to sender-based control. Let’s do `receiver-based control` !  
  
Example: Credit-based control  
  
Receiver gives coupon(credit) to sender, which acknowledge sender and give it a change to re-issue.  
  
- 2 data / ACK (TCP)  
- 1+(1/cwnd) / ACK (Congestion control)  
- 1 / ACK (credit-based control)  
  
---  
  
## Output ports  
  
outport speed is limited by fiber speed (BDP)  
  
Not to loss any packet, 이론적으로 RTT*Capacity  
  
BDP 만큼의 queue가 필요.  
  
최근에는 N개의 flow가 있을 떄는 (RTT*C) / sqrt(N)  
  
이려면 queuing delay도 줄고, memory도 아낀다.  
  
모든 buffer에 다 몰리는 것은 매우 드문 일이기에 가능하다.  
  
→ 즉, congestion control과 credit-based 등의 작업이 필요함.  
  
---  
  
## Scheduling mechanisms  
  
similar to OS scheduling!  
  
→ Choose next packet to send!  
  
**(1) FIFO scheduling**  
  
send in order of arrival.  
  
what packet to discard?  
  
- tail drop (last one)  
- priority (less important)  
- random (randomly)  
- head drop (first one)  
    - might be useful when the `recent data` is more important.  
    - If loss-tolerant and recent data is important (like UDP), dropping stale packet is more practical way.  
  
**(2) Priority Scheduling**  
  
- send highest-priority packet  
  
→ need to implement multiple classes  
  
→ maybe depend on IP, markings, port…  
  
If always sends higher priority, low-priorred packet will be starved! (preempting system) ↔ non-preempting will weight prior packet. (like 90%)  
  
N queue will give time complexity O(1), one queue will give O(N) to find the most priority packet  
  
**(3) Round-Robin scheduling**  
  
- cyclically scans queue, sends one completed packet for each class  
  
[Round-Robin(RR)이란? , CPU-Scheduling들](https://jwprogramming.tistory.com/17)  
  
**(4) Shortest-remaining time job first**  
  
→ Choose mice flow (command…)rather than elephant flow(data flow)  
  
- There is maximum job count per system. We can maximize handled flow per unit time  
- short flow is more important in AI data center  
  
1. incurring data flow command (small)  
2. ACK signal  
3. real data flow (big)  
  
---  
  
(5) Weighted Fair Queueing  
  
Generalized version of Round Robin  
  
→ Each class have weighted amount of service for each cycle!
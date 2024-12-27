---  
tags:  
  - network  
  - network-layer  
  - control-plane  
share: "true"  
github_title: 2024-12-08-network-layer-control-plane  
title: 14. Network Layer - Control Plane  
date: 2024-12-08  
categories:  
  - Lecture Notes  
  - Data Communication Network  
---  
- Forwarding: move packets from router’s input to router’s output → Data plane  
- Routing: Determine where the packet should go.  
  
**Two approches to sturcture network control plane**  
  
- Per-router control (traditional)  
- logically centralized control (SDN)  
  
---  
  
## Routing Protocol  
  
Let’s determine ‘good path’ for packet  
  
“Good means…”  
  
→ `least cost` , `least congested`, `fastest`  
  
Actually, Routing algorithm is important only topology is given.  
  
---  
  
## Then What is `cost` ?  
  
(1) Fixed quantity  
  
- Propagation delay  
- Link length, hop count  
- Speed, bandwidth  
  
(2) variable quantity  
  
- Average traffic  
- Buffer occupancy  
- Processing delay  
- Error conditions  
  
→ Nowdays, Google Map recommend the shortest path for user, not only giving information, but collect report from requesters and calculate possible congestion.  
  
---  
  
### Why SDN?  
  
→ Router with TCAM cannot perform multiple routing metrics (Hop count, bandwidth…) due to hardware of TCAM  
  
↔ SDN can solve this problem!  
  
---  
  
## Routing algorithm classification  
  
1. Global vs decentralized  
  
- Global  
    - All router have complete. topology, link, and cost info  
    - Link state algorithm!  
- Decentralized  
    - router can only know physically-connected neighbors  
    - iterative process to compute.  
    - distance vector algorithm  
  
1. Static vs Dynamic  
  
- Static  
    - routes change slowly over time  
- Dynamic  
    - route change more quickly  
        - periodic update  
        - link cost changes  
  
---  
  
## Centralized vs Decentralized  
  
### Centralized Routing  
  
- Calculates all path between source and destination  
- Distribute routing information to all noes  
- 단점: Single point of failure, complexity  
  
### Decentralized Routing  
  
- Calculates per router. Each node exchanges information of cost.  
    - Keep exchanges until converges  
- 단점: Convergence problem. It might not be an optimal (by delay)  
  
---  
  
## Some definitions for Graph theory  
  
- `Walk` : Sequence of node s.t. pairs are arcs of G  
- `Path` : A walk with no repeated  
    - In SDN, there might be some firewall, so algorithm might fail due to controlled routes  
- `Graph` : Connected if for each node, there exists a path to every other node  
- `Tree` : Connected graph that contains no cycle  
- `Spanning Tree` : Tree that contains all nodes in G  
  
---  
  
## Proof of Graph  
  
1. `G contains a spanning tree`  
      
2. `|A| >= |N| -1`  
      
3. G is a tree ↔ | A | = | N | - 1  
      
  
→ Prove by induction on n  
  
---  
  
## Link state routing algorithm  
  
### Dijkstra algorithm  
  
→ After k iterations, know least cost path to k destinations  
  
- Some notations  
  
1. c(x, y) : cost from x to y. if not neighbored, infinite  
2. D(v): Current value of cost of path from source to v  
3. p(v): predecessor node along path  
4. N’ : set of nodes whose cost path known  
  
### Pseudo-code  
  
```python  
N' = {u}  
for all nodes v:  
	if v adjacent to u  
		then D(v) = c(u,v)  
else D(v) = inf  
  
1. find w not in N', such that D(w) is a minimum and add to N'  
2. Update D(v) for all v adjacent to w, and not in N'  
	D(v) = min(D(v), D(w)+c(v,w)) # 그냥 가는 것과 w를 거쳐서 가는 것 중 더 짧은 것  
	  
3. Repeat this until all nodes in N'  
```  
  
Prove) If already - selected path is not a minimum → it causes cycle, or negative cost  
  
### Advantages  
  
- Algorithm complexity with n nodes  
- need to check all nodes w → n(n-1)/2. nodes → O(n^2)  
- can be achieved by O(nlogn)  
  
### Disadvantages  
  
- This might be slow because we have to collect all link-state before start!  
- May cause oscillations.  
    - Can be solved by implementing more static system  
  
→ Network does their best, but it will cause out-of-order problem and affect upper layer.  
  
---  
  
## Distance vector algorithm  
  
Bellman-Ford equation (DP!)  
  
dx(y) = min { c(x, v) + dv(y) }  
  
→ x에서 y까지 가는데의 최소비용은 x에서 v까지 가는데의 최소 비용과 v에서 y까지 가는데 최소 비용 중 최솟값이 있는 v에서 나온다.  
  
이렇게 계산한 distance vector를 저장하고 있다가, 요청 시에 이웃에게 건네준다.  
  
### Advantages  
  
- Do not require the information beyond the neighbors  
  
## 특징  
  
- Iterative, asynchoronous  
    - local iteration can caused by  
        - Local link cost change  
        - DV update message from neighbor  
- Distributed  
    - Each node notifies neighbors only when its DV changes  
  
---  
  
### Asynchronous system  
  
- Simple; don’t have to find a straggler  
  
### Synchronous system  
  
- Can exchange data with recent information  
      
- All update executed in same timing  
      
    - Can converge to some point faster.  
- Have to define timing  
      
    - should define timing  
    - Should operate in discrete timing interval  
        - Heterogeneous performace, and need to adjust the slowest guy. (straggler)  
  
If we have deadline converge time, synchronous might be useful.
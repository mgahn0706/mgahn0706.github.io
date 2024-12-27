---  
tags:  
  - network  
share: "true"  
github_title: 2024-09-25-packet-switching  
title: 2. Packet Switching  
date: 2024-09-25  
categories:  
  - Lecture Notes  
  - Data Communication Network  
---  
## Data는 packet으로 전달된다.  
  
- application의 메시지를 전달함.  
- L bits의 길이를 가지는 packet으로 나눠짐.  
  
해당 packet은 transmission rate (bits/sec)에 따른 속도로 전달된다.  
  
이는 bandwidth, capacity라고도 한다.  
  
즉, 하나의 패킷의 delay = `L/R`  
  
---  
  
## Packet Switching  
  
패킷은 한 hop을 가는데 L/R만큼의 시간이 걸린다.  
  
즉, end to end를 계산한 one-hop을 계산하면 2L/R인 것이다.  
  
- 만약 n-hop이라면 (N+1)(L/R) 걸린다.  
- k개의 패킷을 넘긴다면 (N+k)(L/R) 이다. - 첫번째 패킷이 들어온 이후부터 k-1개 더 기다려야하기 때문.  
  
→ store and forward, 즉 다음 link로 가기 전에 패킷이 모두 도착된 것이 보장되어야 한다.  
  
### Wormhole routing  
  
헤더만 받고 바로 출발한다는 아이디어.  
  
이 경우에는 (L/R)+(header time)*n 이다.  
  
- packet error 체크 불가능  
  
## Queueing and Loss  
  
- arrival rate가 transmission rate를 넘어가면…  
      
    - packet은 queue에 담긴다  
    - buffer를 넘어가면 drop한다.  
      
    → 그럼 infinite에 가까운 queue를 만들자!  
      
    - Packet loss는 줄겠지만, 속도가 빨라지는데 영향을 주지 못한다.  
- 그럼 optic fiber에서는 어떻게 하지? mirror?  
      
    - optical buffer라는 큰 circle을 만들어서 빛을 계속 돌게해 가둬놓는다.  
    - forwarding은 OEO를 사용하거나, MEM-spaced mirror system을 사용한다.  
  
### Routing and Forwarding  
  
- Routing: routing 알고리즘에 따라 header value에 따른 output link를 정한다.  
      
    - 네트워크 상황에 대해 알지는 못한다.  
- Forwarding  
      
    - 패킷을 적절한 output으로 보낸다.  
    - 이 과정이 중요한데, router가 1000 output port라면 forwarding processor는 router보다 1000배 빨라야한다.  
      
    → 각 port가 1Mbps라면, forward processor는 1Gbps를 처리해야한다는 뜻이다.  
      
  
---  
  
### Circuit Switching  
  
과거의 전화선에 많이 썼던 방식.  
  
end-to-end 리소스가 이미 할당되어있다.  
  
- 장점  
    - guaranteed performance  
    - no packet loss  
    - no hop, so speed is almost c. delay is (L/R)  
    - no blocking, no fluctuate  
- 단점  
    - idle when not using → resource waste  
    - data rate를 나눠가짐. (스위치 간의 속도가 1Mbps라면, 각 전화선당은 250kbps)  
  
<aside> 📖  
  
단점이 이거밖에 없나?  
  
</aside>  
  
---  
  
### Queueing Delay, Throughput  
  
La → (queue) → R  
  
여기서  
  
- L: length of packet(bits)  
- a: average packet arrival rate  
- R: transmission rate(or link bandwidth)  
  
여기서 La/R 의 갓을 traffic intensity라고 한다.  
  
- La/R ~ 0: avg. queueing delay is small.  
- La/R < 1 : avg. queueing delay is large.  
- La/R > 1: packet drops. avg delay is infinite if not dropping  
  
이때 Kendall’s notation에 의해 들어오는 Queueing system을 살펴볼 수 가 있다.  
  
M/M/1 을 가정하는데,  
  
M: 고객의 도착시각 분포 (푸아송 분포)  
M: 서버처리 시간 분포 (푸아송 분포)  
1: 서버 수  
Infinite: queue의 크기  
  
를 의미한다.  
[[이동통신] (큐잉시스템) Queuing system에 Kendall's Notation적용 - 고객당 평균체재 시간, 평균 큐의 길이, 고객당 평균 대기 시간](https://m.blog.naver.com/parkppjjmm/221674156928)  
  
즉, M/M/1에서는 infinite queue 상황을 가정한다.  
  
La/R에서 R은 줄이기 힘들다. 이미 설비가 완료되었기 때문.  
  
즉, 우리는 La를 줄여야한다.  
  
근데 이걸 줄이면 packet 단위에서는 이득일지 몰라도, throughput이 줄어든다.  
  
- Queue에 있는 packet 수의 기댓값  
  
---  
  
### Thorughput과 Bandwidth의 차이  
  
여기까지 공부했다면 thorughput과 bandwidth가 헷갈릴 수도 있을 것이다.  
  
- Throughput  
    - 특정 시점에서 한 채널에서 전송된 데이터의 양 (bps)  
    - 모든 layer에서 사용  
    - 실제로 전송된 데이터의 속도로, practical한 면이 있음.  
    - 실제 전송된 값이므로 latency가 적용된 것임  
- Bandwidth  
    - 어떤 channel이 전송할 수 있는 데이터 양(속도) - capacity  
    - physical mean에 좀 더 focus  
    - latency와 관련 없음  
  
bandwidth는 물이 나오는 수도꼭지에서 수도꼭지가 감당할 수 있는 물의 속도.  
  
throughput은 실제로 물이 나오는 속도로 이해하면 좋겠다.  
  
[Difference between Bandwidth and Throughput - GeeksforGeeks](https://www.geeksforgeeks.org/difference-between-bandwidth-and-throughput/)  
  

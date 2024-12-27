---  
tags:  
  - network  
share: "true"  
github_title: 2024-09-26-delay-in-packet-switching  
title: 3. Delay in packet switching  
date: 2024-09-26  
categories:  
  - Lecture Notes  
  - Data Communication Network  
---  
## Queueing and Delay  
  
queue에서 패킷 수의 기댓값은  
  
$$ E(N) = \sum_{n=1}^{\infty} nP_n  
  
$$  
  
이다. 여기서 P_n(n개의 고객이 있을 확률)은 다음과 같다.  
  
$$ P_n = (1 - \rho) \rho^n $$  
  
여기서 rho는 서버의 사용률이다.  
  
$$ \rho = \frac{\lambda}{\mu}  $$  
  
---  
  
## Loss and Delay  
  
Packet의 arrival rate가 output link의 capacity를 넘기는 경우.  
  
- Packet이 전달되는데에는 두 가지 delay가 있다.  
    1. transmitted delay (패킷이 queue에서 다른곳으로 transmit될 때 어디로 갈지 정하는 delay)  
    2. queueing delay(패킷이 router buffer에서 기다리는 delay)  
  
만약 위의 delay로 인해 free buffer가 사라진다면, 패킷은 드랍됨.  
  
드랍되면 re-transmit을 하면서 시간이 2배로 늘어남.  
  
**그렇다면 packet loss 발생 시 어떻게 하는게 좋을까?**  
  
- 드랍된 packet을 re-transmit한다. (throughput이 중요한, 큰 파일 전송에 좋음)  
- 그냥 몇개 드랍한다. (delay가 작은게 중요한 drone등에서 좋음)  
  
### Priority Queue  
  
우선순위 큐를 이용하면 packet이 drop되어도 덜 중요한게 drop될 수 있다.  
  
- 각 packet마다 우선순위를 미리 정해놓아도 좋고  
- 각 queue에 우선순위를 정해도 좋다.  
  
→ 아니면 service의 퍼포먼스를 올려버리자. 가장 간단한 해결방법이다. (비싸지만 구현 난이도 감소)  
  
→ 하지만 이런 노력에도 불구하고, 우리는 latency를 보장할 수 없다.  
  
**(1) Admission Control**  
  
- Process에 들어오는 요청의 수 제한 → redirect 시키거나, request 자체를 drop 시킴.  
  
→ (이거 현재 네트워크 상황을 Application이 알 수 있나?)  
  
**(2) Overprovision hardware revision**  
  
미리 네트워크 자원을 생산.  
  
buy more equipment!  
  
---  
  
## Queueing and Delay  
  
그래서 queueing에서 딜레이는 무엇무엇이 있을까. 물론 여기서는 packet 기준 딜레이이다.  
  
$$ d_{e2e} = d_{proc} + d_{queue} + d_{trans} + d_{prop}  $$  
  
1. processing delay  
    - 패킷의 헤더를 분석하는 delay (header detaching time)  
    - 어느정도 deterministic함. (예측 가능함)  
    - hardware spec에 비례함.  
    - ms단위임.  
2. queueing delay  
    - 패킷이 한 router에 몰려 router buffer에 queue되고 있는 경우의 기다리는 delay  
    - 제일 예측하기 어려움  
    - greedy하게 사용하면 congestion 발생 → collapse  
3. transmission delay  
    - router의 routing algorithm에 따라 해당 패킷이 다음에 어디로 가야하는지 알고, 보내는 delay.  
    - medium에 집어 넣는 delay라고 보면된다.  
    - hop의 개수가 많을수록(store-and-foward에서는), bandwidth가 작을수록, packet 사이즈가 클수록 증가한다.  
4. propagation delay  
    - hop(한 라우터에서 다른 라우터까지 걸리는 시간)  
    - physical 적인 부분임.  
  
---  
  
### Real Internet Delay  
  
traceroute  
  
```c  
router.asus.com (111.111.111.111) 2.0ms 3.0ms 1.0ms  
router.asus.com (222.222.222.222) 1.9ms 4.0ms 2.0ms   
// sequential  
  
1.1.1.1 (1.1.1.1) 5.0ms  
2.2.2.2 (2.2.2.2) 6.0ms  
3.3.3.3 (3.3.3.3) 5.5ms // parallel  
```  
  
실제로 ping 또는 traceroute를 사용하면 hop-by-hop으로 delay를 확인할 수 있다.  
  
Q. 왜 1번째 try에서 1번째보다 2번째가 더 빠른가.  
  
1번째: pc → 1 → pc  
  
2번째 : pc → 1 → 2 → pc 를 따로따로 측정했기 때문에 더 빠를 수 있다.  
  
[Ping 과 Traceroute 동작원리](https://blog.naver.com/sjh2zo/100043122860)  
  
1. Ping  
  
호스트가 다른 호스트에게 ping을 보내면 해당 호스트는 다시 응답을 보낸다. 이 시간을 계산한다.  
  
1. Traceroute  
  
TCP/IP 에서는 TTL(time-to-live)값이 0이 되는 순간 에러를 원-호스트에게 보낸다. 따라서 TTL값을 1, 2, 3…으로 늘려나가면서 최종 도착지 (R)에게 요청을 보낸다.  
  
즉, 특정 지점까지 도착하는 요청들의 ping 시간을 측정하면서 각 단계별 걸리는 시간을 측정할 수 있다.  
  
---  
  
## Throughput and Bottleneck  
  
그래서 throughput이 뭔데  
  
- Throughput은 rate at which bits transferred between sender/receiver를 뜻한다. bandwidth는 어떤 wire가 처리할 수 있는 최대 속도이다.  
    - 즉, throuput은 순간일 수도, 평균일 수도 있다.  
    - 보통 평균 많이 씀  
  
→ 왜 평균을 많이 쓸까?  
  
- 대체로 throughput을 측정하는 경우에는 시간이 오래 걸리는 경우가 많음  
- internet 상황에따라 순간 throughput은 잘 변하기 때문에 평균으로 하는 것이 consistent함  
  
위 그림에서의 평균 throughput은 Rc이다. 수도꼭지를 생각해보자.  
  
→ 가장 minimum bandwidth이 throughput으로 결정된다.  
  
---  
  
### Throughput formula  
  
O — R1 —→ O — R2 —> O : bandwidth  
  
(1) n-byte의 패킷을 보낸다면  
  
총 throuput은 R1이 R2보다 빠르다고 했을 때  
  
$$ \frac{n}{\left( \frac{n}{R_1} + \frac{n}{R_2} \right)} = { \frac{R_1 R_2}{R_1 + R_2}}  
  
$$  
  
이다.  
  
한편, k개의 패킷을 전송할 때에는  
  
$$ \frac{kn}{\left( \frac{R_1}{n} + k \left( \frac{n}{R_2} \right) \right)}  $$  
  
이다. R1은 충분히 빠르기 때문에 첫 패킷 송신 1회만 시간이 추가되고, 그 후는 n/R2 가 가장 영향을 크게 미친다.  
  
즉, R1이 R2보다 많으면 중간 router에서 queue drop이 있을 수 있기 때문에 첫번째 컴퓨터가 자중해야한다. 즉, Transport layer 단에서 현재 다음 컴퓨터의 상태를 확인하고, rhythm을 check해야한다. (slow down~)  
  
**만약 R1이 R2보다 느리다면?**  
  
R1 < R2일 경우에는 n-byte 패킷을 전송하는데에는 위 식과 같지만, k개의 패킷을 보낼때에는 식은 동일하다. 하지만, bottleneck이 되지 않고 packet이 drop될 위험이 더 작다.  
  
---  
  
실제 네트워크 사용에서의 e2e throughput은 min(Rc, R/10, Rs)이다.  
  
대부분 Rs나 Rc가 문제일 가능성이 높다.  
  
R을 아무리 n으로 나눠도 Rs, Rc보다는 크다.  
  
- Rs: server의 속도는 사실 충분하다. AWS를 봐라.  
- 가운데 있는 저 fiber는 사실상 못바꾼다.  
- Rc: 대용량 파일 다운받는거 아니면 괜찮다.  
  
---  
  
### Encapsulation  
  
각 패킷은 encapsulation이 잘 되어서, 각 단계에 맞는 layer까지만 detatch되었다가 다시 attach된다.  
  
---  
  
### Packet Capturing  
  
보안은 Network의 영역이 사실 아니다.  
  
보안은 Application 영역에서 보통 처리한다. 암호화가 되어있다는 뜻이지.  
  
따라서 Ethernet에서 가져온 정보를 pcap(packet capute)하여 packet analyzer(Wireshark)에 store한다.  
  
그럼 남의 패킷에 담긴 정보를 볼 수 있다!  
  
패킷은 공중에 떠돌아다니기 때문에 마음대로 캡쳐가 가능하다.  
  
wire로 되어있는 LAN선도 마찬가지이다. bus형태로 되어있기 때문에 남의 신호가 나에게도 온다 = 캡쳐가 가능하다.  
  
---  
  
## Internet History  
  
### Packet switching  
  
1. 1961: queueing theory  
2. packet-switching  
3. ARPAnet  
4. ARPAnet with 4 nodes (in America)  
5. 1. ARPAnet public demo  
    2. Network Control Protocol  
    3. e-mail  
  
이후…  
  
### Internetworking  
  
1. ALOHAnet satelite network (link layer)  
2. Cerf and Khan - architecture for interconnecting network  
3. Ethernet  
4. DECnet, SNA, CNA  
5. switching fixed-length packet  
6. ARPAnet has 200 nodes  
  
---  
  
### Cerf and Khan’s internetworking principles  
  
- Minimalism, autonomy - no internal change is required to connect networks  
- **best effort service model**  
    - 단순한 일을 하여, 각 네트워크의 상태를 모르고,  
    - 네트워크 속도는 보장할 수 없지만, 최선의 서비스를 제공하고자 함  
- stateless routers  
- decentralized control  
  
---  
  
### Later…  
  
- TCP / IP  
- FTP  
  
(여기서 만들어진 애들이 아직도 쓰이는 중. 특히 IP.)  
  
IP는 한번 바꾸려는 운동이 있었는데 너무 core해서 실패함.  
  
- Web
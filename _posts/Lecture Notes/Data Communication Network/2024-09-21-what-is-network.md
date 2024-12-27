---  
tags:  
  - network  
share: "true"  
github_title: 2024-09-21-what-is-network  
title: 1. What is Network?  
date: 2024-09-21  
categories:  
  - Lecture Notes  
  - Data Communication Network  
---  
Network가 뭘까. 인터넷은 뭐고, 그걸 연결하는건 어떻게 이루어질까?  
  
---  
  
인터넷은 backbone이 있고 그 backbone을 ISP(주로 통신사들)이 연결해주는 형태를 띈다.  
  
이를 통해 우리는 인터넷을 사용할 수 있게 된다!  
  
이런 인터넷을 사용하기 위해서는 통신규약, 즉 프로토콜이 필요하다. 지금은 간단하게 어떤게 있는지 보고 하나하나 살펴보도록 하자.  
  
1. Application layer  
      
    - 네트워크 애플리케이션의 동작을 돕습니다.  
    - the layer where network applications and application-layer protocol resides  
      
    ex) FTP, SMTP, HTTP  
      
2. Transport layer  
      
    - process간의 데이터 전송을 처리합니다.  
        - transports application layer’s data between endpoints  
    - transmission data rate가 여기서 결정됩니다.  
    - ex) TCP, UDP  
3. Network  
      
    - datagram이 목적지까지 잘 가도록 routing 해줍니다.  
        - moves packets which is datagram from host to another host  
    - ex) IP, routing protocol  
        - routing protocol은 인터넷의 도움 없이, 자체적으로 minimum bandwidth timed을 계산한다. 다른 회사의 peering cost를 계산하기도 하며 자체적인 알고리즘이 존재한다. 5장에서 배운다 ㅎ  
4. Link  
      
    - network element간의 data transfer를 돕는다.  
        - Move a packet from a node from another node. (between network element)  
    - Ex) Ethernet, WiFi, Bluetooth  
5. Physical  
      
    - 이 강의보다는 통신의 기초 과목에서 많이 다룰 듯  
    - wire 위의 bit들을 처리하는 모든 것을 의미한다.  
        - move the individual bits on the wire, from one node to next.  
    - 2/3 light speed로 처리됨 (coax wire, air, optic fiber, twisted pair copper wire…)  
  
이 중 application designer (그러니까 산기요 시절 나)의 interest는 Application Layer와 Transport Layer일 것이다. 그 외에는 이미 설비가 다 정해져있으니까.  
  
---  
  
Network Protocol  
  
= 통신할 때 지켜야하는 약속. 안지키면 discard 해버림.  
  
- ‘안녕’이라고 물어보면 안녕이라고 해야해.  
- ‘몇시야’라고 물어보면 시간을 얘기해줘야해.  
- 일정 시간 대답이 없으면 다시 물어볼거야.  
    - 언제까지  
  
모든 인터넷 통신은 규약을 지켜야한다.  
  
ex1) 전기자동차 충전기 연결 시  
  
- 충전 스펙이 어떻게 돼  
- 몇 와트까지 가능해  
- 현재 배터리 잔량은?  
  
ex2) HDMI로 빔 프로젝터 연결 시  
  
- 해상도가 어떻게 돼 등  
  
> 프로토콜은 네트워크 entity 간에 주고받은 `메시지` 의 형식와 순서를 정의한다. 또, action token을 정의한다.  
  
<aside> 📖  
  
Action Token?  
  
</aside>  
  
---  
  
Network에는 Core와 Edge가 있다.  
  
- Network Core  
    - interconnected routers  
    - network of networks (결국 network edge들을 연결해주는 backbone이란 소리. 짱짱큰 ISP가 만들어준다.)  
- Network Edge  
    - hosts, clients, and servers  
    - Data center에 있는 server까지도.  
        - 즉, core와 비슷한 위치에 있더라도 edge로 본다. 어떤 역할을 하는지가 더 중요하다.  
  
→ 우리는 last-mile network에서 네트워크를 이용한다. 와이파이 등등으로  
  
---  
  
우리는 여기서 원격으로 Network에 연결한다. 원격 Network를 좀 더 알아보자.  
  
Wireless한 통신 방식에는 여러가지가 있다. 3G, 4G같은 WWAN부터, 블루투스같은 WPAN도 있다. 이렇게 통신 Range에 따라 다른 통신 방식을 쓰며, 이에 따른 data rate도 존재한다.  
  
- Data rate vs Range  
  
Range를 키우면 signal과 noise를 구분하는 data rate이 감소한다. 이는 섀넌의 법칙에서 알 수 있다.  
  
[채널 용량](https://ko.wikipedia.org/wiki/%EC%B1%84%EB%84%90_%EC%9A%A9%EB%9F%89)  
  
참고.  
  
채널 용량 = 에러 없이 보낼 수 있는 data의 최대 속도(data rate).  
  
C = Wlog(1+Ps/Pn); 인데, Ps/Pn 값에 비례하는 것을 볼 수 있다. 고리가 멀어지면 자연스럽게 두 신호의 전력 차이가 줄어드릭 떄문에 채널 용량이 감소하며 이에 따라 data rate이 줄어들 수 밖에 없는 것이다.  
  
**다 같은거 쓰면 안됨? Range 상관없이 다 같은거 써버리자.**  
  
→ bandwidth가 한정적이다.  
  
→ bandwidth가 비슷한 두 신호가 있다고 가정하자. global level에서 쓰는 전파에 의해 local에서 쓰는 것이 distorted될 수 있다.  
  
→ 즉, long / short 에 따라 bandwidth를 구분해주고, 이를 orchestrate해주는 center도 필요하다.  
  
long 거리를 보내려면 좀 더 detailed된 implication이 필요하니까.  
  
이런 통신 관련 부품들을 어떻게 다룰 것인가에도 여러 고민이 있다.  
  
하나의 부품이 multi-purpose하게 쓰이게 한다.  
  
- local 통신에서도, global 통신에서도 하나의 기기를 가지고 통신할 수 있다.  
- 부품 1개당 가격이 비싸진다.  
  
부품 1개당 하나의 목적을 가지게 한다.  
  
- 기능이 많은 부품을 만드려면 규모의 경제에 의해 비싸진다.  
- 기능이 하나인 부품을 만들 때 규모의 경제에 의해 싸게 만들 수 있다.  
  
---  
  
- Data rate vs mobility (speed)  
  
왜 이동통신 단말기기가 빠르게 움직이면 data rate가 줄어들까?  
  
→ 무선으로 통신해서 전파가 온 공간에 퍼진다. 즉, 각 신호별로 phase가 다르게 오게 되고, 세기가 감소한다.  
  
→ 여기서 사용자가 이동하면 channel estimation을 다시해야한다. 빠를수록 어려워진다.  
  
→ maximum data rate를 달성하기 힘들어진다.  
  
위 문제는 fundamental한 문제가 아니다. 즉, channel estimation에 의한 것이라 기술 적용에 따른 side effect인 것이다.  
  
우주에서는 방해물이 없고 direct로 위치 계산해서 쏠 수 있어 해당 drop이 거의 일어나지 않는다.  
  
---  
  
Application layer에서는 OS kernel의 network driver가 존재한다.  
  
→ 여기서 TCP header, Link layer 등을 붙인다. 그리고 복호화때 다시 올라온다.  
  
이 과정이 serial하게 일어나기 때문에 느리다.  
  
- application layer에서 DPDK libraries를 이용한다.  
	packet 번들을 받아서 처리한다.  
  
단점  
- throughput은 빠르지만, bundling을 이용하기 때문에 1개의 packet 기준으로는 느리다.  
- 지원되지 않을 수 있다.  
  
---
---  
tags:  
  - tcp  
  - network  
  - cs  
share: "true"  
github_title: 2023-08-07-tcp-feat-udp  
title: TCP (feat. UDP)  
date: 2023-08-07  
categories:  
  - Development  
  - Server  
---  
  
  
TCP(Transmission Control Protocol)는 네트워크 표준 모델링 중, **전송 계층**에서 사용하는 프로토콜이다. ISO에서 만든 OSI model에서 표준이 되는 프로토콜입니다.  
  
TCP protocol은 `연결 지향 방식` 으로 `패킷` 을 지향하며 `3-way handshaking` 과정으로 목적지/수신지 간 정확한 전송을 보장한다.  
  
→ 무슨 말인지 세세히 알아보자.  
  
TCP는 통신하고자 하는 두 엔드포인트가 통신 준비가 되어있는지, 데이터가 정확히 잘 전달되었는지 등을 점검한다. 이때 TCP는 3-way handshake 방식으로 작동합니다.  
  
1. 송신자가 수신자에게 ‘SYN’을 전송하여 통신이 가능한지 확인합니다. Port가 닫혀있거나 통신이 불가능하면 이를 받지 못합니다.  
      
2. 수신자가 송신자에게 ‘SYN’을 받고 ‘SYN/ACK’ 를 보내서 통신할 준비가 되어있음을 알립니다.  
      
3. 송신자가 수신자의 ‘SYN/ACK’를 받은 후 ‘ACK’을 보내서 전송 시작을 알립니다.  
      
  
모든 TCP는 이런 3 way hanshake을 통해 시작하며, 수신자와 송신자 간의 안전한 데이터 전송이 가능한지 미리 확인하게 됩니다.  
  
이렇게 연결 확립이 되면, 송신자는 수신자에게 데이터를 나눠서 보내고, 수신자는 항상 데이터 도착여부를 다시 송신 호스트에게 알려줍니다. TCP에서는 수신 호스트가 확인 응답(ACK)을 보내게 되는데, 이는 수신 호스트가 몇번째 데이터를 수신했는지, 다음에 전송해줄 데이터는 몇번째인지 알려주는 Acknowledgement number로 이루어져 있습니다.  
  
다만, TCP는 패킷에 대한 응답을 하므로 연속성과 속도에 불리합니다.  
  
모든 패킷에 대해 하나하나 성공 여부를 다시 알려주어야하고, 만약 중간에 실패한 경우가 있다면 송신자가 데이터를 재전송하여 데이터 전송의 신뢰성을 확보합니다.  
  
이에 비해 비연결 지향적 프로토콜인 UDP (User Datagram Protocol)은 연결 절차가 따로 없이 송신자가 일방적으로 데이터를 전송합니다. 따라서 위의 TCP보다는 빠르지만, 패킷 유실 및 변조 시에 재전송을 안하기 때문에 신뢰성은 떨어지게 됩니다.  
  
따라서, 안정적이고 신뢰도 높은 통신에는 TCP가 보통 활용됩니다. DB에 접근하거나 원격 로그인을 하는 경우, 안정적 통신이 더 중요하기 때문에 TCP를 활용합니다.  
  
반대로, 실시간 스트리밍같이 빠른 전송속도와 실시간 통신을 지원하는 경우 UDP가 활용되죠.  
  
  
### 참고자료  
  
---  
  
[https://better-together.tistory.com/140](https://better-together.tistory.com/140)  
  
[https://www.geeksforgeeks.org/differences-between-tcp-and-udp/](https://www.geeksforgeeks.org/differences-between-tcp-and-udp/)
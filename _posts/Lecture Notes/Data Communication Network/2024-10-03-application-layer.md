---  
tags:  
  - network  
  - application-layer  
share: "true"  
github_title: 2024-10-03-application-layer  
title: 4. Application Layer  
date: 2024-10-03  
categories:  
  - Lecture Notes  
  - Data Communication Network  
---  
## Network Application  
  
어떻게 카카오톡을 통해 두 디바이스가 통신하게 할까.  
  
매번 IP 주소는 바뀐다. 기기가 이동하니까. 그러면 어떻게 그 둘을 같다고 인식하고 연결하지?  
  
일단, 하나의 고정된 IP address를 가지는 기기가 필요하다.  
  
보통 우리는 이것을 ‘서버’의 컴퓨터로 고정해놓고 쓴다.  
  
(1) Polling  
  
매번 서버가 IP 주소를 일정 간격으로 check한다.  
  
- 알려주기 전까지 IP가 일치하는지 알기 어렵다.  
- It sacrifices device battery  
  
(2) WebSocket  
  
클라이언트가 자신의 IP address가 바뀌었을 때 서버에 고지한다.  
  
---  
  
## Creating a Network Application  
  
각 end system에서 돌아가는 프로그램을 짜자.  
  
우리는 network-core device들을 위한 코드를 짤 필요가 없다!  
  
각 layer에 대한 고민만 하면 되는 걸  
  
---  
  
## Architecture 1 - Server and Client  
  
### Server  
  
- always-on host  
- permanent IP address (mostly)  
    - 요즘은 permanent domain name에 가까움. (DNS에 저장됨)  
    - 왜 IP 주소를 안하고 DNS를 쓸까?  
        1. 이름을 기억하기 쉬움.  
        2. 가장 빠른 서버로 redirect하기 좋음 (ex. 미국에서 네이버 접속하는 경우 한국대신 일본 데이터 센터의 서버 주소로!)  
- data centers for scaling  
  
<aside> 📖  
  
scaling을 위한 data center가 무슨 말일까? → 이용자 수에 따른 server capacity 조정.  
  
</aside>  
  
### Clients  
  
- 서버와 서로 통신함.  
- dynamic IP address를 가질 수 있음  
- 클라이언트끼리는 서로 통신하지 않음  
  
<aside> 📖  
  
Web Socket의 경우에는 클라이언트끼리 실시간 통신을 하는 것으로 아는데, 이것도 클라이언트 간 바로 통신하는 것은 아닌가?  
  
</aside>  
  
---  
  
## Architecture 2 - P2P  
  
peer to peer  
  
- No always-on server  
- 임의의 두 시스템이 직접적으로 통신함  
- **Self scalability**  
    - 새로운 peer가 들어오면 그것은 서비스에 새로운 용량이 늘어났다고 볼 수 있다.  
    - 즉, peer가 하나 증가하면 수요에 맞추어 공급도 증가한다.  
  
→ Client-server에서는 peer가 증가하면 그만큼 서버가 부담해야하는 통신 비중이 증가한다.  
  
다만, p2p에서는 self-scalability 덕분에 각 peer가 부담하는 양이 그렇게 늘어나지 않는다. 또, server infrastructure가 필요하지 않기 때문에 cost-effective하다.  
  
- peer는 간헐적으로 connected되며 계속 IP address가 변경된다.  
      
    → 관리하기는 힘듦  
      
    → reliability가 낮음  
      
    → performance가 보장되지 않음  
      
  
사실 처음에 각 end system들을 연결해주려면 고정된 서버가 필요하긴 하다…  
  
---  
  
## Process  
  
process는 host 안에서 실행중인 프로그램을 말한다.  
  
PID는 user에 의해 실행된 프로세스나 OS에 의해 실행된 프로세스의 id를 말한다.  
  
(우리는 user에 의해 실행된 것만 다룬다.)  
  
- 하나의 host 안에서는 inter-process communication을 통해 두 개의 프로세스가 통신한다.  
- 다른 호스트에 있는 프로세스는 message를 교환하며 통신한다.  
  
**→ 우리에게는 다른 호스트의 pid가 없는데 어떻게 메시지를 교환할까?**  
  
Client에서는 communication을 시작하고, server에서는 contact를 기다리는 프로세스가 실행된다.  
  
(p2p에서는 둘다 존재한다.)  
  
---  
  
## Sockets  
  
- Process는 socket을 통해 다른 프로세스와 메시지를 주고 받는다.  
      
- socket은 process의 door라고 비유하면 좋다!  
      
    - socket을 통해 하위 layer로 전송되고  
    - transpoer layer에서 socket으로 메시지를 다시 전달해준다.  
      
    → Transport Layer로 가는 하나의 door라고 생각하면 됨.  
      
- 즉, Application Layer에서는 각 프로세스가 socket을 통해 주고받는 메시지를 어떻게 처리할건지만 처리하면 된다는 말씀.  
      
  
---  
  
### Addressing Process  
  
- 메시지를 받기 위해서는 process는 identifier가 필요하다.  
- host device에는 32-bit (즉, 4byte)의 IP 주소가 할당되어있다.  
- 그리고 각 process와 관련되어있는 port number가 이미 할당되어있다.  
    - 웹서버는 80이고  
    - 메일서버는 25이다.  
  
→ 뭐 내가 원하는 포트 아무데다가 열 수는 있는데, 명시를 해줘야한다. 그래서 시프 수업에서 도커에 2222 이런거 서로 겹치면 안되려고 이상하게 한 거다.  
  
우리가 친구의 집을 찾을 때는 ‘아파트 주소’와 ‘동호수’를 알아야한다.  
  
→ 패킷을 친구에게 보낼 때는 ‘IP address’와 ‘port number’를 알아야한다.  
  
---  
  
### Application Layer가 정의하는 것  
  
(1) 메시지가 어떤 타입인지  
  
- Request  
- Response  
  
(2) 메시지의 문법  
  
- 어떤 필드가 있는지?  
  
<aside> 📖  
  
Message syntax가 있다는게 무슨 뜻일까? → 이 메시지를 어떻게 해석해야하는지. 어떤 필드가 있고 message가 어떻게 delineate되어야하는지.  
  
</aside>  
  
(3) 메시지의 의미  
  
- 해당 필드의 정보의 의미  
  
(4) 규칙  
  
- 프로세스가 언제, 어떻게 응답을 주고받을지.  
  
→ 프로토콜과 연관있음.  
  
(a) Open protocols  
  
- defined in RFCs (Request for Comments. 즉, 누가 수정좀 해주세요~ 하고 이미 올려져있다,)  
- 서로다른 프로그램이 잘 운용될 수 있어야함. (interoperability. 상호운용성)  
- HTTP, SMTP(email) 등  
  
(b) Proprietary Protocols  
  
- Skype, Zoom  
    - 이 경우 HTTP 등이 아니라 자신들만의 암호화된 프로토콜을 이용한다.  
    - 즉, 이 경우 패킷을 탈취해도 복호화 및 이용이 불가능하다.  
  
---  
  
그렇다면 transport layer에서 application이 원하는 것은 무엇일까?  
  
1. **Data Integrity**  
  
- Some webs require 100% reliable data transfer.  
  
ex) Web server. File transfer  
  
- 어떤 app들은 (audio 등) loss가 좀 발생해도 괜찮다.  
  
1. Timing  
  
- 어떤 앱들은 delay가 너무 심하게 나면 안된다. (telephony, interactive games)  
- 특정 시간 내에 모든 bits 전송을 보장해야함.  
  
1. Throughput  
  
- 어떤 앱들은 최소한의 throughput이 ‘effective’해야한다.  
    - multimedia  
- 한편, 주어진 throughput을 최대한 활용하는 방안도 있다.  
    - elastic app  
  
다음은 각 애플리케이션 별 requirements이다.  
  
|Application|Data loss|Timing|Throughput|  
|---|---|---|---|  
|File transfer|No loss|ok|elastic|  
|E-mail|No loss|ok|elastic|  
|Audio, Video|loss tolerant|should few secs|audio와 video의 bandwidth가 정해져있음|  
|Real-time Video|loss tolerant|should 100ms|이하 동문|  
|Interactive games|loss tolerant|should 100ms|few kbs up|  
  
### +FEC(Forward Error Correction)  
  
data intergrity를 지키기 위한 한 방법.  
  
이 방식은 detection만 하는 것과 correction하는 방식으로 나뉜다.  
  
Detection할 때에는 channel coding을 이용한다.  
  
Redundancy information을 넣어서, 이것이 변형되었다면 전송 과정에서 오류가 있었음을 아는 것이다.  
  
XOR 같은 값을 마지막에 하나 넣으면, 전체 데이터 값이 변했는지 확인하기 쉽다. (parity)  
  
[에러 제어를 위한 채널 코딩(Channel Coding) 방식, 인터리빙](https://peim.tistory.com/23)  
  
Correction에는 추가적인 값들을 주어서 하나정도는 없어져도 괜찮게 하는 것이다.  
  
→ 그런데 이렇게 하면, data 양이 많아져서 throughput, bandwidth waste가 커진다.  
  
적당한 비율을 통해 복호화하는 것이 좋을 것이다.  
  
[FEC](https://www.ktword.co.kr/test/view/view.php?no=693)  
  
<aside> 📖  
  
FEC에서 detection 방식과 correction 방식을 잘 공부하는게 좋을 것 같다.  
  
</aside>  
  
---  
  
## Securing TCP  
  
애플리케이션 레이어에서 필요한 또 하나가 있으니 바로 security이다.  
  
### TCP, UDP  
  
- encryption되어있지 않음  
- internet에 cleartext로 패스워드들이 전달됨 (ㄷㄷ)  
  
### SSL(Secure Sockets Layer), TLS(Transport Layer Security)  
  
- TCP 연결을 encrypted되도록 함  
- data integrity를 보장  
- end-point authentication  
  
→ SSL, TLS는 app에서 돌아가는 라이브러리.  
  
(app layer에 있는건 아니고 그 사이에 독립적인 계층을 만든다. → App은 TCP인줄 알고, TransportLayer는 App인줄 안다.)  
  
Transport layer와 ‘talk’함.  
  
→ socket으로 cleartext가 가지만, 인터넷에서는 encrypted됨  
  
---  
  
### App performace: Time to transfer object  
  
위 그림은 사람들이 인식한 latency를 실제 propagation delay에 따라 나타낸 것이다.  
  
일반적으로 propagation delay가 늘어날수록 latency가 늘어날 것이라고 예측한다.  
  
보통 latency는 (size / data rate) + propagation delay로 느껴진다.  
  
위 그래프에서 size가 커질수록 propagation delay에 의한 latency 증가가 완만해진 것을 확인할 수 있다.  
  
따라서, 사람들은 size가 커질수록 propagation delay의 영향으 줄어들고, throughput이 중요해짐을 아라 수 있다.  
  
한편, 파일 사이즈가 작은 경우에는 data center등을 옮겨서 propagation time을 줄이는 것이 중요하다.  
  
---  
  
## Bandwidth-Delay Product  
  
> 1MB의 파일을 1Gb/s의 bandwidth를 가지는 link로 전송했다. RTT는 200ms이다.  
  
- Throughput은 얼마인가?  
  
→ (전체 파일 크기 ) / (총 걸린 시간)  
  
= 8MB / (transfer time) = ??  
  
- Transfer time은 얼마인가?  
  
→ (size / bandwidth) + **RTT**  
  
= (8Mb / 1000Mb/s ) + 0.2s  
  
= 0.208s  
  
RTT를 더하는 이유?  
  
→ Request + first byte delay  
  
파일 전송 시작 시 서버에게 전송을 요청하고 (0.1s)  
  
다시 first byte가 돌아오면서 acknowledgement를 해줘야한다 (0.1s)  
  
### Throughput이 원하는 만큼 안나오네?  
  
- file 크기가 너무 작아서  
- RTT가 너무 커서  
  
→ 실제로 값을 대입해서 식을 정리하면  
  
$$ \frac{1}{\left( \frac{\text{RTT}}{\text{size}} \right) + \left( \frac{1}{\text{bandwidth}} \right)} $$  
  
이다. 즉, RTT가 size에 비해 너무 큰 경우. 그 비율이 bandwidth에 비해 너무 큰 경우 throughput이 제대로 안나오게 된다.  
  
### Bandwidth-Delay Product  
  
BDP: 수신자가 무언가를 받기전에 전송자가 보낼 수 있는 최대 크기.  
  
(network pipe를 가득채울 파일 크기)  
  
즉,  
  
- 파일이 크다: Bandwidth 낭비가 적다 → throughput이 높다  
- 파일이 작다: queue 처리시간이 작다 → intensity가 높다  
  
---  
  
### Utility  
  
application은 유틸성도 중요하게 여긴다.  
  
- 어떤 앱들은 network의 모든것을 이용할 수 없다.  
- constant bit-rate audio는 특정 bandwidth 이상이면 장떙이다.  
  
대부분의 file transfer는 bandwidth가 높아질수록 좋지만, 특정 구간을 지나면 증가가 둔화된다. 그정도로 큰 파일을 전송할 일이 많이 없기 때문이다.  
  
---  
  
### Burstiness  
  
- 대부분의 앱들은 ‘bursty’하다.  
    - 필요한 bandwidth가 varies하기 때문이다.  
- 즉, 이렇게 bursty한 지점과 원인을 설명하고 분석하는 것이 중요하다.  
    - token buckets  
        - 토큰을 일정한 rate로 넣어서 authenticated된 애들만 보내기  
    - leaky buckets  
        - 패킷들을 한 버킷에 모아서 constant한 비율로만 내보내기 (overflow 가능)  
    - queueing theory  
  
[Token Bucket vs Leaky Bucket](https://medium.com/@apurvaagrawal_95485/token-bucket-vs-leaky-bucket-1c25b388436c)  
  
ex) Google search engine  
  
Frontend가 검색엔지에 요청을 보내면 모든 Backend 서버가 동시에 응답을 준다. 이 경우 network가 쓰는 bandwidth가 한번에 몰리고, 프론트엔드에서 packet loss가 발생한다.  
  
→ 해결법  
  
- bandwidth를 divide하여 각 응답을 slowdown 시킨다.  
- load balance  
  
---  
  
### Jitter  
  
- variance of end-to-end latency (or RTT)  
- 받은 패킷을 재생하기 위해 얼마나 기다릴 것인가?  
    - 너무 짧으면: packet이 너무 늦게 도착해서 audio loss  
    - 너무 길면: 대화라고 볼 수가 없음 ㅋ (150ms)  
  
ex)  
  
Youtube: packet이 도착하는 빈도가 fluctuate하는데 이에 맞춰서 buffering time을 조절한다.  
  
Game streaming: 빈도에 맞추어 quality를 변경한다.  
  
---  
  
### Loss  
  
네트워크는 패킷을 잃어버리기도 합니다.  
  
- Packet Loss rate  
- Bit-error rate  
  
이런 Loss와 error는 detected되어야합니다.  
  
- Codes, (channel coding)  
- checksums,  
- sequence numbers  
  
그리고 corrected되어야합니다.  
  
- Error correction  
- Retransmission  
  
[Cisco Transceiver Modules - Understanding FEC and Its Implementation in Cisco Optics](https://www.cisco.com/c/en/us/products/collateral/interfaces-modules/transceiver-modules/implementation-optics-wp.html)  
  
Latency를 줄이려면…  
  
- encoding rate 줄이기 (클수록 보내는 파일이 고화질이고, 초당 보내는 데이터 수 증가)  
- forwarding을 잘하기 (transmission delay때문)  
- error correction (너무 많이 하면 overhead 발생 및 retransmisson 걸림)  
  
---  
  
## Internet Transport protocols  
  
(1) TCP  
  
- reliable transport  
- flow control - sender does not overwhelm receiver  
- congestion control - throttle sender  
- connection oriented - setup required between client-server  
  
(2) UDP  
  
- unreliable data transfer
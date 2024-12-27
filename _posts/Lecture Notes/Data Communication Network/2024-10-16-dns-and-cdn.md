---  
tags:  
  - network  
  - application-layer  
  - DNS  
  - CDN  
share: "true"  
github_title: 2024-10-16-dns-and-cdn  
title: 6. DNS and CDN  
date: 2024-10-16  
categories:  
  - Lecture Notes  
  - Data Communication Network  
---  
# DNS: Domain Name System  
  
Why?  
  
- hard to remember IP address  
- can redirect to faster server  
  
DNS는 Distributed database이며, 하나의 큰 서버가 존재하지 않는다.  
  
또, DNS는 IP address를 다루는 척하지만 사실 application layer 위에서 돌아간다. 이는 인터넷이 다 만들어지고 나중에 추가된 개념이기 떄문이다.  
  
DNS서비스는 과연 무엇을 하는 것일까  
  
- hostname → IP address translate  
- host aliasing  
- load balance (여러 개의 웹 서버를 하나의 주소로 관리하여 load balance)  
    - ex) [www.google.com](http://www.google.com) → 실제 구글 웹 서버는 여러개가 있다.  
          
        - [www1.google.com](http://www1.google.com), [www2.google.com](http://www2.google.com) …  
          
        이렇게 많은 서버들 중, appropriate server로 redirect한다.  
          
  
### Why not centralize?  
  
- single point of Failure  
- traffic volume  
- distant centralized DB  
- maintenance  
  
---  
  
## DNS는 distributed, hierarchical database이다.  
  
(1) Root DNS server  
  
전세계적 규모의 DNS  
  
(2) TLD DNS server  
  
top level domain server로, kr, uk, com 등을 관리  
  
(3) Authoriative server  
  
[amazon.com](http://amazon.com) 등 특정 회사나 조직의 own-DNS server  
  
**Why?**  
  
→ there are many servers for company (web, mail)  
  
→ IP ↔ name mapping을 하고 싶지만 보안 이슈로 몇개는 mapping 하고 싶지 않음.  
  
즉, IP address를 root domain등에 다 등록하기 보다는 own DNS server를 관리하자는 아이디어  
  
즉, authoritative server는 모든 IP 정보르 알고 있되, 위쪽 hierarchy에 선택적으로 mapping을 propagate한다.  
  
---  
  
## Local DNS name servers  
  
→ 기본적으로 cache 역할  
  
(1) Iterated query  
  
- 먼저 local DNS에게 물어본다.  
- local DNS는 먼저 root DNS에 물어본다.  
    - 없으면 TLD  
    - 또 없으면 authoritative.  
- ‘나한테 없는데 여기 가서 물어봐’라는 마인드.  
  
(2) recursive query  
  
- 먼저 local DNS에게 물어보면,  
    - root → TLD → auth 순으로 요청을 보내고, 다시 recursive하게 돌아온다.  
  
## Caching, Updating records  
  
- 어떤 name server가 mapping을 learn했다면, mapping을 cache한다.  
- 대부분의 TLD는 local dns에 캐시되어있기 때문에 root DNS로 가는 경우는 적다.  
- cached entries는 out-dated될 수 있다.  
    - 즉, 한번 바꾼다고 해서 전세계로 바로 propagate할 수는 없다.  
  
---  
  
## DNS records  
  
DNS record format: (RR)  
  
`(name, value, type, ttl)`  
  
(1) type=A  
  
- name is a hostname  
- value is an IP address  
  
(2) type=NS  
  
- name is domain (ex, [amazon.com](http://amazon.com))  
- value is hostname of authoritative name server for this domain  
  
(3) type=CNAME  
  
- name is alias name for some canonical (real name).  
- value is canonical name  
    - ex) [www.ibm.com](http://www.ibm.com) [servereast.backup2.ibm.com](http://servereast.backup2.ibm.com)  
  
(4) type=MX  
  
- value is name of mail server associated with name  
  
---  
  
### DNS Protocols  
  
DNS도 결국 서버 통신이라 프로토콜이 필요하다.  
  
- query and reply message, both with same format  
  
header -  
  
- identification: 16 bit query  
- flag - query or reply, recursion, authoritative 여부 등등  
  
body -  
  
- name, type field  
- records from auth server  
  
---  
  
### Inserting records!  
  
우리가 실제로 DNS record를 입력할 때 어떤 방식으로 이루어지는지 확인하자.  
  
- 모두싸인이라는 스타트업을 만들었다.  
- modusign.com이라는 이름을 DNS registrar에 등록한다.  
- 이름([modusign.co.kr](http://modusign.co.kr) 등)과 IP addresses 들을 넘겨준다.  
    - ([modusign.co.kr](http://modusign.co.kr), [cdn.modusign.co.kr](http://cdn.modusign.co.kr) NS)  
    - ([cdn.modusign.co.kr](http://cdn.modusign.co.kr), 121.121.121.121, A)  
  
---  
  
### Attacking DNS  
  
(1) DDos Attacks  
  
- bombard root servers  
    - root server 겁내 튼튼해서 끄떡없음  
- bombard TLD server  
  
(2) Redirect Attacks  
  
- Man in middle  
    - query를 intercept하기  
- DNS poisoning  
    - 이상한 응답을 DNS에게 넘겨줘서 해당 값을 caching하게 하기.  
    - 이러면 은행 사이트 리다이렉트 가능  
  
(3) Exploit DNS for DDos  
  
- send queries with spoofed source address: target IP  
  
다른 사람들의 요청이 모두 한 IP로 향하게 해서 DDos 공격을 한다.  
  
---  
  
## Video streaming and CDNs  
  
이거 용량이랑 요청이 미친듯이 큼. 하나에서 다 관리하면 서버 잘 죽고 그러면 전세계 서버에 영향이 간다.  
  
→ 동시에 여러명의 사람들에게 어떻게 content를 streaming할 것인가  
  
(1) 겁내 큰 mega-server를 만든다.  
  
- single point of failure  
- point of network congestion  
- long path to distant clients  
- multiple copies of video sent over outgoing link  
  
→ we cannot scale!  
  
(2) 비디오의 copy 버전을 지리적으로 떨어진 여러 곳에 분산시킨다. (CDN)  
  
- access network 여기저기에 CDN server를 push한다.  
  
Enter deep, Bring home  
  
→ ISP에 접속하여 각 end user에게 최대한 가까이 위치하거나  
  
→ ISP를 home에 넣는 것이다. ISP 액세스 대신 IXP 근처에 많이 만들어놓는다.  
  
---  
  
### CDN의 동작 과정  
  
(1) local DNS based  
  
1. 사용자는 서버에서 동영상 등 콘텐츠를 클릭하여 해당 콘텐츠의 url을 가져온다.  
2. 해당 url domain을 해석하기 위해 local dns server에 요청을 보낸다.  
3. local dns server는 일단 root DNS에게, 그리고 TLD, auth까지 요청을 보낸다.  
4. 이때 auth에서는 실제 한 서버의 주소가 아니라 CDN의 주소를 반환한다. (local dns server 위치 기반)  
5. local dns server는 이걸 다시 cdn의 auth server에서 IP 주소로 translate한다.  
6. 사용자는 실제 CDN에 저장된 콘텐츠의 주소를 받는다.  
7. HTTP로 영상을 수신 받는다.  
  
(2) Account region based (Netflix)  
  
1. 사용자는 서버에게 로그인 요청을 보낸다.  
2. 사용자는 cloud 서버에 요청을 보내 특정 비디오 파일을 받는다.  
3. 해당 값은 이미 여러 곳에 복사되어있는 CDN 서버 중 하나이다.  
4. DASH streaming!  
  
→ 그럼 DASH streaming이 뭘까?  
  
---  
  
### How Zoom streams fast without CDN?  
  
Zoom은 실시간으로 모든이를 연결하여 영상을 보낼까? → 너무 많다.  
  
Zoom은 모든 이의 영상과 음성을 하나의 server로 보낸다.  
  
그리고 다시 해당 서버에서 각 영상을 mix한 뒤, 각 사용자에게 broadcast하는 방식으로 CDN 없이 빠른 비디오 스트리밍을 이뤄냈다.  
  
---  
  
## Video Streaming  
  
- video → 겁나게 큰 파일.  
  
즉, codec을 통해 크기를 줄여서 통신을 해야한다.  
  
(1) spatial  
  
- 같은 색의 ‘purple’들이 연결되어있으면, 하나하나 값을 저장하지 않고 색과 개수만 넣기.  
- 또는 FFT를 이용하여 높은 주파수를 제거하고, detail을 희생하여 압축하기  
  
(2) temporal  
  
- instead of sending complete frame i+1, 변화사항만 보내기  
  
---  
  
### HDMI  
  
HDMI는 유선으로 영상(rgb 값)들을 주고 받는다.  
  
원래라면 compress → network → decompress 과정을 거쳐야 할 것이, 그냥 선으로 다 transmit 되어 버린다.  
  
만약 4k 영상이면 4,000_2,000_32bit = 32MB (per image!) → 2Gbps…!  
  
⇒ HDMI는 bandwidth를 매우매우매우 크게 만들어야한다.  
  
---  
  
## Spatial Encoding  
  
- jpeg encoder  
  
1. RGB to three layer  
2. DCT(discrete cosine transform) and make then F(u,v)  
3. Quantization (to 0 and 1). By specific mapping rule.  
4. similar pattern is observed → make them encoded to short terms  
5. zigzag scan and make them entropy coding  
6. JPEG coded data with, Header, tables(with quantization map) and data.  
  
---  
  
## Temporal Encoding  
  
1. Divide images in video to macro-blocks and sub-macro-blocks  
2. check difference of macroblocks between i and i+1 (move, rotation etc…)  
3. Remove temporal redundancy  
  
→ it takes more time to compress, but saves the space. → maybe we use neural network to detect difference faster!  
  
---  
  
## DASH  
  
Dynamic Adaptive Streaming over Http  
  
**Server**  
  
- divides video into multiple chunks  
- each chunk stored, encoded at different rates.  
- manifest files → provide URL for each chunk  
  
**Client**  
  
- measures server-client bandwidth  
- consulting manifest - request one chunk at a time  
  
**Intelligence at client!:** client determines…  
  
- when to request (for non-empty client buffer, no overflow)  
- what encoding rate: high quality when fast bandwidth available  
- where to request - close to client  
  
→ So, when bandwidth become high, the quality doesnt become high immediately because there is remaining chunk that is playing.  
  
---
---  
tags:  
  - network  
  - application-layer  
  - http  
  - web  
share: "true"  
github_title: 2024-10-08-web-and-http  
title: 5. Web and HTTP  
date: 2024-10-08  
categories:  
  - Lecture Notes  
  - Data Communication Network  
---  
# Web and HTTP  
  
- web page는 객체로 이루어져있다.  
- 각 페이지는 HTML 베이스의 파일로 이루어져있으며, 이미지, 영상 등을 reference하고 있다.  
- 각각의 객체는 URL로써 address될 수 있다.  
  
ex) [www.snu.ac.kr](http://www.snu.ac.kr) → host name  
  
/someDept/pic.gif → path name  
  
---  
  
## URI, URN and URL  
  
(1) URI  
  
- Denotes a resource of its location  
- pointer to black box that accepts request  
  
(2) URL  
  
- Denotes location of source  
  
(3) URN  
  
- Globally unique name, like an ISBN.  
  
---  
  
## HTTP  
  
Hypertext transfer protocol  
  
(1) uses TCP  
  
- client creates socket on port 80  
- server accepts it  
- HTTP exchanges by browser and Web server  
- TCP connection closed  
  
(2) HTTP is stateless  
  
- 요청을 보내면 항상 같은 응답을 한다.  
- server maintains no information of post request → complex!  
  
---  
  
### HTTP connections  
  
(1) non-persistent HTTP  
  
- one object per one TCP connect  
- can achieve stateless HTTP perfectly  
  
(2) persistent HTTP  
  
- multiple objects can be sent over a single TCP connection  
  
---  
  
### Non-persistent HTTP  
  
1. HTTP server client initiates TCP connection. - server accepts  
2. HTTP client sends request  
3. HTTP server sends response into its socket  
4. HTTP server closes TCP. connection  
  
**Response time**  
  
RTT: time for a small packet to travel from client to server  
  
HTTP response time  
  
- TCP connection + ACK response  
      
- HTTP request + HTTP response (file transmitted)  
      
- So, 2*RTT + transmission time  
      
- HTTPS라면 복호화하는 과정에서 RTT가 추가로 발생한다.  
      
- 거리가 멀수록 RTT가 증가하여 이 과정이 critical해진다.  
      
  
→ Google에서는 UDP를 쓰기 때문에 2_RTT이다. (복호화도 한번에 하니 사실상 1_RTT)  
  
---  
  
## HTTP 1.1, 2.0  
  
- 1.1 supports persistent http connection  
- 2.0 supports HTTP multiplexing → parallel request  
    - Server limits the number of transaction speed per user, so no 1/n bandwidth!  
  
---  
  
## HTTP Server Architecture  
  
### Single-threaded web server  
  
socket - connection - create request - HTTP response…  
  
→ 하나의 요청을 수행하는 동안 request를 받지 못한다.  
  
### Multi-thread Web server  
  
setup socket - accept connect - struct request - make thread → waits…  
  
In thread, send HTTP response and delete struct. exit thread.  
  
→ CPU clock에 따라 가기때문에 그렇게 빠르지는 않음. 요즘은 멀티 프로세서가 있다.  
  
### Threadpool web server  
  
socker - accept connection - create request struct → add to linked list of requests  
  
그러면 계속 돌아가고 있는 고정된 thread pool에서 하나씩 받아서 처리함.  
  
→ thread를 미리 만들어놓기 때문에 thread 만드는 비용(시간)이 적게 든다.  
  
→ Memory space allocation에 오래걸리기 때문. mapping address  
  
---  
  
## HTTP request message  
  
- each line has 32-bit  
    - request line (method, URL, version)  
    - header line  
    - entity body (for request, upload, post)  
  
### Uploading form input  
  
(1) Post method  
  
- includes in entity body and POST  
  
(2) URL method  
  
- includes in URL field of request line and GET method  
  
---  
  
### Method Types  
  
HTTP 1.0  
  
- GET  
- POST  
- HEAD (ask server to leave requested object out of response)  
    - GET과 동일하나, 헤더정보만  
  
HTTP 1.1  
  
- - PUT  
- - DELETE  
  
---  
  
### Response code  
  
(1) 200 OK  
  
(2) 301 Moved Permanently - requested object moved Location :  
  
(3) 400 Bad request. - Not understood by server  
  
(4) 404 Not found - Not found on the serber  
  
(5) 505 HTTP version not supported  
  
---  
  
## Cookies  
  
“proof that I already did this before:  
  
1. cookie header line of HTTP response message  
2. cookie header line in HTTP request message  
3. cookie file kept on user’s host and managed by server  
4. backend database at web site  
  
Can be used for  
  
- Authorization  
- shopping carts  
- recommendations  
- user session state  
  
How to keep ‘state’…  
  
- Protocol endpoints: maintain state at sender/receiver over multiple transactions.  
- 쿠키는 상태를 가지는 http 메시지이다.  
  
---  
  
## Web Caches  
  
To satisfy client request without involving origin server.  
  
- 일단 proxy server에 요청을 한다.  
    - cache되어있으면 그거 반환  
    - 없다면 그제야 origin server 요청  
  
**Why?**  
  
- reduce response time for client request  
- reduce traffic on access link  
- Internet dense with caches  
    - poor content provider가 빠르게 content를 전파할 수 있게 한다. → ???  
  
<aside> 📖  
  
뭔소리야  
  
</aside>  
  
외국에 있는 origin servers를 생각해보자.  
  
태평양 access link rate가 엄청 높아질 것이다.  
  
태평양 광통신 장비를 늘려? 그것은 안된다. 비싸니까.  
  
cache를 쓰면 싸게 해결 가능!  
  
어떻게 측정하는가.  
  
→ cache hit rate를 가정하자. 0.4가정.  
  
즉, access link는 0.6 * 1.50 = 0.9Mbps의 사용량을 갖게 되고  
  
access link의 사용률은 0.9 / 1.54 = 58%임.  
  
총 delay는 60% * (2.01s) + 40% * (less than ms) = 1.2초 정도이다.  
  
짱 빠르고 싸다!  
  
### Conditional GET with web cache  
  
- cache가 최신 상태면 굳이 object를 주지 않아도 된다.  
  
---  
  
# P2P  
  
- no always-on server  
- peers are immediately connected and directly change IP address  
  
## How long does it takes? (in N clients)  
  
- Server - client  
  
파일을 sequentially하게 올려야해서  
  
D > max{NFus, F / dmin}  
  
- P2P  
  
chunk 단위로 올리고 뿌리기 떄문에  
  
D > max { F_us, F/dmin, N_F(us+Sum u)}  
  
---  
  
## Bit torrent  
  
- file dividied in to chunks and peer shares them  
  
처음 들어온 사람은 file chunk가 없어서 tracker가 랜덤으로 뺏어서 줌  
  
- file chunk를 다운로드시에 다운로더는 파일 청크를 업로드함.  
- 즉, 한번 파일 받으면 이기적으로 나가거나, 자비롭게 네트워크에 있을 수 있음  
  
청크를 요청할 떄  
  
- 사용자는 정기적으로 다른 peer에서 청크가 있는지 물어봄  
- 사용자는 자기가 없는 청크 중에서 제일 rare한 청크를 항상 가ㅏ져온다.  
  
청크를 보낼 때 (tit for tat)  
  
- 가장 data rate가 높은 4명에게 청크를 보낸다.  
    - 다른 사람들은 choke당한거임 껄껄  
    - 10초마다 탑4 바뀜  
- 30초마다 peer 중, 랜덤 1명에게 청크 전달  
  
만약 둘 사이의 연결이 강하다면, 계속 optimistically unchoke를 할 것이고,  
  
결국 둘은 rich해진다.
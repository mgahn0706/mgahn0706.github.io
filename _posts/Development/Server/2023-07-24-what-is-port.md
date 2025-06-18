---  
tags:  
  - port  
  - cs  
share: "true"  
github_title: 2023-07-24-what-is-port  
title: What is 'port'?  
date: 2023-07-24  
categories:  
  - Development  
  - Server  
---  
  
  
port는 항구라는 뜻입니다. 대한민국이라는 나라에 여러가지 항구가 있어 여러방향에서 들어올 수 있듯이, port는 한 IP 내에서 프로세스 구분을 위해 사용하는 번호입니다. 예를 들어, 동일한 IP 주소인 1.1.1.1 이라도, 다른 port를 이용하면 각기 다른 프로세스를 돌릴 수 있고 접근할 수 있습니다. React를 이용한 프론트엔드 서버는 `:3000` port 에서 운영하면서 백엔드 서버는 `:8080` port에서 운영할 수 있다는 의미입니다.  
  
![](/assets/img/posts/Pasted%20image%2020240718115649.png)  
  
그림 1. 서로 다른 포트 주소로 동일한 인스턴스 서버에서 각기 다른 서버로 접근하는 모습  
  
하드웨어 분야에서는 아래 그림과 같이, 하드웨어에 접근할 수 있도록 하는 커넥터 부분을 포트라고 부릅니다. 네트워크의 ‘포트’와 비슷한 원리로 네이밍이 된 것으로 보입니다.  
  
포트는 0부터 65535까지 존재합니다. 우리는 각 번호마다 프로세스를 할당할 수 있습니다. 여기서 우리는 특정 번호에는 이런 프로세스(서버)를 사용하겠다라는 약속을 했습니다.  
  
|Port|Service|  
|---|---|  
|20|ftp|  
|23|telnet|  
|67|bootps|  
|67|bootpc|  
|80|http|  
|443|https|  
  
http는 포트 80에 할당되어있군요.  
  
이러한 port는 IP 주소 뒤에 붙여서 URL로 표현할 수 있습니다. ex) `localhost:3000`, `snu.ac.kr:80`  
  
이때, 자주 사용되고 있는 http, https의 경우에는 뒤의 Port 번호를 생략해도 들어갈 수 있다고 합니다. `https://snu.ac.kr:443` 으로 접속하면 다른 번호와는 달리, 모두싸인 랜딩페이지로 잘 접속되는 것을 확인할 수 있습니다. 80과 443를 제외한 다른 숫자를 입력하면 접속할 수 없습니다.  
  
참고자료  
  
---  
  
[https://ittrue.tistory.com/185](https://ittrue.tistory.com/185)  
  
[https://en.wikipedia.org/wiki/List_of_TCP_and_UDP_port_numbers](https://en.wikipedia.org/wiki/List_of_TCP_and_UDP_port_numbers)  
  
[https://www.iana.org/assignments/service-names-port-numbers/service-names-port-numbers.xhtml](https://www.iana.org/assignments/service-names-port-numbers/service-names-port-numbers.xhtml)
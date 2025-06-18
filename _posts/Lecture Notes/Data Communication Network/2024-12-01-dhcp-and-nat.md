---  
tags:  
  - network  
  - network-layer  
  - DHCP  
share: "true"  
github_title: 2024-12-01-dhcp-and-nat  
title: 13. DHCP and NAT  
date: 2024-12-01  
categories:  
  - Lecture Notes  
  - Data Communication Network  
---  
Network layer has…  
  
- Routing protocols (path find)  
- IP Protocol (addressing)  
- ICMP protocol (to error report and router signal)  
  
---  
  
## IP datagram format  
  
Note: There is no port number, it is in transport layer  
  
Remark: `TTL (time to live)`  
  
→ maximum number for hop count. We should set ttl for a large number when we connect for the first time, but adjust it when successfully communicated. TTL will prevent the packet goes infinite loop.  
  
We need 40 byte(20 of IP, 20 of TCP) of overhead to attach header  
  
---  
  
## Fragmentation  
  
Network link has maximum transfer size  
  
→ large IP datagrams fragmented and reassembled in final destination  
  
When we fragment the datagram, we should add header so 40 bytes of size should be considered.  
  
---  
  
## IP addressing  
  
32-bit identifier for host  
  
ex) 223.0.1.1 = 11011111 . 00000000 . 00000001 . 00000001  
  
Router는 IP 데이터그램을 받으면 각 subnet을 대상으로 routing table을 이용해 적절한 subnet에 전달한다.  
  
subnet에는 여러가지 host가 있지만, 이는 무시한다. 즉, Router는 IP 주소를 계산하는 routing table이 있는 L3 수준의 network 장치이다.  
  
한편, 이렇게 subnet으로 전달된 데이터는 Ethernet switch나 WiFi base station으로 오게 되는데, 이는 L2 수준이다.  
  
---  
  
## Subnets  
  
ip 주소는 subnet part와 host part로 나뉜다. 몇 개의 호스트를 하나로 묶어주는 subnet이 있고, 그 안에 위계가 있는 것이다.  
  
subnet은 같은 subnet part를 가지는 host들의 인터페이스를 의미한다.  
  
같은 subnet끼리는 router를 intervene 하지 않고 물리적으로 도달할 수 있다.  
  
subnet part가 어디까지인지를 나타내기 위해 IP 주소를  
  
`223.1.3.0 / 24` 와 같이 나타낸다. 여기서 24가 subnet part의 길이로 앞에서 24bit이 subnet이라는 의미이다. 이를 CIDR (Classless InterDomain Routing)이라고 한다.  
  
---  
  
## CIDR  
  
`a.b.c.d/x` 로 나타내어 라우팅하는 구조.  
  
x는 subnet의 비트 수를 의미한다.  
  
일반적으로 한국은 Ip 주소의 크기가 32비트이므로 x=24이면 8개의 비트가 host의 주소를 나타내는데에 할당되어있다고 생각할 수 있다. 즉, 해당 subnet에는 2^8 개만큼의 host가 최대로 있을 수 있다.  
  
이렇게 subnet의 크기에 따라 class A ~ C subnet이 달라지기도 한다.  
  
---  
  
### How host get IP address?  
  
- host can get IP address by hard-coding  
    - Control panel or config file.  
  
→ Can be useful in distributed system or AI factory.  
  
- or get IP address dynamically!  
    - by DHCP, allocate IP address by server  
  
---  
  
## DHCP  
  
DHCP server is on Wifi access point usually.  
  
By using DHCP  
  
- can renew its lease on address in use  
- allow reuse of address  
- support for mobile users  
  
Process  
  
- Client broadcasts to server (discover) [optional]  
    - `src: 0.0.0.0 dest 255.255.255.255`  
- DHCP offer [optional]  
    - `dest 255.255.255.255, your_ip_address_is: 1223.1.2.4`  
- DHCP request  
    - I will use that address!  
- DHCP ACK  
    - ok.  
  
<aside> 📖  
  
Why discovering and offer is optional? → If client already knows DHCP server address, it is not necessary  
  
</aside>  
  
---  
  
### DHCP is more than IP address..  
  
DHCP can return more than ip address like  
  
- address of first hop router  
- name and IP address of DNS server  
- network mask  
  
So, if you access [www.google.com](https://www.google.com) at coffee shop and coffee shop uses KT wifi access point with DHCP server, it will use DNS server of KT(belonging to ISP)  
  
→ Different DNS means it uses different server. So, it can resolve server blocking  
  
<aside> 📖  
  
Why you might get different server if you move the building?  
  
→ DHCP gives not only dynamic IP address, but also DNS server address and name. And DHCP server is different when ISP is different. Different ISP may give different DNS server and give different IP address to same domain.  
  
</aside>  
  
---  
  
### Broadcasting in detail  
  
when we set destination to fffff…ff, it broadcasts to LAN.  
  
→ it propagates endlessly, so we should limit hop count by setting TTL  
  
---  
  
## Then How subnet get IP address?  
  
→ ISP has own its subnet block (ex. 200.23.16.0 / 20)  
  
→ gets allocated portion of its provider ISP’s address space!  
  
So, subnet can be hierarchied  
  
---  
  
### Hierarchical addressing  
  
allows efficient advertisement of routing info.!  
  
→ Internet is well-classified. So, Seoul and Daejeon should have different IP address.  
  
However, Internet is not strict with location → Ip address can be different by ISP.  
  
---  
  
### Then, How ISP get block of address?  
  
→ ICANN 이라는 특정 회사가 관리하고 있다.  
  
- allocate adresses  
- manage DNS  
- assigns domain names  
- resolve disputes  
  
---  
  
## NAT: Network address translation  
  
`192.2.xxx` 같은 IP주소를 다 하나하나 매칭하면 너무 많다.  
  
→ local에서는 virtual ip address를 쓰고, router 밖으로 나갈때는 하나만 쓰자.  
  
→ 외부 인터넷에서 보았을 때는 local network는 하나의 IP 주소를 쓰는 것처럼 보인다.  
  
장점  
  
- ISP는 주소의 range를 저장하지 않고 각 디바이스마다 하나만 저장하면 된다.  
- local device의 IP 주소를 재할당할 때 외부 인터넷에 알리지 않아도 된다.  
- ISP를 바꿀 때 디바이스 자체의 IP 주소를 바꾸지 않아도 된다.  
- 외부 세계에서 내부 디바이스의 주소를 명시적으로 볼 수 없다. (나름의 방화벽 역할)  
  
NAT router must:  
  
- Replace outgoing datagrams to NAT IP address, new port  
- remember every translation table  
- incoming datagrams should be mapped in translation table  
  
NAT has  
  
- 16-bit port number field. 2^16 ~ 60,000 simultaneous connections!  
- No need to have field in IPv6  
  
NAT is controversial  
  
- Router should only process up to L3.  
- address shortage should be solved by IPv6  
- violates end-to-end argument  
- What client should do when it wants to connect behind NAT?  
    - config specific address & port number to NAT to redirect a specific host  
    - Relay (External client)  
  
---  
  
## IPv6  
  
32-bit is too small!  
  
→ fixed header size of 40 byte (note that it was 20 byte in former version)  
  
→ But not allowed to fragment!  
  
[How do you compare and contrast IPv6 fragmentation and reassembly with IPv4 fragmentation and reassembly?](https://www.linkedin.com/advice/1/how-do-you-compare-contrast-ipv6-fragmentation-reassembly)  
  
We can reduce load of router. Reduce overhead.  
  
→ If packet is too big, the source and destination should fragment it, not in router.  
  
---  
  
we talked about destination-based forwarding.  
  
## Generalized Forwarding and SDN  
  
There is a centralized control plane. and flow table has been distributed to each router.  
  
→ Every routers are monitored and gives to centralized server  
  
Useful in AI Factory.  
  
---  
  
### Open flow data plane  
  
→ flow is defined by header fields, and there is pattern. Router perfomrs action which is matched in pattern.  
  
Example)  
  
src=1.2._._. , dest: 1.2.3.*. → Drop the packet, forward with, or report to controller  
  
→ We can program router behavior and program the destination of packet in data center.  
  
→ We can check suspicious packet with specific source. (like North Korea 🙂)
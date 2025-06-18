---  
tags:  
  - network  
  - transport-layer  
  - tcp  
  - congestion-control  
share: "true"  
github_title: 2024-11-17-congestion-control  
title: 11. Congestion Control  
date: 2024-11-17  
categories:  
  - Lecture Notes  
  - Data Communication Network  
---  
## Congestion  
  
“Too many sources sending too much data too fast for network”  
  
- different from flow control  
    - Flow control is to throttle sender’s speed to prevent overflow in the receiver buffer. Adjusting sending data rate to rhythm of ACK. (ACK clocking)  
- 현상  
    - Packet loss (router buffer overflow)  
    - Long latency (Queueing in rouer buffer)  
  
→ There exists convergence point.  
  
---  
  
### Congestion Scenario #1  
  
Two senders, two receivers, infinite buffer  
  
if output link capacity is R, Each flow can share link with R/2.  
  
delay would be infinite when input near to R/2.  
  
---  
  
### Congestion Scenario #2  
  
same with #1, but finite buffer → retransmission.  
  
Now packet can be lost, so retransmission happens.  
  
The ratio of “Effective data” decreases. We do not consider ‘retransmitted data’ in throughput,  
  
throughput declines if input is closed to R/2.  
  
→ Congestion cause costs that  
  
- More work for given goodput.  
- Unneeded retransmissions.  
  
---  
  
### Congestion Scenario #3  
  
multiple-hops.  
  
→ When packet dropped, the capacity used for that packet is wasted.  
  
---  
  
## Congestion Collapse!  
  
If we do not control congestion, the network will run into congestion control.  
  
→ No useful throughput. (deadlock mode)  
  
---  
  
### TCP history  
  
(1) TCP Tahoe  
  
- Fast retransmit dea,  
  
(2) TCP Reno  
  
- Fast recovery  
  
(3) TCP New Reno  
  
- Retransmission during the fast-recovery  
  
---  
  
## TCP congestion Control  
  
### AIMD: Additive increase, Multiplicative decrease  
  
- Sender increases window size slowly(probing for usable bandwidth), if packet drops, decreases to half.  
  
→ Increase cwnd by MSS every RTT.  
  
→ Decrease cwnd in half after loss.  
  
Used in Reno TCP.  
  
Sending rate is cwnd / RTT.  
  
Data rate and RTT is not relavent, but in TCP, due to determining cwnd, it has some relation.  
  
We can control “in-flight” packet by adjusting (congestion) window size!  
  
---  
  
이전에 살펴봤던 ACK clokcing도 congestion 방지를 위함.  
  
---  
  
## TCP slow start  
  
initially, cwnd is 1MSS.  
  
→ double the cwnd every RTT.  
  
→ increases until loss event OR exceeds ssthresh.  
  
This is slow, although it grows exponentially, the size of appropriate window size is relatively large.  
  
---  
  
### Reacting to Loss!  
  
- Loss detected by timeout → cwnd set to 1 MSS. grows exponentially until threshold.  
      
- Loss detected by duplicated ACKs (fast retransmission) : TCP RENO  
      
    - cwnd cut in a half, grows linearly  
      
    In TCP Tahoe, always set cwnd to 1 MSS.  
      
  
---  
  
[[네트워크] TCP Congestion Control: (1) 기본 동작 - 1편](https://ai-com.tistory.com/entry/%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC-TCP-Congestion-Control-1-%EA%B8%B0%EB%B3%B8-%EC%9B%90%EB%A6%AC)  
  
## TCP Congestion Avoidance  
  
- One each ack, increase cwnd by 1/cwnd packets, so it grows linearly after threshold.  
- Threshold is half of previous window size, when packet loss detected.  
  
→ But, it becomes so slow when there was unlucky loss.  
  
---  
  
## Fast retransmit  
  
→ when multiple dups come back.  
  
→ ACK clocking still there, if only one packet lost. It means packet transmission is still working.  
  
We need FAST RECOVERY!  
  
---  
  
## Fast recovery  
  
- `cwnd = ssthresh + (dupacks)`  
- lasts until non-duplication ACK is received.  
  
→ Packet drop can occur not only congestion, but also bit-flipping or wireless environment.  
  
So, keep collecting duplicated ACKs while retransmitting missing segment.  
  
Then, reduce size to ssthresh again, and start AIMD again.  
  
---  
  
### TCP throughput  
  
- What is avg throughput as a function of window size and RTT?  
  
- ignoring slow start and no data,  
- Avg thrpt = (3/4) * (W/RTT)  
- It seems to be waste of utilization, however W / RTT is bigger than 1; due to queue size  
  
TCP over long, fat pipes. - Throughput is 1.22*MSS / (RTT sqrt(L)) where L is probability of segment loss.  
  
---  
  
## TCP Cubic  
  
cwnd = C(t-K)^3 + Wmax  
  
삼차함수 형식으로 증가하는 식.  
  
packet loss가 일어나면, reno와 동일하게 절반 + dupes packet number로 떨어지지만, 예상 max값에 가까워질 때까지 빠르게 올라갔다가, congestion 예상 지점에서 천천히 늘어나고 이내 max값이 찾기 위해 다시 빠르게 증가한다.  
  
packet loss가 발생하는 window size가 크게 변하지 않는 상황이라면, 천천히 올라가는 것보다 예상 지점까지는 빠르게 올라간 뒤, 이후 천천히 탐색하는 것이 더 유리하리라는 판단인 것이다.  
  
즉, loss 이후의 상황에서 CUBIC은 더 빠르게 throughput을 enjoy할 수 있다.  
  
---  
  
## TCP fairness  
  
If K sessions share same bottleneck, each should have R/K rate.  
  
→ or maybe we should penalty multiple hop user.  
  
Luckily, TCP achieve this  
  
It converges to the ‘midpoint’ where both throughput become same.  
  
- How about in UDP?  
  
multimedia apps often do not use TCP  
  
→ do not throttled by congestion control.  
  
→ sends packet at constant rate, tolerate packet loss  
  
- Parallel TCP connection  
  
app can open multiple connections between two hosts.  
  
→ ex) web browser  
  
if already 9 links exist in capacity R,  
  
- new app asks for 1 TCP get R/10  
- new app asks for 9 TCP get R/2  
  
---  
  
## NUM for fairness  
  
NUM: network utility maximization  
  
Maximize the sum of each utilization!  
  
→ proportional fairness는 logxs의 합이 최대가 되도록 한다.  
  
Max efficiency를 위해서는 U(xs) = xs가 되도록한다.  
  
이때, logxs값의 합이 최대가 되려면  
  
각 xs - xs* / xs_의 합이 음수가 되게 하는 xs_는 모두 솔루션이다.  
  
→ TCP Reno나 CUBIC은 RTT 기반 fairness를 만든다. RTT의 역수에 비례하도록 allocate을 해주는 것이다.  
  
---  
  
## AQM (Active Queue Management)  
  
- Marking mechanism  
- Cross-layer method  
  
### RED (Random Early Detection)  
  
- Drops incoming packets with a probability  
- Warns of congestion by dropping packets  
  
Pros:  
  
- Sources learn about congestion before router buffer is full, preventing buffer overflow and slowing down before multiple packet losses occur  
  
Cons:  
  
- We need to determine threshold and probabilty cautiously. If threshold is too low, we cannot use network resource effectivley.  
- Router need additional knowledge  
- Randomly dropped packet might increase latency, and make data rate more fluctuating  
  
### ECN (Explicit Congestion Notification)  
  
ECN bit will be set by router when congestion happens.  
  
When queue size increase, router will probably mark ECN bit, and destination host will give ACK with ECE bit. It notifies queue is large.  
  
If there are too many markings in ECE bits, source host should decrease window size.
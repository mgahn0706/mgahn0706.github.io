---  
tags:  
  - network  
  - transport-layer  
  - ARQ  
  - pipeline  
share: "true"  
github_title: 2024-11-14-pipelining-and-arq  
title: 9. Pipelining and ARQ  
date: 2024-11-14  
categories:  
  - Lecture Notes  
  - Data Communication Network  
---  
stop and wait로 하나씩 보내면 먼 거리 통신할 때 많이 느리다.  
  
→ We need pipelining!  
  
- GBN  
- Selective Repeat  
  
---  
  
### Let’s increase utilization  
  
기존의 stop and wait 방식은  
  
(d_t ) / (d_t + RTT) 만큼밖에 활용할 수 없기 때문에 활용도가 떨어질 수 밖에 없다.  
  
따라서, 여러개의 패킷을 연속적으로 보내는 것이 유리하다.  
  
→ n개를 Pipelining을 하면 n배만큼 활용도가 증가한다.  
  
그러다가 k * dt = dt + RTT가 되는 순간, transmission queuing이 발생한다.  
  
이렇게 util이 1이 되도록 한다면, 그 때 RTT 시간 당 보내는 데이터 양은 BDP가 된다.  
  
---  
  
## Go-back-N  
  
- k-bit seq number in header  
- Sender 측에서 window를 sliding하여 ‘unack’된 가장 작은 패킷을 관리한다.  
- 가장 seq num이 작은 패킷을 기준으로 timer를 측정하며, timeout이 발생하면 n개에 대하여 다시 요청을 보낸다.  
  
receiver 측에서는…  
  
- 그냥 성공한 패킷 중, 가장 숫자가 큰 ACK를 넘겨주면 된다.  
- 즉, 실패했다면 성공한 패킷 중 가장 큰 숫자를 보낸다.  
  
### advtg.  
  
- No need for buffering in each succeeded packets  
- Sender / Receiver need less register (only send_base, nextseqnum for sender. expectedseqnum for receiver) → low cost  
- Tolerant to ACK loss. → We can guarantee lower number ACKs has succeed if we get higher num ACK due to property of cumulative ACK.  
  
→ window size N은 BDP에 따라 달라지는 것이 효율적이기 때문에 외부적인 시스템으로 관리하는 것이 좋다.  
  
반대로 말하면, N이 너무 커져서 BDP를 violate하면 queueing 이 발생한다.  
  
---  
  
## Selective Repeat  
  
- Receiver individually acks correctly received packet.  
- sender retransmits packet for which ACK not received.  
  
→ sender / receiver might have different window base  
  
---  
  
### Selective Repeat: Dilemma  
  
If maximum of sequence number is not enough large for network speed, something will go very wrong.  
  
→ receiver 입장에서는 0, 1, 2를 보냈을 때 ACK들이 실패해서 다시 0, 1, 2를 보낸 것과 실제로 sequence number가 다 돌아서 0, 1, 2가 다시 돌아온 것을 구분하지 못한다.  
  
→ Duplicated data acceptance!  
  
---  
  
둘다 쓰면 괜찮지 않을까. lossy할 때는 selective, 아닐때는 cumulative.  
  
→ have to responsd two sequence number → Size of ACK become larger → more packet loss or corruption due to increased size.  
  
채널의 상황에 따라 어떻게 할지 처리하게 될 수 있다. (현재의 TCP)  
  
---  
  
Selective Repeat을 구현할 때에는 2가지 의사결정 옵션이 있다.  
  
(1) window size만큼의 in-flight packet을 허용한다.  
  
- 즉, 2가 아직 안와서 [2, 3, 4, 5] 인 경우, 5가 도착했다면 일단 6을 보내는 방식.  
- non-consecutive packet in-flight  
  
(2) conservative하게 진짜 chunk단위로 이동하기.  
  
→ It’s up to you  
  
---  
  
## Throughput Analysis  
  
- tI := transmission time to one frame  
- tp := propagation delay (one way)  
- tproc := processing time at receiver  
- ts := transmission time of ACK, NACK  
  
## Stop - and - wait  
  
- Timeout > 2*tp + tproc + ts  
  
→ straightfoward 하죠?  
  
tI가 없는 이유: one frame을 다 넣고부터 timer를 시작해도 되니까.  
  
그렇다면 max-throughput은 얼마일까.  
  
Assume)  
  
- Transmitter A sends to transmitter B  
- A always has something to send (saturated sender)  
- no loss  
  
tT(round trip time) = Tout + TI;  
  
If no error,  
  
- Max = 1 / tT (frame / second)  
  
  
이제 오류가 있는 상황을 가정하자.  
  
p := frame당 에러 발생 확률  
  
tv := 성공적으로 전달된 두 프레임의 시간차 (프레임 하나 전달에 걸리는 시간)  
  
N := 재전송 횟수  
  
E(tv) = E(tv| N = 0)*P(N=0) + E(tv|N=1)*P(N=1) * …  
  
(전체 소요시간) = (한번에 보낼 확률)*(한번 가는데 걸리는 시간) + …  
  
이때 P(n) ⇒ (1-p), p(1-p), p^2 (1-p) … ⇒ (1-p)*p^n  
  
E(tv|N=n) = (n+1)tT  
  
(0번이면 tT걸리고, 1번이면 2*tT걸리고…)  
  
즉, E(N) = n * sum of E(N = n)  
  
→ p / (1-p)  
  
---  
  
## Go-back-N 분석  
  
go-back-n은 다른 점은, 모든 시간에 frame을 넣을 수 있다는 점이다.  
  
즉, 1/tI가 에러가 없을 때 최대 throughput이다.  
  
E(tv) = tI(1-p) + p(1-p)_(tI + tT) + p^2(1-p)_(tI + 2tT);  
  
패킷 1개가 전송에 실패하면, tT를 다 거친 이후에야 해당 패킷을 다시 보낼 수 있기 때문이다.  
  
---  
  
## Selective Request 분석  
  
New assumption: Infinite reordering buffer at receiver  
  
여기서는 tv (한 프레임에서 다음 프레임으로까지 걸리는 시간)의 평균을 역수취하지 않고, 다른 방식으로 구한다.  
  
먼저 시도 횟수의 기댓값을 구한다.  
  
E(k) = 1*(1-p) + 2_p_(1-p) + 3_p^2_(1-p) + …  
  
= 1/(1-p) 멱급수 계산.  
  
Idea: 모든 transmission 중에서 retransmission을 빼면 된다.  
  
단위시간당 들어온 데이터 크기에서 retransmission으로 왔을 프레임의 기댓값을 나눠주면 된다.  
  
예를 들어, 단위 시간당 4개의 패킷이 성공하는데, 평균 재시도 횟수가 2라면, 사실상 2개가 actual transmit이라고 보는 것이다.  
  
Max throughput = (단위 시간당 프레임의 전송 개수) / (프레임 당 평균 재시도 횟수)로도 계산할 수 있다.  
  
---  
  
## 결론: 뭐가 좋은가?  
  
a = tT / tI 라 할때,  
  
Stop- and - wait: (1-p)/a  
  
Go-Back-N: (1-p)/ (1+(a-1)p))  
  
selective repeat : 1-p  
  
- a가 1에 가깝다면, (즉, RTT, tout이 충분히 작다면) 세 값 모두 같아진다. 이 말은, transmission delay dominates propagation delay.  
      
- a가 크지만, p가 optic fiber처럼 매우 작다면,  
      
    - stop and wait is bad  
    - 나머지는 비교해볼만함  
    - 1+(a-1)p 와 1 중 더 작을수록 이득임.  
        - 즉, (a-1)p가 0에 가까울수록 유리한데, 이건 한번 봐야함  
        - 이거에 대한 차이보다 다른 비용 이슈가 더 클수 있기에…  
- ap가 매우 큰 경우  
      
    - selective repeat이 성능이 제일 좋다.  
  
우리는 여러 상황을 고려해서 적절한 공학적 의사결정을 해야한다.  
  
예를 들어, nvidia graphic card같은 경우에는 a와 p가 둘다 매우 작기 때문에, simple하게 써도 된다.
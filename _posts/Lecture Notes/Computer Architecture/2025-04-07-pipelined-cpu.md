---  
tags:  
  - cpu  
  - pipeline  
share: "true"  
github_title: 2025-04-07-pipelined-cpu  
title: 7. Pipelined CPU  
date: 2025-04-07  
categories:  
  - Lecture Notes  
  - Computer Architecture  
---  
## Pipelining… is laundry.  
  
이론적으로 세탁 - 건조 - 개기 - 옷장을 하나하나 단위로 하면 한참~ 걸린다.  
  
몇개가 건조기 도는 동안 세탁기를 돌리고… 처럼 병렬로 연결하면 throughput이 4배 가까이 늘어난다.  
  
이론적으로 완벽한, 리소스 낭비가 없는 그림이 나온다.  
  
하지만, 실제로는 각 단계가 일정하지 않다.  
  
각 thorughput이 가장 긴 step에 묶이게 되는 단점이 있다.  
  
예를 들어 나머지가 아무리 빨라도, 건조기가 1시간씩 걸리면 세탁물은 1시간에 1번 나온다.  
  
이 경우 건조기를 2개 사면 해결 된다. 돈으로 해결되는 문제도 있는 것이다.  
  
---  
  
## Pipeline Idealism  
  
HW를 조금만 추가해서 throughput을 늘리자.  
  
- Repetition of identical operation  
    - 비슷한 인풋들에 대해 동일한 동작을 계속 수행해야한다.  
- Repetition of independent operation  
    - 반복되는 작업에는 의존성이 없다. (누가 더 빨리 실행해야한다가 없음.)  
- Uniformly partitionable sub-ops  
    - 동일한 latency의 세부 동작으로 분화할 수 있다. (ALU를 동시에 쓰면 안된다.) (나눗셈은 pipeline이 어려움)  
  
### Ideal Pipeline  
  
Bandwidth = n / T 이다. 이상적인 경우에는…  
  
1. 시간  
  
pipeline register가 들어가기 때문에, 이 latency를 S라 하자.  
  
$BW = {1\over T+S}$  
  
$BW_k = {1\over T / k + S}$  
  
k가 커지면 커질수록, S가 중요해지기 시작한다.  
  
1. 공간  
  
$Cost = G + L \times k$  
  
이제, 성능 대비 가격을 최소화하자.  
  
$$ C / P = {(G+Lk)\over({1\over{T/k + S}})} $$  
  
위 값이 최소가 되는 지점을 미분을 통해 찾을 수 있다.  
  
⇒ 파이프라인은 어느 순간 성능 향상이 멈춘다.  
  
<aside> 💡  
  
Pipelining을 하면 왜 성능이 오르는가?  
  
→ 병렬성이 높아진다? (X) 프로그램을 동시에 실행하는게 아님. → T/k가 짧아지기 때문이다. 이러면 frequency를 올릴 수 있다. (O)  
  
</aside>  
  
> “Pipelining의 성능 향상은 명령어를 k단계로 나눠 각 단계를 더 빠르게 실행할 수 있기 때문이며, 이로 인해 클럭 사이클 시간을 줄이고 주파수를 높일 수 있어서 결과적으로 throughput이 증가하는 것이다.”  
  
---  
  
## Now pipleline CPU!  
  
5 stage…. but why not 4, or 6?  
  
Note: 여기서부터 마이크로아키텍쳐 영역임. 원래 한 명렁어씩 실행한다는 아키텍쳐 약속이 있는데 내부적으로 깨버렸음.  
  
IF에서 나온 결과물들을 넘겨주고, ID는 다음 사이클에 그걸 받고 다시 넘겨주고… 하는 것이지.  
  
하지만, 우리는 단순 datapath뿐만 아니라, 명령어가 흘러가면서 필요한 signal들도 같이 흘러가야함. 다만, 사용되는 시점이 다르다.  
  
### Sequential Control  
  
각 control code는 (대부분) ID에서 만들어진다.  
  
따라서 이 control 신호들도 pipelining이 되어야 한다. 어떻게  
  
(1) 한번에 decode한 후 신호들만 pipelining한다.  
  
(2) instruction 만 보내고 그떄그때 decode한다.  
  
→ Which is better?  
  
> “(1)은 ID 단계에서 control을 미리 다 만들어서 pipeline으로 넘기기 때문에 빠르고 설계가 간단하지만, flush나 stall에 덜 유연하고, pipeline register가 커집니다.  
>   
> 반면 (2)는 instruction만 넘기고 각 단계에서 다시 decode해서 control을 만드는 방식이라 유연성은 높지만, decoding logic이 반복되고 복잡해질 수 있습니다.”  
  
---  
  
## Reality of Pipelining…  
  
1. 일단 매번 똑같은걸 안하고… (타입에 딸 ㅏ다름)  
2. 일단 의존적이지가 않음. (셔츠보다 바지 먼저 빨아야함.)  
    - 레지스터 a와 b를 더한 값을 주소로 쓰려면, 일단 a와 b의 계산정도는 끝나야함.  
    - 앞 명령어에서 결과가 다 나와 나갈 때 까지는 기다려야함.  
    - 의존적인 명령어가 가까울수록 파이프라인 성능 똥망  
3. 메모리가 RF Read보다 훠어어어어어얼씬 오래 걸린다.  
  
⇒ 이로 인해 더 적은 k에서 멈추게 되어있다.
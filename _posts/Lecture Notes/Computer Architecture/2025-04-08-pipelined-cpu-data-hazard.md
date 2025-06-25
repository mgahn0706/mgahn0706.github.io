---  
tags:  
  - cpu  
  - pipeline  
  - hazard  
share: "true"  
github_title: 2025-04-08-pipelined-cpu-data-hazard  
title: 8. Pipelined CPU - Data Hazard  
date: 2025-04-08  
categories:  
  - Lecture Notes  
  - Computer Architecture  
---  
이전 글에서, 파이프라이닝이 똥망하는 이유를 봤다.  
  
## Data Dependence  
  
### Data dependence  
  
r3 ← r1 + r2  
  
r4 ← MEM[r3]  
  
`Read-after-write dependency (RAW)`  
  
### Anti-dependence  
  
r3 ← r1 + r2  
  
r1 ← r4 + r5  
  
`Write-after-read dependency (WAR)`  
  
### Output-dependence  
  
r3 ← r1 + r2  
  
r3 ← r5 + r6  
  
`Write-after-Wrtie dependency (WAW)`  
  
We talk about only RAW (for now 🙂)  
  
---  
  
## Data depencency makes hazard  
  
이렇게 data dependeny가 생기면 hazard가 발생해서 기다려야한다. WB까지 기다려야하기 때문에..  
  
충분히 기다리지 않고 바로 들어오면 문제(hazard)가 생김  
  
dist(i, j) ≤ dist(X, Y) → Hazard!!  
  
(같은 레지스터를 쓰는 명령어끼리의 거리) ≤ (명령어 내 ID, WB 거리) 이면 문제가 생긴다.  
  
### RAW Hazard가 발생하는 조건  
  
(1) 앞의 명령어가 쓴 값을 내가 받아서 사용해야함.  
  
(2) 그 둘 사이이 거리가 3 (ID ~ WB)보다 같거나 작아야함  
  
2가지 조건이 만족되면 Hazard  
  
## Stall  
  
이렇게 해서 앞 명령어가 끝날때까지 3-cycle 기다리는 것을 `stall` 이라고 한다.  
  
- Hazard가 resolve될 때까지 어린 명령어를 기다리는 것  
  
1. 먼저 의존성 있는 친구와 그 뒤에 파이프라인에 따라들어온 애들을 멈추고  
2. 먼저 들어간 친구가 WB을 해서 해결되면 그 다음 사이클에 다시 시작한다.  
  
이때 해결되는 동안에는 명령어가 안들어오는 것처럼 보이는데, 이를 bubble이라고 한다.  
  
### How to stall?  
  
- Disable PC and IR Latching  
- Control should stop regWrite, MemWrite.  
  
### When to stall?  
  
- 아까 두 조건이 만족되었을 때.  
- Ib가 EX, MEM, WB 단계에 있는 Ia가 쓰는 레지스터를 쓰려고 할 때 멈춰야함.  
  
### Stall Condition  
  
- rs(IR_ID == dest_EX) : 현재 ID 단계의 명령어의 rs부분(읽으려는 부분)과 EX단계의 목적지 부분이 같고,  
- 실제로 R-type등 IR_ID가 그 레지스터를 쓰며, (우연히 맞았을 수 있어)  
- EX단계의 명령어가 실제로 update를 하려고 할떄  
  
→ 멈춰어어어어  
  
가까운 것부터 비교하는데, 가까운게 더 중요해서 우선순위가 있다.  
  
만약 ID와 EX를 비교했다면 3-cycle  
  
MEM을 비교했다면 2-cycle  
  
WB을 비교했다면 1-cycle을 기다리면 된다. (bubble)  
  
→ 어케 구현하냐 ㅋㅋ  
  
물론 이건 rs 얘기고 rt도 비교해야함.  
  
<aside> 💡  
  
EX, MEM, WB 과정은 stall 중에서도 계속 계산은 된다.  
  
</aside>  
  
### Impact of Stall on performance  
  
Ideal IPC: 1 (매 사이클마다 하나씩 뱉은게 이상적.)  
  
With stall?  
  
→ stall 날때마다 1~3 cycle 손해  
  
N개의 instruction에서 S개의 stall이 나왔다?  
  
→ $N / (N+S)$  
  
이떄, S는 RAW 가 있는 경우, 해저드 간 거리가 짧은 경우. 등이 있다.  
  
→ i0 ~ i1 이 해결되어도 i0와 i2가 또 위험이 있다면 더 기다려야한다.  
  
<aside> 💡  
  
조건문에 걸린 명령어들은, hazard가 있을수도, 없을수도 있지 않나요?  
  
→ Condition을 모르는 경우에는 다음 명령어가 들어오지 않는다고 가정합니다.  
  
</aside>  
  
어셈블리 코드가 주어졌을 때, 각 명령어 사이에 stall을 몇번 해야하는지에 대한 응용문제 풀어보기!  
  
---  
  
## Data Forwarding  
  
눈물의 hazard 줄이기 ㅠㅠ  
  
굳이 레지스터 파일까지 기다려야 함?  
  
ALU에서 나온 EX 스테이지의 연산을 레지스터에 넣어서 기다리게 하지말고, 그냥 다시 EX에 넣어서 바로바로 쓸 수 있게 한다.  
  
forwarding unit을 둬서 forwarding 가능 여부를 체크하고  
  
이를 통해 ALUSrcA에 앞에 3-cycle에서 나온 값을 포워딩해서 바로 EX에 써버릴 수 있다.  
  
Note: EX, MEM은 오케이. Register File에서 WB을 할때도 가능한가?  
  
- **레지스터 파일(Register File)** 은 보통 WB 단계에서 update돼.  
- 그런데 뒷 명령어가 이 값을 WB까지 기다리지 않고 **지금!** 읽고 싶어 함.  
- 그래서 **register 파일을 통하지 않고 바로 값을 전달해서** 1-cycle 기다리는 걸 없애자는 거.  
  
⇒ 여러개의 조건이 동시에 만족되면?  
  
“무조건 가까운 EX, MEM, WB 순.” 가장 오래 기다려야했을 것을 포워딩 해야한다.  
  
### Data Hazard Analysis with Forwarding (중요)  
  
RAW Hazard를 ‘생산’할 수 있는 친구는 R,I-type (ALU어세 produce)과 LW (MEM에서 produce)이다.  
  
그리고 각 명령어가 값을 쓰는 부분은 정해져있다. 대부분 EX, JR만 ID에서 바로 점프함.  
  
따라서 이 부분으로 forwarding하면, R-I type에서 만들어진 정보는 바로 EX로 넘어가 바로 사용할 수 있다. Jr의 경우는 ID에서 한번 기다려야 한다.  
  
즉, R-I type 관련 stall 문제를 완벽히 해결할 수 있다.  
  
한편, MEM에서 나오는 값은 EX와 한 사이클 떨어져있기 때문에, 만약 의존성 있는 두 명령어가 파이프라인에 붙어온다면, 뒤의 명령어는 한번 더 기다려야 한다.  
  
---  
  
## Load Delay Slot  
  
instruction이 load 뒤에 바로 딸려오면, 어차피 기다려야 한다.  
  
ID에서 기다릴 것이 뻔하므로, 그 시간에 다른 `독립적인` 명령어를 실행한다는 마인드이다.  
  
ex)  
  
```nasm  
addi $s1, $s2, -1  
...  
lw $t3, 0($t2)  
lw $t4, 4($t2)  
slt $t0, $t4, $t3 // still need 1-cycle.. so add slot  
  
addi $s1, $s2, -1  
...  
lw $t3, 0($t2)  
lw $t4, 4($t2)  
(delay slot for independent instruction)  
slt $t0, $t4, $t3 // still need 1-cycle.. so add slot  
  
```  
  
→ 마이크로 아키텍쳐가 외부(컴파일러)로 노출된 꼴이기 때문에 매우 안좋은 것이다. binary compatibility를 지키지 못하므로 pipelining을 안쓰는 다른 CPU에서는 돌아가지 않는다!  
  
---  
  
### Hazard Resolution  
  
(1) Static  
  
Schedule instructions at compile time (by coding, compiling)  
  
(2) Dynamic  
  
Detect hazard and adjust pipeline operation (stall, flush, forward) at runtime  
  
### Pipeline interlock  
  
- Hardware mechanisms for dynamic hazard resolution  
- detect and enforce dependences  
  
---  
  
## Superpipeline  
  
### Why not deep pipeline?  
  
성능이 그렇게 좋아지지 않는건 둘째 치고,  
  
(1) Branch penalty가 매우 커짐  
  
flush할 것만 엄청나게 많아짐…  
  
(2) Forwarding, stall, hazard 처리 미친듯이 복잡해진  
  
원래는 EX → EX, MEM → EX 정도였는데 이제는  
  
EX1 → EX5, MEM2 → … 이렇게 모든 경로에 있는걸 forwarding해야 성능이 올라갈 수 있음.  
  
그렇다고 안하면 stall 때문에 안하느니만 못하니…  
  
line이 많아지고 복잡도가 증가해  
  
(3) 무엇보다 레지스터가 많아짐  
  
pipeline register is not free.  
  
회로 크기도 커지고 파워도 많이 먹는다.  
  
(4) 명령어간 의존성 해결이 힘듬  
  
이제는 MEM→EX 등만 생각할게 아니라 MEM5 → EX1 이렇게 생각해야함.  
  
이러면 클럭 주기는 짧아졌어도, stall 시에 기다려야하는 사이클이 늘어나기 때문에 어차피 stall로 인한 대기 시간은 같음.  
  
### Intel P4’s superpipelined ALU  
  
32비트 덧셈을 할때 16비트 16비트 나눠서 함.  
  
의존성 문제도 안생김.  
  
bandwidth는 1/(16비트 add 시간), 즉 약 2배 빨라진 것.  
  
### 나누기 힘든 리소스도 있다.  
  
메모리 자체는 pipelining이 힘들다.  
  
왜? → 순차성이 필요하고, 메모리 접근 속도가 불확실하다(cache miss, hit)  
  
병렬적인 메모리 접근을 위해 메모리를 많이 넣거나, L1, L2등 여러 캐시를 두거나 할 수는 있는데 근본적인 RAW hazard를 해결하는 건 아님/  
  
---
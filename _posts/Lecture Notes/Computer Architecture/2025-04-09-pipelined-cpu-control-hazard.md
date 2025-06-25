---  
tags:  
  - cpu  
  - pipeline  
  - hazard  
  - branch-prediction  
share: "true"  
github_title: 2025-04-09-pipelined-cpu-control-hazard  
title: 9. Pipelined CPU - Control Hazard  
date: 2025-04-09  
categories:  
  - Lecture Notes  
  - Computer Architecture  
---  
### Data Dependence (Review)  
  
- True dependence (Read-after-Write)  
    - Instruction must wait for all required input operands  
- Anti-Dependence (Write-after-Read)  
    - Later write must not affect a still-pending earlier read  
- Output-Dependence (Write-after-write)  
    - Earlier write must not affect an already-finished later write  
  
---  
  
### Control Dependence  
  
- 모든 명령어는 control flow에 영향을 받습니다.  
- 모든 명령어는 PC를 바꿉니다.  
    - 즉, 모든 명령어는 PC에 의존성이 있다! (레지스터, 메모리뿐만이 아님)  
  
PC의 값을 어떻게 바꿀지는 위의 단계에서 정해진다.  
  
예외적으로 branch 명령어만 EX단계에서 결정되는데, 이는 BEQ등의 명령어는 두 operand에 대한 빼기 등 비교 연산이 시행된 후에 PC에 얼마를 더할지 정해지기 때문이다.  
  
→ 이 말은 우리는 ID를 보기 전까지는 PC를 업데이트할 수 없다는 의미이다.  
  
헐 개망한듯 무조건 1-cycle stall이 생기잖아. 이건 forwarding할수도 없다. (이미 계산된걸 빨리 땡겨오는게 아니라 계산조차 안됨)  
  
그렇다면 우리는 다음 IF를 하기 전에 한 사이클 기다린 뒤, PC주소가 나오면 IF를 해야하는가? Branch면 2 사이클? 2배 느려지네?  
  
---  
  
## MIPS R2000 Control Flow Design (in early stage…)  
  
Simple address calculation based on instruction only.  
  
- 일반적인 주소는 다음과 같은 간단한 연산입  
    - Branch offset: 16bit full addition + 14-bit half addition (???)  
    - Jump PC offset: concentation only  
- 간단한 branch condition은 RF기반으로 빠르게 처리하기  
    - register가 0보다 큰지 작은지, 같은지만 보면 됨  
  
→ Branch condition을 ID에서 해버리는 것.  
  
→ branch여부도 가져오자마자 처리함.  
  
$$ IPC = 1 / [1+(0.2\times0.7)\times1] = 0.88 $$  
  
전체 명령어 중, 20%가 branch. 70%가 그 중 실제로 jump하는 비율이다.  
  
stall은 branch jump시에만 일어나기 때문에…  
  
→ 사실 실제로는 메모리가 100cycle 정도 걸려서, 100이나 99나..  
  
### Branch delay slot  
  
어, 어차피 branch 걸리면 무조건 1-cycle 기다리잖아? 일단 그럼 무관한 한 사이클 처리하고 점프하자.  
  
하든 안하든 dependent가 없는 명령어 하나를 끼워넣는다.  
  
→ 나중에 순서대로 실행하는 CPU가 나오면 실행 불가.  
  
### Data Hazard Analysis (최종)  
  
EX에 use가 있는건 forwarding으로 땡겨왔기 때문에 값을 바로 쓸 수 있기 때문이다.  
  
Br은 PC를 해결하기 위해 어쩔 수 없이 거리가 멀어졌다.  
  
### PC Hazard Analysis (최종)  
  
휴, 이제 웬만하면 처리가 된다. 하지만, 여전히 jump하게 되는 부분에는 ID에서 Jump임을 알기 떄문에 jump인 경우에는 한 사이클을 기다리게 되는군.  
  
→ 실제 modern CPU에서는 10~20 cycle 뒤에 알게되기 떄문에 한 사이클 일찍 안다고 좋을게 없다.  
  
## 이제 뭐해야지?  
  
걍 branch이면 찍어야함;;  
  
Note: branch predictor는 functionality에 영향을 주지 않음. 조금 느려질 뿐.  
  
### (1) PC=PC+4로 찍자  
  
Note: ~20%만이 jump 관련이다.  
  
대부분 forward(if-else)는 50%정도이고, backward는 (Loop back)은 90%정도로 점프한다. (ret, call 등등)  
  
계산해보면 ~70%정도가 뛰고 ~30%정도가 안뛴다.  
  
즉, 1-0.2*0.7 = 0.86의 확률로 맞는 branch predictor 인 것이다. 근데… 14%에 해당하면?  
  
pipeline에 잘못 들어온 친구들이 존재한다. 그냥 다음으로 예측했는데, 사실은 jump하는거였으니 너네는 들어오면 안되는 애들이야.  
  
→ 이런 친구들을 `wrong path instruction` 이라고 한다.  
  
아키텍쳐적인 이유에 의해 잘못들어온 친구들은 파이프라인에 들어온 흔적을 남기면 안된다.  
  
ID를 하고 EX를 하니 엥 뛰는에였네? ID와 EX에서 들어와버린 2개를 죽여야한다.  
  
즉, 14%는 2-cycle penalty가 생긴다.(ID에서 눈치챘을 때) (text-book에서는 3개의 bubble이 생긴다고 정한다. 왜일까?)  
  
<aside> 💡  
  
Why textbook say 3-cycle loss? EX가 끝난 상황에서 알면, branch 명령어가 MEM으로 가는 시점에 명령어가 잘못되었음을 파악한다. 따라서 현재 들어온 IF, ID, EX를 모두 버려야한다. 한편, EX가 끝나고 다음 사이클이 시작되기 전에 신호를 보내면, IF, ID만 버리면 되므로 2 cycle 손해가 된다.  
  
</aside>  
  
IPC = 1 / (1+0.14*2.5) = 0.70~0.78  
  
패널티를 줄이려고 하는데, 패널티 자체는 못줄인다. (요즘 CPU는 버릴게 많다.) 따라서 틀릴 확률을 줄이자.  
  
### (2) PC = Jump로 하자  
  
그냥 branch가 아니라도 +4로 jump하는 것으로 간주하는 거지.  
  
80%는 브랜치가 아니니까 +4로 뛰는것으로 간주  
  
14%는 실제로 뛰는 녀석이니 뛰는 것으로 간주  
  
→ 94%의 정확도.  
  
근데…  
  
(1) 이게 뛰는지의 여부도 맞아야하지만  
  
(2) 얼마나, 어디로 뛸건지도 예측해야한다.  
  
→ 더 어렵다.  
  
---  
  
## Branch Target Buffer (Hardware Memory; Oracle)  
  
큰 메모리가 있어. PC의 가능한 경우의 수 2^32개의 row가 있어. 이때, BTB에는 지난번에 뛴 주소를 적어놓는 것이다.  
  
ex) 1000 ADD rs rt rd … 실행했으면 그 후에 1000번째 주소에 1004가 적혀있음.  
  
ex) 2000 J 1000이면 그 후 2000번째 주소에 3,000이 써져있음.  
  
IPC = 1 / (1+ 0.2_0.3_2) 이다.  
  
0.2 = branch 일 확률  
  
0.3 = 안뛸 확률  
  
### In real BTB…  
  
- 2^32 = 4GB짜리 버퍼를 만들 수는 없으니, PC의 LSB 일부만 따와서 만든다.  
- 즉, PC를 Hash하는 것이다.  
- N은 8 이하로 해야 한 사이클 내에서 완료 가능.  
  
→ 하지만, collision이 발생할 수 있다. 이 경우 엉뚱한 곳으로 jump한다.  
  
→ Use TAG to detect this collision!  
  
### Tagged BTB  
  
앞부분을 tag로 하여 tag table을 따로 만든다.  
  
(1) JUMP일때만, tag table과 BTB에 저장한다. 이떄, 앞부분은 tag table에, 뒷부분은 BTB에 저장한다.  
  
(2) BTB에서 뒷부분을 이용해 hash하면, 값이 나온다. 이때 같이 붙어있던 tag table에서 앞부분 tag를 비교한다.  
  
(3) 맞다면 그대로 jump, 아니라면 PC+4한다. (아닌 명령어는 register 명령어일 가능성이 매우 높으니)  
  
→ 즉, 진짜 같은 JUMP인데 틀릴 확률은 뒤의 N비트가 같은 명령어 주소가 있었고, 하필 두 명령어 모두 BRANCH 명령어어야한다.  
  
(4) Collision마다 BTB Update  
  
→ 만약 재수없게 JUMP인데 collision이라 jump안했으면 여부를 기억하고 있다가 실제 branch 정보 파악 후 flush  
  
### Branch History Table  
  
I know…you…  
  
- 80프로는 브랜치 아니라 무조건 맞춤  
- 20프로 중에서도  
    - backward에는 (ret, call) 90프로 맞춤  
    - if-else에는 50%로 맞춤.  
  
→ forward인지 backward인지에 따라 나눠주면 되겠네?  
  
→ 가정: ‘아까 뛰었다면 이번에도 뛸 확률이 높다”  
  
1비트 추가.  
  
- BHT에서 0(방금 안뜀) 이면 다 맞아도 안뜀  
- 1이면 뜀  
  
Worst case: T - NT - T - NT - T - NT … (0%)  
  
2비트로 state 나누기\  
  
### 2-bit Saturation Counter  
  
강한 뜀 - 뜀 - 안뜀 - 강한 안뜀  
  
뛸때마다 왼쪽, 안뛸때마다 오른쪽  
  
### 2-bit Hysteresis Counter  
  
2연속 틀리면 아예 상태를 강하게 바꿔버림  
  
각 state model은 다른 패턴을 인식한다. 즉, 어떤 프로그램을 돌리냐에 따라 다르다.  
  
## State-Machine Based Predictors  
  
이 모데은 평균적으로 90% 이상 맞춤.  
  
IPC = 1 / (1+0.2_0.10_2) = 0.96  
  
와!  
  
2-bit을 굳이 쓰는 이유는 무엇일까?  
  
- branch의 80%는 1, 2bit 성능이 비슷함. → 계속 하던거 하는 애가 많다는 의미. ret, if else 등  
- 5~10%만이 성능에 영향을 주는데, 계속 바뀌는 친구들이다.  
    - 1-bit에서는 2 mis  
    - 2-bits에서는 1mis  
- 나머지는 구제 불능. 즉, 돈을 더 써도 조금밖에 좋아지지 않을 수 있다.  
  
<aside> 💡  
  
Why we don’t make 3, or more bits of BHT?  
  
- 컴퓨터 프로그램은 하던 일을 반복하려고 함. 즉, 하던 일을 계속 하는걸로 가정하는건 잘 만듦.  
- 하던일을 안하려고 하는걸 예측하는건 더더 어려움. 돈도 많이 들고 → Amdahl’s Law  
  
</aside>  
  
<aside> 💡  
  
96%면 좋은 것 아닌가요? → No.  
  
→ 실제 CPU는 명령어를 6~7개씩 가져오고, 파이프라인 내의 명령어도 20개정도가 된다.  
  
즉, 이중 20%가 브랜치이면 거의 100개가 있는거다. 즉, 파이프라인은 모두가 맞아야한다.  
  
0.95^100 ⇒ 엄청 낮다.  
  
하나라도 틀리면 파이프라인의 절반이 날아가버림 ㅋㅋ ㅠ  
  
</aside>  
  
---  
  
## Global Path  
  
Branch의 결과는 보통 다른 브랜치와 엮어서 많이 나온다.  
  
```cpp  
aa = bb = 1;  
if(a > 1) ;; B1  
	aa = 0;  
if(b > 1) ;; B2  
	bb = 0;  
if(aa==1 && bb==0) { ;; B3  
...  
}  
  
// Note that B3 = !B1 && B2  
```  
  
→ How to capture this?  
  
### Gshare Branch Prediction  
  
Global한 BHSR (Branch History Shift Register)은 지난 M개의 브랜치 명령어의 결과를 추적한다.  
  
(NT T NT T T NT …)  
  
M-bits와 BTB idx N-bits을 XOR연산해서 tag table에서 찾는다.  
  
물론 이러면 더이상 tag table idx는 마지막 주소가 아니다. 하지만, 실제 주소와 최근 M개에서 나온 패턴을 바탕으로 한 상황을 바탕으로 찍기 때문에 좀 더 효율이 좋다.  
  
<aside> 💡  
  
Gshare branch predictor is both local (PC주소 기반) and global (taken pattern 기반) predictor!  
  
</aside>  
  
### Predicting call and ret?  
  
call은 예측하기가 쉽다. (하나의 주소에 있는 call은 하나의 함수를 가르키기 때문에 비교적 local하게도 예측이 쉽다.)  
  
하지만 ret은? 소프트웨어적으로 누가 이 함수를 호출했는지 모르는데 BTB 따위가 어떻게 알수가 있냐. 매우 어렵다.  
  
### Return Address Stack  
  
ret 명령어가 나왔다면, 돌아갈 명령어 (call을 부른 명령어 주소 +4)를 하드웨어적인 부분인 Return address Stack이다.  
  
BTB를 안보고 무조건 return address stack을 본다.  
  
<aside> 💡  
  
Call stack의 caller-saved-register를 이미 저장하는데 그거 쓰면 안되나요? → 그건 메모리에 있어서 로드하는데 너무 오래걸리구요..  
  
그것은 functionality를 위한 것인데 이 return address stack은 RET 명령어의 branch prediction 확률을 올리기 위한, 하드웨어적인 장치이다.  
  
</aside>  
  
|질문|답변|  
|---|---|  
|RISC ISA에서 `RET` 명령어가 없는데, 하드웨어는 어떻게 return인지 알까?|**CALL(jal 등)을 추적해서 RAS에 push하고, `jr $ra` 같은 패턴을 return으로 heuristically 판단해 pop한다.**|  
|하드웨어가 100% 정확하게 알 수 있나?|❌ 아니야. 일반적인 jump와 혼동될 수도 있어서 prediction miss가 생길 수 있어.|  
|실전에서는?|**정확도 높지만 완벽하지 않은 return predictor**로 쓰고, miss하면 flush로 회복함.|  
  
---  
  
## Two-level branch `direction` predictor  
  
composite of Branch History Table and Pattern History Table  
  
PC 주소를 통해 BHT를 본다. 그러면 해당 값은 지난 M번동안 ‘뛰었는가 안뛰었는가’가 저장되어있다.  
  
|명령어 주소 바탕으로 패턴 기록 (BHT)|  
|---|  
|뜀뜀안안안안|  
|뜀뜀안안안뜀|  
|…|  
|…|  
  
|뛴 패턴에 따른 현재 상태 (PHT = state machine)|  
|---|  
|매우 뜀|  
|매우 안뜀|  
|…|  
|…|  
  
‘각 패턴을 PC마다 따로 or 하나의 레지스터’ 인지에 따라 앞 알파벳 PA vs GA가 갈리고  
  
‘브랜치 상태를 따로 관리 or 하나의 상태로 관리’에 따라 p vs g가 갈린다.  
  
|종류|정확도|테이블 크기|구조적 난이도|특징 요약|  
|---|---|---|---|---|  
|GAg|낮음|작음|쉬움|빠르고 작지만 conflict 많음|  
|GAp|중간~좋음|중간|약간 복잡|실제 CPU에서 자주 사용됨|  
|PAg|중간|중간|약간 복잡|PC별 특화된 히스토리 but 공유된 테이블|  
|PAp|가장 좋음|가장 큼|어려움|논문 수준 predictor, 실용성은 낮음|  
  
---  
  
## Alpha 21264 Tournament Predictor  
  
Pag와 Gag 중 ‘더 잘맞을 것 같은거’ 정한다.  
  
Pag와 Gag를 둘 다 쓴 뒤, Choice prediction을 통해 정한다. (누가 맞았는지 히스토리)  
  
|코드 예시|어떤 predictor가 유리?|이유|  
|---|---|---|  
|`if (i < N)` (루프 조건)|Local (PAg)|루프 횟수만 보면 됨|  
|`if (A && B && C)` 중간 분기|Global (GAg)|앞 분기 결과가 영향 줌|  
|`if (error_flag)`|Local|고정된 플래그 기반|  
|상태 전이 기반 조건들|Global|이전 흐름이 중요한 상황|  
  
---  
  
### Multiple Predictors Power PC 604  
  
여러 레벨로 파이프라이닝을할 수 있다.  
  
---  
  
### Implementing Branch predictor in Pipeline!  
  
`Trust, but verify`  
  
→ 브랜치 맞냐 틀리냐 여부는 한참 뒤(짧아야 2~3 cycle, 많으면 20cycle)에 나오기 때문에 BHT나 BTB를 업데이트하려면 엄청 기다려야한다.  
  
→ 따라서 브랜치 predictor는 그냥 내 예측이 맞았다고 가정하고(…) BHT, BTB를 바꿔버린다.  
  
**Speculative Execution**  
  
분기 결과가 확정되기 전에 예측된 경로의 명령어를 미리 실행해 성능을 높이는 기법이다.  
  
---  
  
## Trace Caching  
  
Branch predictor의 예측 결과를 바탕으로,  
  
실제 실행될 instruction 흐름(trace)을 통째로 캐시해놓는 구조  
  
→ branch prediction 결과를 바탕으로 미리 cache에 해당 명령어를 basic block단위로 가져다놓는다.  
  
---  
  
## Predicated Execution  
  
모든 경우의 수를 다 동시에 계산하는 파이프라인.  
  
Dataflow적인 하드웨어 구조를 만든다.  
  
하지만 이 경우 브랜치가 3개만 되어도 8개의 파이프라인이 돌게 된다. 파워를 10배이상 먹게되어 상당히 안좋다.  
  
---  
  
## SW in branch prediction  
  
brp - btb등을 컨트롤한다.  
  
→ 아키텍쳐 가정을 꺴다.  
  
brp 포함 시 다른 컴퓨터에서 안돌아간다.
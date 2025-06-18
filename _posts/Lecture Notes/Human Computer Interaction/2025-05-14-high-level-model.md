---  
tags:  
  - hci  
  - conceptual-model  
  - GOMS  
share: "true"  
github_title: 2025-05-14-high-level-model  
title: 12. High-Level Model  
date: 2025-05-14  
categories:  
  - Lecture Notes  
  - Human Computer Interaction  
---  
## GOMS  
  
HIP: good model for ‘short’, ‘isolated’ task.  
  
→ Do not scale to complex, routine tasks!  
  
GOMS: A higher-level model  
  
→ Models `skilled` behavior using Goals, Operators, Methods, and Selection rules.  
  
Why use GOMS?  
  
- `experienced workers` 의 수행 시간 예측 가능  
- 인터페이스 디자인 결정을 도움  
- routine cognitive-motor task에 집중함 (problem solving이 아님)  
  
---  
  
### CNM-GOMS  
  
- Goals  
    - 원하는 결과나 작업  
    - 어떤 응용 프로그램이냐에 관계 없이 동일함. 함수명과 같음 (ex. print page)  
- Operators  
    - 작업을 수행하기 위한 기초적인 행동. (perceptual, cognitive or motor) (ex. 선택한다, 하이라이트 한다)  
- Methods  
    - sub-goal이나 operator의 일련의 순서 → 목적을 달성하기 위함  
    - 선택한다 → 백스페이스를 누른다. → 지워진 것 확인 → (글자 지우기 목적 달성!)  
- Selection Rules  
    - 여러 method가 있을 때 무엇을 선택할 것인가?  
    - 애매하지 않은, 하나로 딱 정해지는 기준이 있어야함 (deterministic)  
  
→ Classic GOMS (CNM-GOMS, KLM) assumes `skilled users`  
  
→ CPM-GOMS, NGOMSL address `learning` and `parallel behavior` → more accurate.  
  
---  
  
## Origin of GOMS  
  
목적  
  
- Expert user가 어떻게 인터페이스와 상호작용하는지에 대한 structural way를 준다.  
  
영향  
  
- Model-based evaluation in HCI → 사용자 없이 수학적 모델로 실험.  
- Led to the development of several GOMS variants!  
  
---  
  
<aside> 💡  
  
GOMS 바탕으로 분석하기!  
  
</aside>  
  
ex) 단어 일부 옮기기.  
  
Goal: quick brown을 앞으로 옮기고 싶다.  
  
subgoal: 해당 문장을 하이라이트하고 싶다.  
  
Operators: 단어를 더블클릭하여 하이라이트한다. 키보드 백스페이스를 누른다.  
  
Methods: 키보드로 복사-붙여넣기를 한다. 단어를 삭제하고 다시 타이핑한다.  
  
Selection Rules: 단어 단위 이동이면 더블클릭. 글자 단위라면 지우고 다시 쓰기.  
  
---  
  
→ bottleneck을 파악하고 자주 반복되는 operator들을 shortcut으로 만들어 줄 수 있다.  
  
---  
  
## Keystroke Level Model (KLM)  
  
- GOMS의 간소화버전.  
- Routine, error-free task  
- No selction rules → Assume Decision already made  
  
키보드 입력 - K (=0.2s), 포인터 이동 - P (=1.1sec) 처럼 각 operator를 매핑함.  
  
**→ 고정된 값으로 매핑하기 때문에 상대적으로 비교하는 것이 중요.**  
  
KLM도 predictive model!  
  
- Task 실행 시간을 예측할 수 있음. (experienced users)  
- 구현 전에 interface를 비교할 수 있음.  
  
---  
  
<aside> 💡  
  
KLM 바탕 시간 분석이 나올 듯.  
  
</aside>  
  
K: 키보드 버튼 누르기  
  
P: 마우스 포인팅. 커서 옮기기  
  
H: 키보드 ↔ 마우스 손 옮기기  
  
M: 행동 전 생각하기  
  
R(t): 시스템 응답 시간  
  
---  
  
그 외에도 B: 마우스 버튼 클릭, W: system response를 기다리는 wait time 등이 추가될 수 있음.  
  
→ Multiple variants!  
  
→ Useful for tasks with fine-grained interactions. (dnd)  
  
---  
  
## Application & Limitation of GOMS  
  
### Application  
  
- CAD system  
- Telephone operator (CPM-GOMS: modern)  
- KLM  
  
### Limitations  
  
- Only assume skilled users (for GOMS)  
- Do not deal with **errors**  
- Do not deal with skull aquisition  
- Do not deal with high level issues (functionality, fatigue, workload)  
- Better for `relative` than absolute timing (그냥 고정된 값 할당한거라 그 자체로는 의미가 별로…)  
  
---  
  
## CPM-GOMS  
  
cognitive perceptual motor GOMS.  
  
각 cognitive model이 parallel하게 동작. 의존성 있는거 최대한 기다리고 각 프로세서 (모터는 심지어 눈,왼손, 오른손이 나뉨) 에 최대한 할당.  
  
### NYNEX Example  
  
전화 회사에서 이걸 적용해서 아주 이슈가 되었다~  
  
- keystroke을 줄이고  
- 자주쓰는걸 유저 손가락 가깝게!  
  
→ 근데 4% 느려짐…  
  
KLM만 썼으면 이걸 설명할 수가 없음. 하지만 CPM-GOMS는 가능함.  
  
→ 제거한 keystroke는 critical path에 있지 않았음. (어차피 slack time에 누르는 것)  
  
→ 제거한 keystroke이 critical path에 놓이게 되면서 더 느려짐.  
  
사실 이건 실제 관찰 기준이 아니라 spec 기준으로 해서 그렇게 됨. (실제로 어떻게 이루어지는지 모르고 만듦. 그래도 field trial보다는 쌌잖아 한잔해~)  
  
Saving not bottleneck doesnt help!  
  
→ 설득 측면에서 이득.  
  
---  
  
## NGOMSL Methodology  
  
- Top down breadth-first task decomposition  
    - 사용자의 탑-레벨 목표부터 시작.  
    - 그 목표를 이루기 위한 과정을 subgoal이나 keystroke 수준에서 작성.  
    - keystroke만 남을 떄까지 반복.  
    - selection rule 적용  
- Count the number of statements in methods to predict learning time  
    - re-used submethods? → 간편화하자.  
  
그럼 selection rule 어떻게 설정하는가.  
  
- 만약 너가 비디오 녹화 시작할 때와 끝날 때 모두 출석이라면 → 버튼으로.  
- 끝날 때 없고, 시간을 안다면 → 끝나는 클럭 타이머 세팅  
  
조금더 natural language에 가깝다.  
  
---  
  
## 그래서 GOMS의 Value가 뭐지?  
  
- (아마도) high-value decision에 좋다.  
- (아마도) strong-arguments를 만드는데 좋다.  
- 개발자/디자이너가 어떤 작업, 어떤 디자인 결정이 속도에 영향을 주고 안주는지 결정하는데에 대한 직관을 기르게 해준다!  
    - Helping designers develop an intuition about what **works** and what **doesn’t** work. and the impact of **design decision on speed**
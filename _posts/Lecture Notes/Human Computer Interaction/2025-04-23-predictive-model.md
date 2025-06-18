---  
tags:  
  - hci  
  - predictive-model  
  - fitts-law  
share: "true"  
github_title: 2025-04-23-predictive-model  
title: 11. Predictive Model  
date: 2025-04-23  
categories:  
  - Lecture Notes  
  - Human Computer Interaction  
---  
## Predictive Models?  
  
- A predictive model is a `mathematical formula` used to estimate outcomes.  
- predicts the result for a `criterion variable` (aka `dependent variable`) ← based on `predictor variables` (aka `independent variable`)  
    - 예측 변수로 기준 변수를 예측.  
  
<aside> 💡  
  
Predictor variables(독립 변수) shoule be `numeric` or encoded in a way that the model can use. (e.g. one-hot encoding)  
  
</aside>  
  
→ 사용자가 어떻게 행동하는지 explore하는 것을 도와준다.  
  
→ descriptive models와의 차이점?  
  
- 아이디어나 개념 뿐만 아니라 number을 다룬다!  
  
### Levels of Measurement  
  
### Why use predictive models?  
  
- 최초의 HCI 연구에서 실험 결과가 잘 나왔지만, 더 나아가 그들은 이렇게 얘기했다!  
  
> 이 논문은 pointing device를 직접 사용하는 것의 경험적 결과에 대한 것이지만, `결과에 대한 이론적인 설명` 이 만들어졌으면 더 좋을 것 같다. 이를 통하면 다음과 같은 이점이 있다.  
  
1. the need for some experiments might be obviated  
    - 일부 실험의 필요성이 없어질 수 있다. 즉, 정확한 예측 모델이 있으면 굳이 모든 실험을 하지 않아도 되므로 시간과 자원을 아낄 수 있다.  
2. Ways of improving pointing performance might be suggested  
    - 모델 바탕으로 어떤 요인이 성능(포인팅 디바이스)에 영향을 주는지 분석하고, 이를 바탕으로 성능을 높일 수 있는 개선점을 도출할 수 있다.  
  
## Predictive model examples  
  
## Linear Prediction equation  
  
선형 관계를 나타내는 아주 기본적인 방정식  
  
`linear regression` 을 통해서 예측 방정식을 만들어 낸다.  
  
목표: 주어진 (x, y) 샘플에서, 식 y=mx+b의 계수 m, b에 대해 `squared distance를 최소화하는 선` 을 만드는 m, b를 찾는다  
  
- 결과는 x와 y의 관계를 가장 잘 추정한 결과로 도출됨  
- Assumption: relationship is `linear` ! (당연하지만…)  
  
Squared correlation(상관계수): prediction equation이 data variation의 n%를 설명한다.  
  
## Fitts’ Law  
  
- Model for `rapid aimed movements` (e.g. cursor toward, selecting the target)  
- Three key uses in HCI  
    - Use Fitts’ law prediction equations to predict and compare design alternatives (→ Predictive model에 대한 설명)  
    - Fitts Law의 IP (Index of performance; aka Throughput)를 종속변수로 쓰고 입력 장치, 기술의 퍼포먼스 평가. → (Im이 어떻게 변하는지 확인)  
    - 디바이스가 Fitts’ law를 잘 따르는지 평가  
  
**Task Paradigm**  
  
- Serial Task → 타깃까지 가는 시간을 측정.  
- Discrete Task. → 신호를 주면 방향을 결정하고 이동하는 것 까지 측정.  
  
**Index of difficulty (ID)**  
  
target selection task의 난이도를 측정한다.  
  
$ID = log_2({A\over W} +1 )$  
  
단위 = 비트  
  
피츠의 가설: Movement time (MT)는 ID에 비례한다.  
  
**`Effective` Index of difficulty**  
  
$W_e$ : Effective target width. 유저가 응답한 것의 variability. 4.133*SD로 계산하며 여기서 SD는 유저가 클릭한 위치의 표준편차이다. → ID_e 는 실제로 유저가 수행한 활동을 capture한다. (무엇을 하라고 시켰는지 보다는)  
  
즉 엄청 큰 버튼이라도 레이블이 작아서 사람들이 레이블 위주로 클릭했다면 유효 너비는 작아질 수 있다.  
  
## Choice reaction time  
  
n개의 자극이 각각의 반응으로 매핑되어있다고 하자.  
  
ex) 5개의 전구 자극 → 각 손가락 매핑  
  
이 자극을 바탕으로 어떤 행동을 할지 고르고 수행하는데 걸린 시간이 `choice reaction time` 이다.  
  
`Hick-Hyman law` 에 의해 predict될 수 있다.  
  
$$ RT = a + b \times log_2 (n+1) $$  
  
이때 n은 정보의 종류 개수이다.  
  
→ Hick-Hyman law는 uncertainty가 얼마나 응답시간과 정확도에 영향을 주는지 설명한다.  
  
→ 선택지가 많을수록 더 많은 정보를 처리해야한다는 뜻이고, cognitive load를 증가시킬 수 있다.  
  
이때 확률이 다른 경우에도 엔트로피 법칙을 이용해 적용할 수 있는데…  
  
$$ H = \sum p_i log_2 ({1 \over p_i} +1) $$  
  
이때 p_i가 모두 같으면 위의 Hick-Hyman law가 나오며, H는 불확실성의 척도로 볼 수 있다. RT = a + bH로 계산되는 것이다.  
  
**Application Example)**  
  
- Menu design: broad and shallow vs narrow and deep  
  
two depth + four items vs one depth + eight items?  
  
→ log(3)+log(5) vs log(9)  
  
one depth가 빠르다.  
  
## Keystroke-level model (KLM)  
  
---  
  
higher level model에서…  
  
## Skill acquistion  
  
대부분의 HCI 작업들은 반복적인 경우가 많은데, 반복할수록 수행능력이 좋아진다.  
  
(predictor variables) ⇒ amount of practice  
  
(criterion variales) ⇒ Proficiency (time, speed …)  
  
### Power Law of Learning  
  
proficiency 와 practice 간의 non-linear한 관계  
  
$$ T_n = T_1 \times n^a $$  
  
분수함수꼴 (Power)로 감소.  
  
Note: a는 음수 (그래야 감소하제..)  
  
### Speed Variation  
  
$$ S_n = S_1 \times n^a $$  
  
(0<a<1 : 서서히 증가폭이 감소하며 증가하는 꼴)  
  
작업을 반복하면 반복할수록 점점 빨라진다.  
  
### Example: QWERTY vs Opti  
  
### Learning  
  
Problem solving, Manual Skill, Writing books 모두 로그 스케일로 시간이 감소한다.  
  
### Stage of Skill Acquisition  
  
(1) Cognitive  
  
- Verbel representation of knowledge (아는거 계속 말하기)  
- Instructions, Examples  
- Learn through problem-solving (trial and error)  
  
(2) Associative  
  
- Proceduralization  
    - Rehearsal → recognition  
  
(3) Autonomous  
  
- More and more automated  
- Faster.  
- No cognitive involvement!  
    - Become hard to describe  
- `The importance of motor program`  
  
<aside> 💡  
  
In cognitive stage, user often face `novel problem` (ex. 강 건너기에서 다시 돌아오기) 효율적으로 하기 전에 사용자는 어떻게 해야할지 찾아내야한다.  
  
</aside>  
  
### To conquer complex problems…  
  
We need to break them down → divide-and-conquer  
  
→ `Operator Subgoaling` (by Newell)  
  
### Operation Subgoaling  
  
A strategy where a problem solver breaks down a task into a smaller, more manageable sub-tasks  
  
달성 방법  
  
- Subgoal creation: 큰 문제를 작은, 관리가능한 부분으로 나눔  
- Operation Application: 각 subgoal마다 특정 작업이나 operation을 수행함.  
- Iterative Process: 해당 과정 반복.  
  
→ Help manage Cognitive load by allowing user to focus on smaller aspect.  
  
Tips?  
  
- Backward Planning  
- Subgoal → Mental Rule (각 subgoal이 if-then rule로 LTM에 저장)  
  
### Production Rules  
  
- Set of rule-based instruction used to `control a system` or `predict an outcome`, formatted as if-then statements.  
  
→ Human thinking, decision-making process를 모델링할때 사용  
  
다음으로 이루어져있다.  
  
- Rule Base: 특정 조건에서 수행할 작업이 정의된 규칙의 set임  
- Working Memory: The current information or state which is being processed  
- Inference Engine: 변화나 의사결정을 할 때 working memory에 규칙을 적용하는 메카니즘  
  
### Why Production Rules are useful?  
  
1. Structured Control을 가능하게 한다.  
  
- 각각의 subgoal은 production rule에 명시된 조건에 따라 트리거될 수 있음. 복잡한 문제에 대해 구조화된 컨트롤이 가능해진다.  
  
1. 과정을 만들어나갈 때, memory load가 줄어듦.  
    - control-action 쌍은 procedural knowledge를 나타냄  
    - 메모리를 적게 쓸 수 있음.  
2. step-by-step으로 매번 탐색하기보다는 빠르고 직접적인 액션이 가능  
    - 모든 가능성을 생각하지 않고도 바로바로 인지할 수 있음 (not O(n)! )  
  
예시)  
  
1 → 2 → 3…을 셀 수 있는건 각 숫자를 매번 생각하는게 아니라, 3 다음이 4이다. 라는 정보가 LTM에 저장된 것.  
  
### Experts  
  
Expert doesn’t engage cognitive system…GOAT. (even perception goes away 😲)
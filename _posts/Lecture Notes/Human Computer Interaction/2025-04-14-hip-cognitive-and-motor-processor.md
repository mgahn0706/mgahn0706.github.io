---  
tags:  
  - hci  
  - psychology  
  - cognition  
share: "true"  
github_title: 2025-04-14-hip-cognitive-and-motor-processor  
title: 10. HIP - Cognitive and Motor Processor  
date: 2025-04-14  
categories:  
  - Lecture Notes  
  - Human Computer Interaction  
---  
# Cognitive Processor  
  
cognitive processing rate: $\tau_c = 70ms$.  
  
HIP에서 basic principle은, `Recognize-Act Cyle of Cognitive processor` 이다.  
  
즉, 인지하고 행동하기를 명령하는 사이클인 것이다.  
  
### Recognize  
  
- The contents of WM `initiate actions` associatively linked to them in LTM.  
  
### Act  
  
- These actions in turn `modify the contents` of working memory.  
  
즉, WM에서 a라는게 들어오면 LTM에서 a→b라는 action을 가져온다. 이걸 바탕으로 b라는 action을 만든다. (여기까지 recognize). 그 후 WM에 b를 올려놓는게 act인 것이다.  
  
### Variable Cognitive Processor Rate Principle  
  
(1) Cycle time is shorter when greater effort is induced  
  
(2) Cycle time decreases when you practice!  
  
→ Cognitive processor가 관여하는 부분이 줄고, muscle memory가 담당하게 된다.  
  
### Cognitive processor의 특성  
  
Parallel in recognition, but serial in action.  
  
- 한번에 여러개를 aware할 수 있다.  
- 하지만, attention은 한 번에 하나씩만 처리할 수 있다.  
    - 우리가 실제로 동시에 한다고 생각하는 것은 다음과 같이 처리된다.  
        - `skilled intermittent allocation` 을 하고 있다.  
        - `interrupt-driven` time sharing  
  
---  
  
## Stay in the Flow  
  
사람의 attention은 한정되어있기 때문에 UX를 구성할 때 하나의 플로우에만 집중하게 하는 것이 cognitive footprint를 줄이는데 도움이 된다.  
  
- Make them only focus on doing their job, not understanding what UI work  
  
---  
  
### Human Performance  
  
사람마다 성능이 다르다.  
  
Slowman - middleman - fastman  
  
---  
  
## Motor System  
  
- Receive input from working memory(which came from cognitive processor)  
- Execute motor programs (not by `step-by-step`)  
  
한 스텝에서 멈추고 가는게 아님.  
  
두 선 사이에 최대한 많이 왔다갔다를 시켰을 때, 보통 5초에 68번 왔다갔다한다.  
  
즉, motor processor는 약 73.52ms이다. (대충 70)  
  
다만 이 케이스에서는 cognitive와 perception도 일어나는데…  
  
---  
  
### Closed Loop  
  
feedback from perception → cognitive → motor → correction.  
  
위의 왔다갔다 예시가 바로 correction이 있는 closed loop!  
  
### Open Loop  
  
motor executed without perception or cognition. → no feedback, no correction  
  
예시) 양궁  
  
만약 Open loop을 가정했다면, cycle time은 74ms.  
  
Closed loop을 가정하여 correction이 약 20번 났다고 하자.  
  
correction에는 x + 100 + 70 ms 가 든다.  
  
5초동안 났으므로, 5000 / 20 = 250ms  
  
250ms = 100 + 70 + x.  
  
x = 80ms.  
  
---  
  
## Fitts’ Law  
  
Predictive model of human movement  
  
$$ MT = a +b ID = a+blog_2 ({2D\over W}) $$  
  
임을 피츠가 밝혔다.  
  
그 후에 Welford가 밝히기를  
  
$$ T = I_M log_2({D\over S}+0.5) $$  
  
---  
  
그 후에 MacKenzie는  
  
$$ T = b log_2({D \over S}+1) +a $$  
  
를 썼다.  
  
Im, Id는 log(2D/S), 즉 어려운 정도를 뜻한다.  
  
Ip는 Id/T로, 어려움에도 빠르게 해결한 정도를 뜻한다.  
  
사람들이 실제로 누른 영역을 actual width로 계산해야한다는 견해도 있다.  
  
타겟까지 손을 움직이는데 걸리는 시간은, n번의 과정을 거치게 되는데…  
  
$$ T = n(\tau_p + \tau_c + \tau_m) $$  
  
이다.  
  
$X_i$를 i번째 수정 후에 타겟까지의 거리라고 하고, 상대적 정확도 $\epsilon = {X_i \over X_{i-1}}$라 하자. 이를 0.7로 가정하면..  
  
$$ X_n = \epsilon^n D \le 0.5S $$  
  
일 때 멈춘다고 하자.  
  
$$ n = -log_2(2D/S) /log_2(\epsilon) $$  
  
---  
  
이므로 log_2(2D/S)에 비례하게 되는 것이다.  
  
I_M도 구할 수 있는데, -(240ms)/log_2e = 63ms/bit 이다.  
  
### Implications  
  
- Larger, Closer targets are easy to click  
- Mac is faster to use (사실상 화면 위의 넓은 곳이 다 클릭 가능 범위)  
- pie menu is better than pop-up menu  
  
---  
  
## Power Law of Practice  
  
$$ T_n = T_1n^{-\alpha} $$  
  
알파값은 0.2~0.6  
  
---  
  
## Overall of HIP  
  
It is a model - understandable by computer scientists  
  
Predictive, but simple  
  
Does not accurately describe underlying mechanisms  
  
Ex) Do two letter same?  
  
A a  
  
1. A는 이미 인지한 상태에서 a를 인지한다  
2. a가 cognitive processor에 a라고 인식된다.  
3. a가 A랑 같은지 matching 한다  
4. 이제 response를 만든다  
5. 실제로 반응한다  
  
100 + 3*70 + 70 = 380ms  
  
어… 그러면 표에 따르면  
  
simple Reaction: 100+70+70  
  
Physical match: 100+2*70+70  
  
Name match: 100+3*70+70  
  
Class match: 100 + 70 + 70 + 70 + 70 + 70  
  
인데, 실제 실험에서는 name이 더 빨랐지? → name match에는 더 많은 단계가 필요하다고 예측했지만, LTM 등 다양한 변수가 있다. 고정된 시간이 아니다. 사람들은 이름 비교에 더 익숙할 수 있다. 즉 이는 완벽한 모델이 아님을 보여준다.  
  
---  
  
### Reading Speed  
  
RSVP로 읽으면 매우매우 빨리 읽을 수 있다. No motor time.  
  
EYE MOVEMENT = 230ms정도 이다. (지각-인지-이동) 해야하니까.  
  
saccade에는 120ms가 든다.  
  
phrase마다 눈을 움직인다고 가정하고, 구 마다 2.5단어가 있다고 하면…  
  
230ms / EM * EM / phrase * 2.5/phrase = 약 652 words / min  
  
→ bottleneck은 230ms. 따라서 motor cycle을 줄이자.  
  
170ms로 줄일 수 있다. RSVP로 한다면. 882까지!
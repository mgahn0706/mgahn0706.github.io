---  
tags:  
  - hci  
  - psychology  
  - perception  
  - memory  
share: "true"  
github_title: 2025-04-11-hip-perceptual-processor-and-memory  
title: 9. HIP - Perceptual Processor and Memory  
date: 2025-04-11  
categories:  
  - Lecture Notes  
  - Human Computer Interaction  
---  
## Human Information processor model  
  
- 인지심리학의 컨셉을 ‘통합’하여 만들어짐  
- 컴퓨터과학자들에게 이해시키기 위한 모델  
- 매우 간단화되었음.  
- Practical!  
  
## HIP has subsystems  
  
메모리는 공유되고, 각각의 프로세서를 가진다.  
  
- 메모리: decay가 있다. (정보손실), capacity  
- processor: 고정된 1-cycle  
  
### Perceptual system  
  
- Detect input through visual sensors  
- Store `sensory memory`  
- 감각된 정보들은 symbolic code로 코딩해서 working memory에 save  
  
### Cognitive system  
  
- Working memory에 저장된 정보를, long term memory의 정보와 matching을 한다.  
- 기존 지식 기반으로 decision-making을 한다.  
  
### Motor system  
  
반응에 따른 모터를 작동시킨다.  
  
⇒ 수학적으로 표현 가능.  
  
---  
  
## Perceptual System  
  
### Sensor (Eye) 👀  
  
central vision  
  
- Fovea (1~2D)  
- 2도  
  
periphral vision  
  
- retina  
- intensity  
  
30도 이상 떨어지면 머리를 움직임  
  
### Visual Image Store vs Working memory  
  
Visual image store  
  
- Passive system  
- Hold raw visual info (~1sec)  
- 집중 필요 없음  
- 의도하지 않으면 빠르게 decay됨  
  
Working memory  
  
- active  
- 수 초  
- 비교, manipulation 등  
  
### Perceptual Processor  
  
- Physical perception → abstract concepts  
  
색, 모양, 방향 등… unidentified non-symbilic → recognized symbolic  
  
- Coded for transfer to working memory  
    - Progressive decoding  
        - 들어오는대로 변환  
    - Selective decoding  
        - 특정 신호에 집중  
- Has Capacity (ex. 17 letter)  
  
### Capacity and Decay  
  
12개중 평균 4.5개. (사실 기억을 다시 말하고 쓰는 과정에서 decay 가능성)  
  
→ Partial report procedure  
  
전체를 보여준 후 일부만 복기하도록. (거의 100%)  
  
따라서, verbalize 되기 전에 decay 되는 것을 확인  
  
→ delay를 늘이면 decay를 측정 가능  
  
### Sperling’s experiment  
  
decay: ~200ms  
  
반감기처럼 거의 50%가 되는 시간이 200ms.  
  
### Variable Perceptual Processor Rate Principle  
  
- Cycle time of perceptual processor: $\tau_p = 100$ (50~200ms)  
      
    - 하나의 지각 단위를 처리하는데 걸리는 시간.  
- 조건에 따라 이 사이클 시간을 짧아질수도 길 수도 있다.  
      
    - 신호의 세기가 크면 사이클 시간을 짧아진다. (더 빠르게 처리한다.)  
    - ex) 고세기, 고대비 자극이 들어오면 → 아주 빠르게 처리 (50ms 이하)  
    - ex) 저대비, 약한 신호가 들어오면 → 느리게 처리 (200ms 이상)  
- Cycle time = Unit impulse response  
      
    - h[n] 아님  
    - Impulse 이후에 사람이 봤다고 선언하기 까지의 걸리는 시간.  
      
    → 응답시간까지 걸리니까 좀… 부정확함. (하나의 impulse가 들어왔을 때 symbolic하게 코딩해서 working memory에 넣는 시간)  
      
  
Key concept: `Quantum Experience`  
  
- 각 지각 당 100ms  
      
- 이 시간동안… 자극은  
      
    - 서로 합쳐질 수 있음 (perceptual fusion)  
    - 서로 인과관게가 있다고 느낄 수 있음 (causality) → 중요!  
      
    → 100ms 내의 자극에서는 하나로 합쳐져서 양자화 됨.  
      
  
### Bloch’s Law  
  
$$ R = I \times t = k    
$$  
  
(단, $t<\tau_p$, $k$ 는 상수)  
  
- R: response (실제로 지각된 밝기)  
- I : Intensity (자극의 세기)  
- t: lasting time of stimulus  
  
→ 시간 * 강도로 합성한다. 밝은 빛, 짧은 시간 = 어두운 빛, 긴 시간  
  
### Moving picture rate  
  
프레임 지속 시간이 지각 perceptual cycle time보다 짧아야한다.  
  
### Perceptual Causality  
  
- 입력과 반응이 100ms 안에 일어나야 내가 눌러서 일어났구나, 라고 안다.  
- 즉, 10fps보다는 높아야 부드럽다고 느낌  
  
→ UI Design Insight: UI feedback이 100ms보다 짧게 온다면, 유저에게는 바로 일어났다고 생각됨. = better UX  
  
### Color makes them popout  
  
color, orientation, shape, size 등을 바꿔서 pre-attentive 하게 할 수 있다  
  
→ 굳이 working memory에 저장하여 cognitive하지 않아도 된다.?  
  
### Pre-attentive Task  
  
attention이 유발되고, cognitive 돌긴 하는데, 거의 안쓰이는.  
  
250ms 안에 처리할 수 있는.  
  
Hue and Shape는 짧은 시간에 할 수 없다. not preattentive.  
  
Fill and Shape은 boundary가 있는지 없는지 확인하는 것은 바로 알거나 (fill), 모른다 (shape)  
  
Hue and shape에서도 hue가 지배적임  
  
Hue and brightness에서는 둘 다 preattentive함  
  
---  
  
## Working memory  
  
Register file이 있다 ㄷㄷ  
  
- Access in chunks (이것도 같네..) → task dependent하게 정의됨. (words, image…)  
- 7 +- 2 chunks  
  
→ Working memory도 decay한다. (수 초)  
  
- Content dependent  
- attention span(집중할 수 있는 시간)은 5초 정도이다. 즉, 5초를 넘을 수 없다.  
- Long term memory에 commit해야함.  
- external cognition tool이 필요!  
  
### Decay Rate  
  
7초의 반감기를 가진다.  
  
→ Effect of interference. 기존 정보와 얽히게 된다.  
  
Murdock과 Peterson의 실험에서 밝혀짐!  
  
따라서, UI를 디자인할 때, 7초 이상 무언가를 기억하게 한다면 congnitive load가 증가하게 된다!  
  
### Interference  
  
기존에 내가 갖고 있던 long-term memory와 섞여서 decay될 수 있다.  
  
### Chunks  
  
- LTM에 활성화된 element들  
- memory나 perception의 기본 단위  
- 내가 무엇을 알고 있는지에 따라 의존적임  
  
Chunk can be related to other chunks!  
  
→ Activation spread in LTM. → interfere with old ones.  
  
ex) ROBIN - ROBERT - BIRD - WING - WINGSPAN - BOARDGAME - 으아아  
  
→ 한번에 activation하여 link할 수 있는 chunk는 제한되어있기 때문에 이러면 decay가 일어난다.  
  
### Capacity  
  
- `pure capacity`: 3 chunks (숫자를 불러주다가 갑자기 이제 역순으로 불러보세요 하기)  
- `effective capacity` : LTM을 써가면서 (???) 한다. 약 7+- 2개의 chunk 가능  
  
---  
  
## Long-term memory  
  
- 매우매우 큰 저장소 (virtually infinite)  
- Semantic encoding (단순 물리적 신호를 저장하는게 아님)  
- network of related chunks, accessed associatively from WM (working memory와 관련이 있는 애들을 LW할 수 있음)  
  
1. **Associative Access**  
  
fast read: 70ms  
  
- 각 프로세스 cycle 마다 접근해서 가져올 수 있음  
  
Expensive, slow write: 10s  
  
- noisy  
- require several rehearsal, recall  
- information is stored semantically  
  
⇒ Context the time of acquisition is key for retrieval!  
  
1. Unlimited capacity and little decay (no erase!)  
  
Then why we forget?  
  
→ No effective associations. (dangling pointer가 생긴다. 우리 뇌는 아쉽게도 garbage collecting이 없다.)  
  
→ Interference by similar associations (light가 여러 의미로 저장이될 수 있는데, 다른 애들과 간섭나버림)  
  
1. To remember something…  
    - Associate with items already in LTM with novel ways  
    - Elaborative Rehearsal vs Maintenance Rehearsal (repition)  
        - 한번 외우고도 반복, 또 반복
---  
tags:  
  - hci  
  - design  
  - prototype  
share: "true"  
github_title: 2025-03-30-design-process-prototyping  
title: 6. Design Process - Prototyping  
date: 2025-03-30  
categories:  
  - Lecture Notes  
  - Human Computer Interaction  
---  
## Make Idea Tangible!  
  
Prototype is a `simplified` and `incomplete` models of a design used to  
  
- Explore ideas  
- elaborate requirements  
- Refine specifications (spec 미리 정의)  
- Validate functionality (되는지 안되는지 미리 확인)  
  
### Prototype can help designers to…  
  
- 실세계의 디자인 요구사항을 이해할 수 있다.  
- 실제로 구현하기 전에 미리 시각화하고, 테스트하고, early stage에 구체화 가능  
- 다 만들기 전에 미리 무엇이 되고 무엇이 안되는지 확인 가능  
  
---  
  
## Prototypes  
  
왜 프로토타입을 써야하는가  
  
- 유저와 함께 디자인할 수 있다. → 협업과 iteration 강조  
- 무엇이 되는지 안되는지 미리 알 수 있고 사용성 테스트를 미리 해볼 수 있다. → before investing full development!  
  
→ Lo-Fi prototypes uncover usability problems as many as Hi-Fi ones.  
  
---  
  
### Idea selection: Prioritizing for prototype  
  
Define each idea’s importance  
  
- Reality 생각  
- User preference, target user population  
- Feasibility (아이디어 짤 때는 아니었어도, 하드웨어 구현이 가능한지, 비용은 안비싼지 등…)  
- Window to market  
- Team skills and resources  
  
→ Rank them, and pick top 1~5.  
  
---  
  
## Prototyping methods across PHASE  
  
### Phase I, Early Exploration  
  
Goal: Understand user need, test ideas  
  
→ Rapid Lo-Fi implementation.  
  
Sketches, board, storyboard…  
  
### Phase II, Concept Validation  
  
Goal: Test with real users  
  
- Digital mockups (Figma)  
- Wizard of OZ  
- Clickable UIs  
  
### Phase III, User Evaluation  
  
Goal: test in more realistic  
  
- Toolkit based implementation  
- Actual UI libraries  
- Larger groups  
  
### Phase IV, Final Product  
  
Goals: Validate ,polish  
  
- Fully functional system  
  
---  
  
Now let’s see what each prototypes are!  
  
---  
  
## Lo-Fi Prototypes  
  
Paper, Plastic based interface  
  
- Using sketches, foamcore, PICTIVE (종이, 필름 기반 인터랙션)  
  
### Sketches  
  
- drawing of outward appearance  
- `crudity` means people concentrate on `high-level` concepts!  
    - 못그릴수록 사람들이 기능에 집중한다. → pixel, 폰트가 이상하다는 피드백이 안온다.  
  
→ 잘 그릴 필요 없다.  
  
**Sketching is thinking out loud!**  
  
(1) Create  
  
- Early ideation, brainstorming  
- Visualize  
  
(2) Record  
  
- ideas you develop  
- archive idea for later reflection  
  
(3) Reflect, share  
  
- Communicate with others  
  
---  
  
### Getting the Right Design vs. Getting the Design Right  
  
(1) Right Design  
  
- Generate many ideas  
- Focus on what to solve  
  
‘많은 아이디어 중에 무엇?’  
  
(2) Design right  
  
- 어떤 아이디어든  
    - 테스트하고  
    - usability를 향상 시키고  
    - refine, finalize하는 일련의 과정을 잘 지키는 것.  
  
⇒ You can find local maxima by making design right, but is it best solution…? We need many ideas!  
  
- Generate many ideas  
- Reflect on all ideas  
- Develop them in parallel  
- Add new ideas as they come up  
- iterate!  
  
---  
  
### Elaboration and Reduction  
  
기회를 찾아가는 elaboration. (make the right design)  
  
선택지를 줄이며 의사결정하는 reduction. (make the design right)  
  
→ 반복하는 Repeat 중요  
  
**선택을 할 때, 창의성이 발휘될 수 있는 지점이 두 군데 있다:**  
  
1. **선택지 자체를 ‘의미 있게 다르게’ 나열하는 창의성**  
      
    → 즉, _내가 어떤 선택지들을 고려할지_ 정하는 데 창의성을 발휘하는 것.  
      
    예: 앱 디자인을 할 때, 그냥 색깔을 바꾸는 수준이 아니라 “카드 기반 인터페이스”, “챗봇 인터페이스”, “AR 기반 UI”처럼 진짜 서로 다르게 작동하고 경험이 다른 옵션들을 생각해내는 것.  
      
2. **그 선택지를 고르는 기준(=기준이나 휴리스틱)을 정하는 창의성**  
      
    → 즉, _그 많은 선택지 중에 어떤 기준으로 고를 것인지_에 창의성을 발휘하는 것.  
      
    예: 성능이 아니라 “사용자가 덜 피곤하게 느낄 수 있느냐” 같은 기준을 새롭게 만들어서 그 기준으로 판단하는 것.  
      
  
---  
  
### 그래서 Lo-Fi prototype은..  
  
1. 싸면서도  
2. high-level 피드백을 줄 수 있으며  
3. 유저의 반응을 볼 수 있다.  
  
부정확하긴해~  
  
---  
  
## Wizard of OZ  
  
엣헴  
  
실험을 하는 사람이 이론적으로 지능이 있는 컴퓨터(AI 등)를 시뮬레이션 한다.  
  
실제 소프트웨어가 없는 상황에서 사용성 테스트하기  
  
→ 음성인식, 얼굴인식, 필기인식 (너무 옛날 아닌교~)  
  
반응 및 인터랙션을 확인하고, 그에 맞는 동작을 ㅎ준다.  
  
ex) 음성인식으로 타자 입력하기. (실제 구현까지는 오래걸려도, 미리 어떻게 입력해야하는지 어떤 UX가 좋은지 테스트해볼 수 있다.)  
  
자율주행 자동차 버튼 테스트 (실제로는 사람이 운전해주고, 버튼 사용성을 테스트한다.)  
  
---  
  
### Low-Tech Prototype  
  
- Design are cumbersome(번거롭다!)  
  
→ Wizard of OZ costs high-cognitive load.  
  
해야할거 너~~~~~~무 많아서 휴먼-컴퓨터가 이제 힘들어질 수 있다. 빠르게빠르게 못해줄 수 있지.  
  
---  
  
### Tool for prototyping  
  
1. DENIM (interactive prototyping wth storyboard)  
2. WOZ Pro (Quick and easy creation of lo-fi ui prototype)  
  
---  
  
## Medium-Fi (for phase II and III)  
  
- Using prototype tools (JS, FIgma…)  
  
(1) Vertical prototpye  
  
하나의 기능에 대해 끝까지 구현.  
  
모두싸인에서 하나의 리마인더 유저스토리를 끝내는 것을 피그마로 만들었다.  
  
모달의 사용성, 디자인 등 평가할 때 용이  
  
(2) Horizontal prototype  
  
하나의 완성된 UI를 제작  
  
메뉴 세팅이나 레이아웃 테스트에 용이  
  
(3) Scenario Prototype  
  
미리 짜둔 태스크의 walkthorugh만 테스트  
  
Rigid: No deviation!  
  
Useful for simulating a user journey  
  
세줄요약  
  
1. `시간`이 많이 든다. 종이보다는 당연히 더 들겠죠.  
2. 팀원간 `정렬` 이 안맞을 수 있다.  
    1. 개발자는 ‘이미 개발한건데 또 바꿔?’ 라고 생각할 수 있고  
    2. 주주들은 ‘이게 완성본인가요? 너무 구린데요?’ 라고 생각할 수 있다.  
3. 형태보다는 `기능` 에 집중하게 된다.  
    1. 디테일에 집중하지 마라  
    2. 폰트나 컬러같은거 고르지 마라. (이건 내가 현업할때 잘 못했던 것 같다.)  
    3. 픽셀 틀어진걸로 뭐라하지 마라  
  
---  
  
## High-fi prototypes  
  
- Piecewise prototype  
- Alpha, beta release  
- Nearly final product  
  
→ 여기서 바꾸면 너무 비싸~  
  
---  
  
### Alternative Classification?  
  
`Concept` prototyping → 예비 디자인을 평가하고 발전시키기  
  
- 초창기 아이디어 평가에 좋음  
- 실물같은 착각을 하게 되는 문제 (걍 컨셉인디…)  
  
`Rapid, Thow-it-away` prototyping → 작은 모델을 테스팅하는 것  
  
- 딱 기능적인 부분만 테스트하는 것. (ex. 차체 모델의 풍랑 테스팅)  
- scaling fallacy 발생 가능 (아니 작게 했을 때는 됐는데…)  
  
`Evolutionary` Prototyping → 디자인 스펙이 너무 자주 바뀌고 불명확할 때  
  
- 디자인 → 평가 → 정제 과정을 계속 거침  
- Incremental principles
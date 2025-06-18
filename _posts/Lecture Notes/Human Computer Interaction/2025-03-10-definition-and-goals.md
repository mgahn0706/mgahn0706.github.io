---  
tags:  
  - hci  
  - ux  
share: "true"  
github_title: 2025-03-10-definition-and-goals  
title: 1. Definition and Goals  
date: 2025-03-10  
categories:  
  - Lecture Notes  
  - Human Computer Interaction  
---  
## Computer is upgrading, but…  
  
Moore’s Law에 의해 컴퓨터의 속도는 점점 빨라지고 있고 (요즘 깨지긴 했지만)  
  
AI는 사람보다 더 잘해지는 분야가 많아지고 있다.  
  
이에 반해 인간의 능력은 거의 constant하게 유지되며, 컴퓨터와 인간의 능력 차이는 점점 커지고 있다.  
  
---  
  
## HCI  
  
### What is HCI?  
  
HCI는 다음과 같이 정의된다.  
  
> A discipline concerned with the **analysis**, **design**, **implementation** and **evaluation** of `interactive computing systems` for `human use` and with the study of major phenomena surrounding them.  
  
‘concerned’한게 정의라니 참 모호하다.  
  
결국 인터랙티브한 컴퓨팅 시스템을 인간이 사용하는 것을 분석하고, 디자인하고, 구현하고, 평가하는 것에 관심이 있다는 뜻.  
  
### Content of HCI  
  
(지금은 은퇴하신) Bengt Göransson께서 쓰신 **User-Centred Systems Design - Designing Usable Interactive Systems in Practice(1992)** 논문에서는 HCI의 content를 다음과 같이 정의한다.  
  
**N. Nature of HCI**  
  
- (Meta-)Models of HCI  
  
**U. Use and Context of Computers**  
  
- Human Social Organization and Work  
- Application Areas  
- Human-Machine Fit and Adaption  
  
**H. Human Characteristics**  
  
- Human Information and Processing  
- Language, Communication, Interaction (Language는 요즘 AI도 하지만, 일단 인간)  
- Ergonomics (인간공학)  
  
**C. Computer System and Interface Architecture (Not primary in this course)**  
  
- Input & Output Devices  
- Dialogue Techniques  
- Dialogue Genre  
- Computer Graphics  
- Dialogue Architecture  
  
**D. Development Process**  
  
- Design Approaches  
- Implementation Techniques  
- Evaluation Techniques  
- Example Systems and Case studies  
  
**P. Project & Examination**  
  
### Importance of HCI  
  
**Users**  
  
- For heterogeneous & diverse users  
- For novice users with less technical expertise (노인, 어린이 등)  
- For almost every task (even toothpaste!)  
  
**Technology**  
  
- Mobile  
    - Smartphones, tablets…  
- Ubiquitous  
    - high mobility → Faster, more reliable, smaller, cheaper…  
- Ambient  
    - Bigger, complicated  
  
**Business**  
  
- ex) 삼성이 애플의 ‘bounce-back’ 패턴과 디자인 특허를 침해했는데 이 UI와 인터페이스 소송으로 1조 넘는 보상액을 지불해야했다. 즉, 비즈니스에서도 HCI가 중요해졌다.  
  
---  
  
## Scope and Terms of HCI Research  
  
HCI는 범위가 정말 넓다.  
  
먼저, I**nteractive Computing System**을 만들고 해당 시스템에는 상호작용이 가능한 **인터페이스**를 만든다. 사용자는 해당 인터페이스로 **인터랙션을** 하고, 이를 통해 **User Experience**를 얻는다.  
  
해당 도구(Tool)를 활용해 Behavior가 변화하게 되고, 이를 통해 우리가 달성하고자 했던 Goal에 (좋든 나쁘든) 영향을 주게 된다.  
  
어떤 사람은 각 계층 중에서 인터페이스 단에 더 관심이 있을 수도, UX 분석에 더 관심이 있을 수도 있다.  
  
또, 하나의 scope (예를 들어, Human)에서도 1명만 집중할 것인지 여러명에 관심을 둘 것인지도 다 다르다.  
  
  
위의 Experience는 손 터치의 아이폰에 비해 펜의 사용성을 늘리는 연구를 한 것인데, 당시 UI Component의 한계로 경험을 더 좋게 만들기 어려우셨다고 한다. 그리고 펜이 사라지면서 연구가 많이 쓸 일이 없어졌다.  
  
→ HCI 연구를 할 때에는 포맷이 변해도 잘 유지되는 주제를 선정해야겠군.  
  
---  
  
## User Experience (UX)  
  
> A person’s **perceptions** and **responses** that result from the use or anticipated use of a **product**, **system** or **service** (ISO 9241-210)  
  
ISO 표준으로 UX의 정의가 내려져있다. 사람이 제품, 시스템, 서비스를 사용할 때 느끼는 인지와 반응을 의미한다.  
  
- 사람이 어떤 것을 사용할 때 **`감정을 느끼는`** 방식, 기쁨과 만족, 열고 닫고, 보는 등…  
- 사람들이 사용하는 모든 제품은 UX를 가지고 있다. (Garrett, 2003)  
  
따라서 우리는 UX를 ‘디자인’할 수는 없다. UX를 타깃할 수는 있어도 indirect하게 조정할 수 있을 뿐이다. → designers cannot fully control.  
  
### Characteristic of UX  
  
> The focus has shifted from `objects` to the `experiences` that result from interacting with them. (Norman, 2008)  
  
(1) Humane, but Soft  
  
- UX는 인간의 특성과 행동을 잘 이해하고 분석해야하지만, 수학적인 점수와 측정가능한 척도가 부족할 때가 있다.  
  
(2) Strategic, but Abstract  
  
- UX는 종종 high-level의 전략적 사고를 기반으로하며, 회사의 전략적 decision에 큰 영향을 주지만, 추상적이며 tangible하지 않다.  
  
(3) Contextual, but Uncertain  
  
- UX는 이 시스템이 어떤 환경에서 쓰일지, context를 고려하여 기반을 세워야하지만, 그 context는 dynamic하게 바뀐다. (예상치 못한 사용성 등)  
  
→ Without proper theories(WHY) and methodologies(HOW), UX can be just mirage!  
  
---  
  
## HCI Research Framework  
  
논문을 위한 논문을 쓰지 않기 위해… Observation을 한 뒤, 모델이 제대로 설명되지 않는 경우를 찾고, 설계하고, 실험해야함.  
  
---  
  
## Goal of HCI  
  
→ “Optimal User Experience (UX)”  
  
### Usefulness (유용성)  
  
결국 사용할 때 유용해야한다. 유저가 goal을 이루는 것을 도와줘야한다.  
  
ex) 세탁기의 여러 기능들, 여러 기능이 추가된 갤럭시 폴드, 새로운 기능의 자동차 등  
  
### Usability (사용성)  
  
쓰기 편하고 효과적이어야 한다. 아무리 유용해도 쓰기 어려우면… (ex. 터미널로 명령어 입력하는 chat gpt) 구린 UX이다  
  
> The extent(사용성) to which a product can be used by `specified users` to achieve `specified goals` with **effectiveness**, **efficiency**, and **satisfaction** in a `specified context of use`. (ISO 9241-11) Usability  
  
사용성은 결국 ‘누구나’ ‘아무거나’가 아니라 특정 유저가 특정 목표를 , 특정 상황에서 효과적으로 달성하도록 하는 것이다.  
  
ex) ‘30대 남성 헬스 트레이너’(users가 ‘음악을 운동하면서 들을 때’ (context of use), 더 효율적인 ‘음악 추천 서비스를 제공’(goal)한다.  
  
⇒ effectiveness, efficiency, statisfaction을 어떻게 측정할 것인지 정의한 뒤, 사용성 testing을 진행한다.  
  
**사용성 목표 예시**  
  
- 얼마나 빨리 작업을 수행하는가 (효율성)  
- human error의 비율 (효과적인가)  
- time to learn (learnability)  
- 한번 배우고 n주 뒤에 다시 시켰을 때 얼마나 기억하는가 (retention 측정, memorability)  
- 주관적인 만족  
  
### Affection (심미성)  
  
감성적인 것도 무시할 수 없는 요소이다.  
  
결국 디자인은 사람들을 `설득`하기 위해 (물건 구입 등) 하는 것이다.  
  
미묘하고 기분 좋은 방법으로 그들을 설득해야한다. (명시적으로 하면 거부감 들 수 있음)  
  
ex) 계단을 이용하라고 설득하고 싶을 때 → 엘베 금지 (X), 계단을 예쁘게 꾸미기 (O)  
  
**Emotional design**  
  
- 이미 존재하는 perception으로 유저 설득하기  
      
- 어떤 물체의 디자인은 three-level로 인식된다.  
      
    (1) Visceral: 첫인상 (gut feeling)  
      
    (2) Behavioral: 몇번 쓰면서 느끼는 perception. Usability, Functionality  
      
    (3) Reflective levels: Meaning, Connection. 오래 쓰다보면 느낌.  
      
  
<aside> 💡  
  
이런 감성적 영역은 측정을 시도할 수는 있으나 noise가 많아서, 대체로 interview를 진행한다.  
  
</aside>
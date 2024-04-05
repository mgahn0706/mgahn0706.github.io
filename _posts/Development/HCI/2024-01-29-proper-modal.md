---
tags:
  - modal
  - ui
  - ux
share: "true"
github_title: 2024-01-29-proper-modal
title: 모달 잘 쓰기
date: 2024-01-29
categories:
  - Development
  - HCI
---
### 찾아보거나 알게된 배경
---

Too many modals…
모달을 잘 쓰는 방법과, 모달이 많을 때의 단점을 알아봅니다.


### 모달이란?

> A dialog is a modal window that appears in front of app content to provide critical information or ask for a decision.

모달은 material design에서는 Dialog 라고 지칭하고 있습니다.
제품과 사용자가 ‘대화’를 한다는 점을 강조한 네이밍인데요. 이 비유만 잘 마음속에 간직하면 이어질 내용들이 이해가 더 잘될 것입니다.
모달은 중요한 정보를 제공하거나, 사용자에게 어떤 결정을 내리라고 시킬 때 사용하는 컴포넌트입니다.
Toast, Snackbar와 가장 큰 차이는 사용자의 행동을 막아버린다는 점이죠.
현재 사용하고 있는 페이지를 덮어버리고 새로운 콘텐츠를 띄워줌으로써 사용자가 새롭게 뜬 내용을 빠르게 인지할 수 있도록 합니다.
사용자에게 ‘행동’을 묻거나 ‘중요한 정보를 잘 인지했는지’ 물어볼 때 사용할 수 있습니다. 단순 정보제공의 경우에는 지양하는게 좋습니다. 모달이 주는 그 위계와 영향력은 다른 어떤 컴포넌트보다도 크니까요. (다른 행동을 다 막아버림)

### 모달을 왜 무분별하게 쓰면 안될까

> 이유 요약: **Dialogs disable all app functionality when they appear, and remain on screen until confirmed, dismissed, or a required action has been taken.**

모달은 사용자가 어떤 행동을 취하기 전에는 app 자체를 비활성화시킵니다.
상당히 강압적인 UX이죠. 따라서 중요한 행동이 아니라면 모달을 사용하는 것을 지양해야합니다.
불필요한 모달은 아래와 같은 문제점이 있어요

- 끄기 어려워요
- 잘 정의하지 않으면 접근성을 해칠 우려가 있어요
- 인지 부하(cognitive load)를 증가시켜요. 사용자가 생각하는 중간에 새로운 정보가 들어오기 때문이에요
- 화면이 작은 사용자에게 안좋은 UX를 제공할 수 있어요. (모바일 화면에 적합하지 않은 경우가 많다)
- 너무 많이 씁니다
- 사용자는, 모달이 떴을 때 무엇을 해야하는지 다시 파악하기 때문에 혼란스러워한다는 연구결과가 있습니다.

### 모달 잘 쓰는 법

모달을 쓰지 말라는 것은 아닙니다. 어떻게 하면 잘 쓸 수 있을까요?

### **Don’t**

**(1) 자기혼자 열리는 모달**

사용자가 예상할 수 없는 모달 띄우기는 사용자를 불안하게 합니다.
사용자의 액션 없이 모달이 스스로 띄워지게 하는걸 지양해야해요.
제품이 먼저 말을 걸어오는 상황인데, 다른 행동을 모두 막아버린다는 점을 염두해야합니다.


**(2) 모달료시카 (Nested Modal)**

~~이제 선언적으로 열려서 콜백지옥이 생긴다~~
이렇게 알려줄게 많다면, 다른 페이지로 만드는게 맞지 않았을까요?


**(3) 여러 단계가 있는 모달 (Multistep Modal)**

언제 끝날지 가늠이 안되는 여러단계 모달은 사용자를 불안하게 합니다.
다음 step에는 뭐가있길래 이렇게 오랫동안 막는거지?
그리고 ‘한 모달은 하나의 역할을 해야한다’는 원리를 깨기도 합니다.


**(4) 마케팅 모달**

마케팅은 중요하지만, 사용자의 행동을 막아서는 순간 사용자는 읽지 않습니다.

### Do

- 닫기 쉽고, (접근성까지 고려해서)
- 하나만 물어보며 (사용자는 ‘할지’ ‘말지’만 선택하면 됨)
- 짧아야한다. (사용자가 콘텐츠를 빠르게 파악할 수 있어야한다.)

 > 💡 **사용자의 행동을 막으려는자, 그 무게를 알라. Great power comes with great responsibilities**



### 참고자료

---

[https://m3.material.io/components/dialogs/guidelines](https://m3.material.io/components/dialogs/guidelines)

[https://modalzmodalzmodalz.com/](https://modalzmodalzmodalz.com/)
---
tags:
  - affordance
  - hci
  - ux
  - ui
share: "true"
github_title: 2023-11-08-affordance
title: Affordance(어포던스)
date: 2023-11-08
categories:
  - Development
  - HCI
---

### Introduction
---

‘이 컴포넌트는 어포던스가 낮아요’

‘어포던스를 높였으면 좋겠어요’

위계, 가시성이 높으면 어포던스가 높은 것일까. 자주 듣는 이 어포던스를 어떻게 이해하면 좋을까?

---
### What is Affordance?

> [!info] An affordance is what an object can do (but not feature!)

어포던스는 어떤 물체가 ’할 수 있는 것’입니다. 우리가 여태까지 써왔던 ‘어포던스’의 용례와는 많이 다르죠.

그 이유는, 어포던스는 사용자에 의해서만 나타나기 때문입니다. ‘물체가 할 수 있는 것’은 사용자가 해당 물체와 상호작용할 때에만 나타나죠.

그러므로 어포던스는 물체가 ‘사용자와의 상호작용(user interaction)’에 의해 할 수 있는 것을 의미합니다.

물체의 인지적 특성은 그 물체가 무엇을 할 수 있는지와, 어떻게 조작될 수 있는지를 나타내죠.

어포던스는 ‘높고 분명(obvoius)’하거나 ‘숨겨질(hidden)’ 수 있습니다.

### Signifier

이러한 어포던스는 Signifier에 의해 구체화 됩니다. signifier는 물체가 무엇을 할 수 있는지 나타내거나 설명해줍니다. 여기서 signifier는 어포던스의 존재에 대한 감각적/인지적 (perceptual or sensory) 지표를 얘기합니다.

signifier는 ‘확실하거나’ ‘모호할’ 수 있습니다.

→ 따라서 어포던스는 높거나 낮은 상태로 항상 존재하는 것이고. signifier에 의해 ‘확실하거나 모호하게’ 사용자에게 인지됩니다.

→ 어포던스가 높다 = 사용자에게 이 친구가 **무엇을 하는 친구**인지 잘 설명된다.

### Example of Obvious / Subtle Affordance
![Pasted image 20240220132615.png](../../Pasted%20image%2020240220132615.png)

왼쪽의 시계는 어포던스가 모호합니다. 어떤 곳을 눌러야 하는지도 모르겠고, 위에 있는 버튼이 무엇을 하는지 사용자가 알기 어렵습니다.

오른쪽의 선풍기 버튼은 어떤가요? 이 버튼이 선풍기에 어떤 조작을 가할지 확실하게 드러나며, 어포던스가 분명한 편입니다. 이 어포던스는 버튼 아래의 label이라는 signifier에 의해 강하게 전달되었군요. 버튼이 튀어나와있다는 점도 한 몫한 것 같네요,

→ 오른쪽의 선풍기 버튼은 ‘누를 수 있다’는 강한 어포던스를 가지며 그 아래의 라벨이라는 signifier로 인해 ‘바람 세기를 조절하려면 눌러라’라는 것을 말해준다.

### Negative Affordance and False Affordance

negative affordance는 ‘하지 말라’는 것을 말해줍니다. `이 버튼은 눌러도 할 수 있는게 없어. 기능이 없어.` 라는 것을 알려주는 것이죠.

대부분의 서비스에서는 disabled 된 버튼이 negative affordance를 주고 있습니다.

반대로, false affordance는 ‘할 수 있는 것 같았는데 안되는’ 어포던스입니다. ‘상호작용가능하다’는 어포던스가 있었는데 정작 사용자가 사용해보니 작동이 안되는 케이스입니다.

이런 경우는 사용자에게 오해와 안좋은 UX를 줍니다. 대부분 잘못된 디자인이나 제품 버그로 나오게 됩니다.

### Affordance === Visibillity?

어포던스가 높다는 것은 그래서 ‘잘 보인다’. ‘눈에 잘 띈다’ 라는 의미일까요? 완벽한 동의어는 아니라고 합니다.

어떤 물체의 affordance는 좋은 signifier를 통해 높은 가시성을 확보하게 됩니다.

결론적으로, 가시성은 ‘얼마나 어포던스가 잘 나타났냐’를 의미하고 ‘사용자가 어떻게 해당 물체의 option을 알고 자신이 하고 싶은 것을 얼마나 straight하게 알 수 있었냐’를 의미합니다.

> **Good visibillity means…**
> 
> How clear can users now what all the options are, and know straight away how to access them.


그러니 ‘어포던스를 높여주세요’는 ‘눈에 잘 띄게 해주세요’가 아니라 ‘이 컴포넌트가 무슨 역할인지 잘 드러나게 해주세요’라는 뜻입니다!

### 참고자료

---

[https://careerfoundry.com/en/blog/ux-design/affordances-ux-design/](https://careerfoundry.com/en/blog/ux-design/affordances-ux-design/)

[https://www.tandfonline.com/doi/abs/10.1207/S15326969ECO1502_1](https://www.tandfonline.com/doi/abs/10.1207/S15326969ECO1502_1)

[https://www.interaction-design.org/literature/book/the-glossary-of-human-computer-interaction/affordances](https://www.interaction-design.org/literature/book/the-glossary-of-human-computer-interaction/affordances)
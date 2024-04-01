---
tags:
  - hierarchy
  - ui
  - design
  - hci
share: "true"
github_title: 2023-10-18-hierarchy
title: 시각적 위계(hierarchy)는 어떻게 구현되는가
date: 2023-10-18
categories:
  - Development
  - HCI
---
### Introduction

---

회사를 다니면서, 협업하고 있는 디자이너분과 대화하다보면 ‘시각적인 위계’, ‘버튼의 위계’ 등의 말이 자주 나오게 됩니다.
저는 버튼의 컬러나, border만 수정하면 되는 일이었지만, 왜 버튼의 색이나 border가 어떤 ‘위계’를 만들어주는지 궁금해졌습니다.
버튼의 어떤 요소가 위계를 만드는 것일까요?

### 요약

---

디자인의 요소에는 점/선/면 이 있으며 이 요소는 어떠한 ‘위계’를 가집니다.

![hierarchy.png](/assets/img/posts/hierarchy.png)
위 그림에서 알 수 있듯이, 선에서 현실 세계의 표현으로 갈수록 눈에 더 잘 띄게 됩니다. 이것으로 인해 시각적인 위계가 생기게 되는 것이죠.

동그랗게 그은 선보다는 면이, 면보다는 입체감을 준 면이 더 눈에 잘 띈다는 의미입니다.

실제 프로덕트에서 ‘점’을 사용하는 경우는 거의 없으므로  ‘선’으로 구현된 디자인이면 위계가 낮구나~ 정도로만 생각하면 될 것 같습니다.

https://www.atlassian.com/ko

위 웹사이트에서는 ‘지라’의 UI를 나타내고 있습니다.

shadow나 입체감 없이 flat하게 구현된 것을 볼 수 있습니다. 각 item은 선으로 표현했으며, 특정 버튼과 Epic은 면(plane)으로 표현하여 위계를 높였습니다.

가장 위계가 높은 것은 ‘Create’ 버튼으로 보입니다. 강렬한 파란색 버튼으로 그리게 되면서 해당 화면에서 가장 높은 시각적 위계(시각적인 자극)을 보였습니다. 이렇듯 조형적 요소와 더불어 색깔로도 위계를 구현할 수 있는 것입니다.

Quick Filter 개수와 동일한 색깔을 가지지만, 면적 상 create 버튼이 더 높은 위계를 가지게 됩니다.

만약 토스처럼 3d 그래픽으로 스토리나 에픽 아이콘을 만들었다면 위계상 이상해질 것 같네요.

![modu-example.png](assets/img/posts/modu-example.png)

모두싸인의 내 문서함도 비슷한 기조를 가집니다.

item과 사용량 progress bar는 선으로 구현되어 있습니다. 데이터 추출 버튼, 도움말 버튼도 선으로 구현되어있어 위계가 낮아보입니다.

다만, GNB, 문서함 필터 등은 면으로 구성되어 있어 눈에 많이 띄게 되죠.

특히, 서명 요청 버튼은 CTA(call to action)를 의도한 것으로 보이며 색깔도 강렬하여 가장 높은 위계를 가집니다.

또, dropdown이 열린 문서의 경우는 shadow가 추가된 plane으로 표현하여 ‘이미 선택된 문서’에 대한 위계를 다른 문서보다 높게 가져갑니다.

문서함 서비스에서 현재 ‘실제 이미지’를 넣은 곳은 없습니다. 넣는다해도 ‘서명 요청 버튼’의 위계보다 높아질 우려가 있어 대부분 그래픽 디자인으로 처리할 것 같습니다.

이 관점에서 status chip (아니면 Badge)의 디자인이 바뀐 이유를 생각해보았습니다.

https://modusign.notion.site/8397c6724d7142ce824d66be92bf8445#b79196053d2a4e419b907db37ff032d8

문서의 상태 chip이 작은 아이콘과 텍스트로 구성되었는데, 좀 더 면적이 넓은 면으로 수정되고 색깔도 변경되었습니다.

이전에는 문서 제목과의 위계가 비슷하여 정보를 인식하는 순서가 비슷했고, 색깔 구분이 쉽지 않았습니다.

변경된 후에는 ‘면’의 요소가 더 강화되고 색깔로 더 선명하게 바뀌어서 ‘문서 제목’보다 높은 위계를 가지게 되었습니다. 이에 따라 사람들은 문서 상태를 보다 먼저 인식하게 될 것입니다.

### 참고자료

---

[https://pirrcreatives.com/point-line-and-plane-the-building-blocks-of-graphic-design/](https://pirrcreatives.com/point-line-and-plane-the-building-blocks-of-graphic-design/) 
[https://brunch.co.kr/@cliche-cliche/25](https://brunch.co.kr/@cliche-cliche/25)
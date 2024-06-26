---  
tags:  
  - ownership  
  - reflection  
share: "true"  
github_title: 2023-08-13-where-does-ownership-come-from  
title: 오너십은 어디에서 오는가  
date: 2023-08-13  
categories:  
  - Development  
  - General  
---  
###  배경  
  
---  
  
내가 짠 코드들을 둘러보면서 회고를 하던 도중, ‘이때 이런 것 했었지, 개선해보면 좋겠다’ 라고 생각되는 코드가 있었던 한편, ‘내가 이런 코드를 짰었나’ 라는 코드도 있었다.  
  
진행했던 프로젝트마다 기억나는 정도가 달랐는데, 단순히 시간의 문제는 아닌 것 같았다.  
  
작성한 코드의 오너십의 차이가 나는 것이었다. 과연 오너십은 어디에서 오는 것인가  
  
### 요약  
  
---  
  
1. 내가 작성한 코드  
    - 오너십을 가지기 위한 필요조건이라고 생각한다. 어떤 코드에 책임감을 갖고, 주인의식을 가지기 위해서는 최소한 어떤 방식으로든 기여를 하는 것이 필요하다는 생각이 들었다. 내가 짜지 않은 코드에 오너십을 가지기란 쉽지 않다.  
    - 그러나 충분조건은 아니다. 아무리 내가 짠 코드라도, 오너십을 갖게 되는 정도에는 분명한 차이가 있다. 예를 들어, SI 업체처럼 남이 시켜서 며칠동안 짜고 내 손을 떠난 코드는 내가 작성한 코드라도 오너십을 가지기 힘들 것이다.  
2. 내가 소유한 코드  
    - 나의 소유가 된 코드는 오너십을 가질 수 있는가? 코드를 수정하기 위해서는 나의 리뷰가 필요하고, 해당 도메인을 건드릴 때마다 나의 의사가 들어간다면, 오너십을 가질 수 있을까? 분명히 내가 지속적으로 관리하고 의견을 내야하는 도메인이 생기면 주인의식이 느껴질 것 같다.  
    - 하지만, 현재 다니고 있는 회사에서는 아직 ‘이렇다할 소유권’이 없다. 내가 최근에 작성했으면 어느정도 명시적인 소유권을 가지는 것이지, 내가 이 코드를 공식적으로 소유한다는건 없다. 그럼에도 나는 오너십을 느끼고 있기 때문에 가장 큰 요소는 아니라고 생각했다.  
3. 의사결정 과정에 내가 관여한 코드  
    - 가장 중요한 것은 ‘**해당 코드를 짜기 위한 의사결정을 할 때 내가 얼마나 관여했냐**’ 라고 생각한다. 내가 어떤 의사결정을 했다는 것은 그 후에 그에 따른 결과를 책임지겠다는 의미이다. 따라서, 내가 해당 코드를 짤 때 의사결정을 많이 했을수록 자연스럽게 그 코드의 오너십이 커지는 것 같다. 실제로, 이미 의사결정이 완료되어 단순 구현만 한 코드와 도메인 수준에서부터 열심히 조사하고 의사결정에 참여한 코드의 오너십은 크게 달랐다.  
    - 나(폴스)만의 성향일수도 있지만, 제품의 어떤 기능을 만들겠다고 할 때 킥오프부터 하나하나 의견을 낸 비율이 높을수록 해당 코드의 오너십이 높아지는 것 같다. 즉, 제품의 어떤 기능을 만들기 시작하는 단계에서 적극적으로 참여할수록 그 코드에 대해 오너십을 가지기 쉬워지고, 좋은 엔지니어링 문화로 이어질 수 있을 것이다.  
    - 비단 코드 자체뿐만 아니라, 제품의 기능에 대한 오너십에도 비슷하게 적용되는 것 같다.  
  
**결론: 내가 의사결정에 큰 비율로 참여하여 내 손으로 짠 코드가 오너십을 느끼기 가장 좋다.**  
  

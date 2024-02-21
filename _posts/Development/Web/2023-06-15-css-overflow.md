---
tags:
  - css
  - overflow
share: "true"
github_title: 2023-06-15-css-overflow
title: css overflow의 우선순위
date: 2023-06-15
categories:
  - Development
  - Web
---
### Introduction
---

사이드바 UI를 작업하는데, ContextMenu는 사이드바 가로를 튀어나와서 표시되도록 설계하였다.

이를 위해선 overflow: visible이 설정할 필요가 있다.

설정했더니, 컴포넌트 가로에 맞춰서 잘리고 스크롤이 생기는, overflow:auto 가 설정되었다.

난 분명 명시적으로 overflowX: visible라고 알려줬는데, 왜 스크롤이 생기는 것일까?

### 요약
---

[https://www.w3.org/TR/2007/WD-css3-box-20070809/#overflow1](https://www.w3.org/TR/2007/WD-css3-box-20070809/#overflow1)

2018년 이전에 게시된 웹 표준 툴에서, overflowX나 overflowY 둘 중 하나가 visible이고 다른 하나가 visible이 아니라면, visible은 다른 한쪽의 값으로 계산된다고 한다.

> The computed values of ‘overflow-x’ and ‘overflow-y’ are the same as their specified values, except that some combinations with ‘visible’ are not possible: if one is specified as ‘visible’ and the other is ‘scroll’ or ‘auto’, then ‘visible’ is set to ‘auto’. The computed value of ‘overflow’ is equal to the computed value of ‘overflow-x’ if ‘overflow-y’ is the same; otherwise it is the pair of computed values of ‘overflow-x’ and ‘overflow-y’.

자세한 이유는 없지만, overflow라는 값이 overflow-x와 overflow-y로 계산되는데 가로는 스크롤이 가능하면서 세로는 튀어나오도록 보여주는 것이 부자연스럽다고 생각한 것 같다. 계산하는 방식도 어려운 것 같기도 하고.

2018년의 페이지에서는 해당 내용이 없어졌지만 현재까지도 적용되어있다.

이런 문제는 사이드바 기능을 구현할 때 자주 발생할 것 같은데 참고하길 바랍니다.

→ 해결방법

```
#wrapper {
    height: 100px;
    overflow-y: visible;
}
#content {
    width: 200px;
    overflow-x: auto;
}ㅑ
```

inner-container를 하나 더 만든 후, 이곳에는 ‘높이와 overflow-Y’, 그 안의 내용 컨테이너에는 ‘가로와 overflow-X’를 적용하는 trick이 있다.

### 참고자료
---

[https://stackoverflow.com/questions/6421966/css-overflow-x-visible-and-overflow-y-hidden-causing-scrollbar-issue](https://stackoverflow.com/questions/6421966/css-overflow-x-visible-and-overflow-y-hidden-causing-scrollbar-issue)

[https://www.w3.org/TR/2007/WD-css3-box-20070809/#overflow1](https://www.w3.org/TR/2007/WD-css3-box-20070809/#overflow1)
---  
tags:  
  - border-radius  
  - css  
share: "true"  
github_title: 2023-02-10-border-radius  
title: border radius는 어떻게 계산될까  
date: 2023-02-10  
categories:  
  - Development  
  - Web  
---  
  
### 찾아보거나 알게된 배경  
---  
  
코드를 보던 중, 어떤 box의 borderRadius가 {100%}으로 설정되어있었습니다.  
  
borderRadius에 값이 들어가면 어떻게 계산되어 나오는 것인지 궁금했습니다. 특히, x와 y가 다를때 어떻게 될지 궁금했습니다.  
  
![](/assets/img/posts/Pasted%20image%2020240610100512.png)  
  
기본적으로, borderRadius의 시작점은 (꼭짓점)에서부터 (설정한 거리) 만큼 떨어진 위치를 기준으로 합니다.  
  
이때, pixel 단위로 주면 고정 반지름이 적용되고, %로 주면 전체 width(또는 height)에 대한 비율로 위치가 선정됩니다.  
  
![](/assets/img/posts/Pasted%20image%2020240610100533.png)  
  
x와 y값을 서로 다르게 준 경우, 타원을 통해 border-radius를 그리게 됩니다.  
  
![](/assets/img/posts/Pasted%20image%2020240610100549.png)  
  
만약 (전체 width) < (border-radius) 라면 어떻게 될까요?  
  
이 경우 border-radius는 값을 계산할 수 있는 것들 중 최댓값인 50%에 맞추어 계산을 하게 됩니다.  
  
border-radius가 50%라면, 직사각형의 각 꼭짓점이 border-radius의 시작점이 되기 때문에 전체 직사각형은 타원의 모양을 하게 될 것입니다. 이를 넘어가도록 border-radius를 설정할 수 없는것을 그림을 그려보면 알 수 있습니다.  
  
따라서, 우리가 border-radius에 100%를 주던, 50% 주던, 모두 타원이 그려지게 될 것입니다.  
  
근데 타원 픽셀은 어떻게 해서 계산되는 것일까요? 그건 다음 TIL에서 알아보도록 하겠습니다.  
  
### 참고자료  
  
---  
  
[https://developer.mozilla.org/en-US/docs/Web/CSS/border-radius](https://developer.mozilla.org/en-US/docs/Web/CSS/border-radius)  
  
[https://prykhodko.medium.com/css-border-radius-how-does-it-work-bfdf23792ac2](https://prykhodko.medium.com/css-border-radius-how-does-it-work-bfdf23792ac2)
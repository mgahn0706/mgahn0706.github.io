---  
tags:  
  - css  
share: "true"  
github_title: 2023-06-13-difference-between-align-content-and-align-items  
title: alignContent와 alignItems의 차이  
date: 2023-06-13  
categories:  
  - Development  
  - Web  
---  
  
솔직고백: 두 개 차이 모르게 그냥 `구현이 잘되는 방식`으로 썼다.  
  
item 들을 세로로 정렬하는 두 방식의 차이에 대해 알아보기로 했다.  
  
### 요약  
  
---  
  
> align-items는 flex-container 안에서 **전체 item의 배치**를 어떻게 할 것이냐에 대한 속성이다.  
>   
> align-content는 flex-container에서 **item의 줄 간격**을 어떻게 배치할 것이냐에 대한 속성이다.  
  
  
![](../../assets/img/posts/Pasted%20image%2020240717145319.png)  
→ flex에서 아무 속성 없이 아이템들을 적용하면 위와 같이 됩니다.  
  
![](../../assets/img/posts/Pasted%20image%2020240717145351.png)  
  
→ align-items: center를 준다면 위와 같이 전체 item들이 가운데에 들어가게 됩니다.  
  
![](../../assets/img/posts/Pasted%20image%2020240717145416.png)  
  
→ 만약 item들이 늘어다 2줄이 된다면, align-items: center인 경우 위와 같이 각 줄마다 가운데에 정렬되는 모습이 나오게 됩니다. (flex-wrap: wrap인 경우)  
  
가운데 줄 간격이 보기 싫다. 나는 저 아이템들이 진짜 ‘container의 가운데’에 왔으면 좋겠다 할때 ‘align-content’를 사용합니다.  
  
![](../../assets/img/posts/Pasted%20image%2020240717145435.png)  
  
→ align-content: ‘center’인 경우 위와 같이 의도한대로 잘 나타나집니다.  
  
여태까지 2줄 이상의 아이템을 다룰 일이 크게는 없었던 것 같다. 그래서 아무거나 써도 잘 되었던 것이다.  
  
### 참고자료  
  
---  
  
[https://stackoverflow.com/questions/27539262/whats-the-difference-between-align-content-and-align-items](https://stackoverflow.com/questions/27539262/whats-the-difference-between-align-content-and-align-items)  
  
[https://www.inflearn.com/questions/752797/align-items-vs-align-content](https://www.inflearn.com/questions/752797/align-items-vs-align-content)
---  
tags:  
  - css  
  - grid  
share: "true"  
github_title: 2023-02-21-fr-and-repeat-in-grid  
title: Grid에서 fr 단위와 repeat()의 사용  
date: 2023-02-21  
categories:  
  - Development  
  - Web  
---  
**What is CSS-grid?**  
  
CSS 그리드는 2차원의 레이아웃 시스템으로, column과 row 기반이다.  
  
![](/assets/img/posts/Pasted%20image%2020240718115014.png)  
  
각 행과 열 사이에 공백을 줄 수 있는데, 이를 `gutter` 라고 합니다.  
  
ex)  
  
```css  
.container{  
	display: grid;  
	grid-template-column: 100px 100px 100px;  
}  
```  
  
이렇게 짜면 100px 짜리 column 3개가 있는 grid가 생성됩니다.  
  
**What is fr unit?**  
  
위의 예시처럼 절댓값을 이용해 각 행(또는 열)을 설정할 수 있지만, 비율을 통해서도 grid를 그릴 수 있습니다. 그냥 px 값을 넣은 것과의 가장 큰 차이는 각 column이 가변적이라는 것입니다.  
  
ex)  
  
```css  
.container{  
	display: grid;  
	grid-template-column: 1fr 2fr 1fr;  
}  
```  
  
위의 코드는 사용 가능한 공간을 1:2:1의 비율로 나눕니다.  
  
예를 들어, container의 전체 가로 길이가 400px이라면, 100px 200px 100px을 가로길이로 가지게 되는 것입니다.  
  
**repeat() 함수 사용**  
  
만약 만들고자 하는 행의 개수가 8개고, 1 : 1 : 1 : 1 : 1 : 1 : 1 : 1 의 비로 나누고 싶다면 어떻게 코드를 짜야할까요?  
  
```css  
.container{  
	display: grid;  
	grid-template-column: 1fr 1fr 1fr 1fr 1fr 1fr 1fr 1fr; // too long  
}  
```  
  
너무 길다. 깔끔하게 처리할 수 없을까 → repeat()를 쓰자  
  
사용법: repeat(반복 횟수, 값);  
  
```css  
.container{  
	display: grid;  
	grid-template-column: 'repeat(8, 1fr)';  
```  
  
훨씬 간편해졌다.  
  
### 참고자료  
  
---  
[https://developer.mozilla.org/ko/docs/Learn/CSS/CSS_layout/Grids](https://developer.mozilla.org/ko/docs/Learn/CSS/CSS_layout/Grids)
---  
tags:  
  - html  
  - css  
share: "true"  
github_title: 2023-04-11-sibling-selector  
title: Sibling selector ( +, ~ )  
date: 2023-04-11  
categories:  
  - Development  
  - Web  
---  
  
### 요약  
  
---  
  
- `+` **Adjacent sibling combinator (인접 형제 선택자)**  
    - `A+B` 는 A 바로 뒤에 오는 B element를 선택합니다.  
  
```html  
.A + .B {  
	color: red;  
}  
  
<div class='A'>A</div>  
<div class='B'>B1</div> // 얘만 적용되어서 색깔이 변함  
<div class='B'>B2</div> // 얘는 인접해있지 않아서 변하지 않음  
```  
  
  
  
- `~` **General sibling combinator (일반 형제 선택자)**  
    - `A~B` 는 A 다음에 오는 B 모두를 선택합니다. (동일한 부모를 가지고 있다면)  
  
```html  
.A ~ .B {  
	color: red;  
}  
<div class='B'>B0</div> // 얘는 이전에 있으니 안나오고  
<div class='A'>A</div>  
<div class='B'>B1</div> // 얘만 적용되어서 색깔이 변함  
<div class='B'>B2</div> // 얘도 변함  
```  
  
~를 사용하면 꼭 인접하지 않아도, A 뒤에 오는 B들 모두 선택이 됩니다.  
  
  
### 참고자료  
  
---  
  
[https://w3c.github.io/csswg-drafts/selectors/#class-html](https://w3c.github.io/csswg-drafts/selectors/#class-html)
---  
tags:  
  - d3  
  - visualization  
  - info-vis  
  - javascript  
  - react  
  - abstraction  
share: "true"  
github_title: 2025-10-21-programming-visualizations  
title: 9. Programming Visualizations  
date: 2025-10-21  
categories:  
  - Lecture Notes  
  - Information Visualization and Visual Analytics  
---  
## Web Technology & JavaScript  
  
- HTML: structure of web page  
- CSS: style  
- Javascript: functionalities  
- DOM  
    - Programming interface of HTML document  
    - document as node and object  
- Web browser는 DOM 파싱 후 (사실 엄청 많은 과정이 있지만…) 이를 html 코드로 바꾼다.  
  
여긴 너무 많이 들었던 부분이라 패쓰..  
  
## D3 and React  
  
### D3  
  
Data driven documents.  
  
- Web based js library for manipulating DOM object  
  
### React  
  
- JavaScript Library  
- SPA  
- Component-wise programming, modularization  
    - by JSX  
- Virtual DOM!  
  
## Why D3? Why React?  
  
- Component & UI Structure → React  
- Detailed Visualization Design → D3  
  
사실 이렇게만 말하면 frontend framework를 쓰는 이유정도밖에 설명이 안되어서, flux pattern과 virtual dom, component-wise programming을 통한 UI 재사용을 들어야할 것 같지만 넘어가자  
  
## How to use D3 with React  
  
### yarn  
  
- JavaScript package manager  
  
## React  
  
### React Hook  
  
- React 16에서 등장  
- class 컴포넌트에서 함수 컴포넌트 방식으로 넘어왔는데, 여기서 로직, 특히 상태관련 로직이나 다른 life cycle 관련 사이드 이펙트를 처리하기 쉽게해줌.  
  
### Sepraration of Concerns (관심사분리)  
  
- React는 UI를 컴포넌트로 나누어 관심사를 분리한다.  
    - html, css, js 와 같이 나누던 separation of technology와는 다름  
  
### JSX  
  
- js xml.  
- document structure 정의 위해서 사용하는, 템플릿 언어  
  
### Components  
  
(= single function that returns a JSX object)  
  
### Props  
  
- Parent component가 자식 컴포넌트에 넘겨주는 값들.  
    - 가장 간단한 의존성 주입 방식.  
  
### States  
  
- 훅으로 관리 가능한, 해당 컴포넌트의 상태.  
- 하나의 세계라고 보면 편함  
  
### One-way Data binding  
  
- achieved by props. tree-like structure  
    - 위 상태가 바뀌면 다시 그린다.  
  
## State vs. Local variable  
  
State → Render components  
  
local variable → do not trigger rerendering  
  
→ D3는 컴포넌트 리렌더를 발생시키지 않음. update가 internally로 일어나면 local variable이 더 적절하다  
  
(옮긴이 주. 정확히는 렌더링과 관계 없는 값. 화면 업데이트와 관계없는 값은 local variable. 나머지는 useState가 더 좋은 설명일 듯. update가 internally 일어나도 렌더링은 가능할 수 있기 떄문)  
  
---  
  
### useRef  
  
값은 유지되나, 값이 바뀌어도 렌더링이 일어나지는 않음. (렌더링 이전 참조 불가)  
  
### useEffect  
  
- 사이드 이펙트 관리.  
- <svg/> 렌더 이후에 해당 DOM을 조작할 수 있으므로, UseEffect 내에서 DOM 조작해야함  
  
### React Hooks Life Cycle  
  
프론트엔드 개발에서 정말 중요한 개념인데… 이 수업에서 시험에 나올진 모르겠다  
  
![image.png](attachment:7fc8c2da-72db-433f-8ee7-fb6f7770d92a:image.png)  
  
- Render phase (마운트, 또는 업데이트 처리)  
- Commit phase (사이드 이펙트 처리, DOM 조작)  
- Cleanup phase (메모리누수 방지)  
  
---  
  
### SVG  
  
- Scalable vector graphics  
- Can be embedded and modified  
  
### Selection  
  
```tsx  
d3.select(selector)  
selection.attr(name[,value])  
d3.selectAll(selector)  
  
selection.data([data[, key]])  
  
// example  
let data = [1,2,3];  
let selection =  d3.selectAll("rect").data(data)  
selection.enter().append('rect')  
				.attr('width', 30)  
				.attr('height', 20)  
				.attr('transform', (d, i)=> 'translate');  
				  
selection.exit().remove();  
  
```  
  
![image.png](attachment:64c24c6e-af23-4ee1-b380-11e466e85101:image.png)  
  
### Interaction  
  
```tsx  
useEffect(()=> {  
	const rect = d3.select (svgRef.current).select('rect')  
	rect.on("mouseenter", () => {  
		d3.select(this).attr("fill", "red");  
	});  
},[])  
```  
  
### Transition  
  
enables animation  
  
```tsx  
const rect = d3.select(svgRef.current).select("rect");  
rect.transition()  
		.delay(500)  
		.duration(3000)  
```  
  
### Brushing  
  
Masking an enclosed region va mouse interactions  
  
d3-brush  
  
### Linking  
  
- Connecting multiple visualizations.  
- Strategy: implement single event handler  
  
---  
  
## D3  
  
- D3 is a bundle of libraries  
  
### Plot  
  
- Higher level wrapper package of D3  
  
### Vega-Lite  
  
- High-level visualization language for JS  
  
---  
  
### Utilizing LLMs  
  
(경험적으로 다 아는거지만…)  
  
- modular code, short file  
- specify tasks  
- one function at a session.
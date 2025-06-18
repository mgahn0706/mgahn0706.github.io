---  
tags:  
  - javascript  
share: "true"  
github_title: 2024-02-16-foreach-does-not-wait  
title: forEach는 기다리지 않는다  
date: 2024-02-16  
categories:  
  - Development  
  - Web  
---  
e2e 테스트를 할 때, 각 인풋마다 값을 입력해주는 행동을 하는 함수를 정의했다.  
  
받아온 배열을 forEach를 통해 비동기로 누르도록 했다.  
  
나는 각 배열마다 비동기함수가 순차적으로 진행되는 것을 기대했는데, e2e 결과를 보니 뭔가 순서가 이상했다.  
  
### 요약  
  
---  
  
이유: forEach method는 synchronous function만 기대하기 때문이다.  
  
즉, forEach를 사용하면 promise를 기다리지 않는다.  
  
> `forEach()` expects a synchronous function — it does not wait for promises. Make sure you are aware of the implications while using promises (or async functions) as `forEach` callbacks.  
  
forEach 입장에서는 사실 callback이 뭐가 오든 iterative하게 callback을 실행하기 때문에 promise가 성공/실패 할 때까지 기다리지 않는건 당연한 것이다.  
  
```jsx  
if (window.NodeList && !NodeList.prototype.forEach) {  
  NodeList.prototype.forEach = function (callback, thisArg) {  
    thisArg = thisArg || window;  
    for (var i = 0; i < this.length; i++) {  
      callback.call(thisArg, this[i], i, this);  
    }  
  };  
}  
```  
  
polyfill을 봐도 단순 for문 실행해주는 method인 것이다.  
  
~~찾아보니 프론트엔드 면접 국룰 질문이라고 한다. 흑흑~~  
  
그렇다면 for 문으로 사용해서 block 함수를 만들면 되는 것일까  
  
[https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for-await...of](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for-await...of)  
  
찾아보니 for awiat of는 [async iterator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Iteration_protocols#the_async_iterator_and_async_iterable_protocols) object를 순회하는 Loop을 만들어준다고 한다.  
  
다수의 비동기 함수를 처리할 때, 이번 e2e 케이스와 같이 하나하나를 기다려야하는 경우에는 for await … of 구문이 유용한 것을 알았다.  
  
참고자료  
  
---  
  
[https://developer.mozilla.org/ko/docs/Web/API/NodeList/forEach](https://developer.mozilla.org/ko/docs/Web/API/NodeList/forEach)
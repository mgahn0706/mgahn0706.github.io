---  
tags:  
  - react  
share: "true"  
github_title: 2023-02-01-use-sync-external-store  
title: useSyncExternalStore  
date: 2023-02-01  
categories:  
  - Development  
  - Web  
---  
### 요약  
  
---  
  
useSyncExternalStore은 React 18에 새롭게 나온 훅입니다.  
  
해당 훅은 concurrent rendering에서 사용자 인터렉션에 대한 부분을 먼저 렌더링하면서 발생할 수 있는 렌더 트리 안에서의 차이(tearing)를 해결할 수 있습니다.  
  
useState와 같이 리액트에서 제공하는 상태관리 도구들은 이런 concurrent rendering에서 발생하는 tearing을 처리할 수 있도록 구현되어있습니다. 하지만, redux같이 외부 상태관리 도구(external store)에서는 문제가 발생할 수 있습니다.  
  
![](../../assets/img/posts/Pasted%20image%2020240717150652.png)  
  
용법  
  
```jsx  
  
import { useSyncExternalStore } from 'react';  
import { todosStore } from './todoStore.js';  
  
function TodosApp() {  
  const todos = useSyncExternalStore(todosStore.subscribe, todosStore.getSnapshot);  
  // ...  
}  
```  
  
이렇게 하면 React는 콜백함수로 넘겨진 함수를 구독할 것이고, 변경사항이 있을 시 리렌더해줄 수 있을 것입니다.  
  
### 참고자료  
  
---  
  
[https://beta.reactjs.org/reference/react/useSyncExternalStore](https://beta.reactjs.org/reference/react/useSyncExternalStore)  
 [https://velog.io/@jay/useSyncExternalStore](https://velog.io/@jay/useSyncExternalStore)
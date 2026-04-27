---  
tags:  
  - web  
  - hook  
share: "true"  
github_title: 2026-04-27-use-effect  
title: useEffect 실수 바로잡기  
date: 2026-04-27  
categories:  
  - Development  
  - Web  
---  
## 찾아보거나 알게된 배경  
  
React를 쓰다 보면 자연스럽게 `useEffect`를 남발하게 된다.  
실제로 React를 처음 배울 때 상태 관리와 흐름에 익숙하지 않게 되고, 뭔가 상태가 내 마음대로 바뀌지 않을 때 `useEffect`를 사용하게 된다. 그리고 그렇게 짜게되면, 대개 잘 돌아가는 것처럼 보이기 일쑤이다.  
  
사실 AI 시대에 이걸 이해하지 않고 사용해도 알아서 잘 짜주겠지만...  
`useEffect`는 특히나 잘못 사용하기 쉬운 hook인 것 같다.   
맹목적으로 사용하다간ㄴ 어느 순간부터는 그냥 “뭔가 바뀌면 실행해야 할 것 같아서” 넣게 된다.  
  
이번에는 React 공식 문서인 You Might Not Need an Effect 를 기반으로    
정말로 언제 필요한지, 그리고 왜 대부분의 경우 필요 없는지 정리해보려고 한다.  
  
---  
  
## 요약  
  
- `useEffect`는 렌더링과 “외부 세계”를 동기화하기 위한 도구  
- 내부 상태 로직을 처리하기 위해 쓰는 순간 대부분 잘못된 사용  
- 많은 경우는    
    → 계산으로 해결 가능하다  
    → 이벤트 핸들러로 해결 가능하다    
    → state 구조를 바꾸면 해결 가능하다  
  
하나하나 알아보자.  
  
---  
  
## useEffect의 본질  
  
React에서 렌더링은 순수 함수처럼 동작해야 한다.  
  
즉, 같은 props나 state에 의해서 → 같은 UI가 그려져야 한다!  
  
그런데 현실에서는...  
  
- 서버에서 데이터 가져오기  
- DOM 직접 조작  
- 외부 라이브러리 연결  
등을 해야할 때가 있는데, 이건 React 내부에서 해결할 수가 없다. DOM을 직접 조작하는걸 리액트 내부에서 처리하기가 힘들다는 것이다.  
  
그래서 `useEffect`가 “React 외부와 동기화”를 위해 나왔고, 이 역할이 아닌 useEffect의 사용은 (대부분) 안티패턴으로 봐도 무방하다.  
  
---  
  
## 우리가 실제로 하는 잘못된 사용  
  
  
우리는 종종 이런 코드를 쓴다:  
  
```  
const [fullName, setFullName] = useState('');    
    
useEffect(() => {    
  setFullName(firstName + ' ' + lastName);    
}, [firstName, lastName]);  
```  
  
겉보기에는 자연스럽지만 구조적으로 보면:  
  
state → effect → state 업데이트 → re-render  
  
즉, 불필요한 렌더링을 한 번 더 만든다.  
  
---  
  
## 계산으로 해결 가능한 경우  
  
위 코드는 그냥 이렇게 쓰면 된다:  
  
```  
const fullName = firstName + ' ' + lastName;  
```  
  
---  
  
## “동기화 착각” 문제  
  
많은 사람들이 이렇게 생각한다:  
  
“A가 바뀌면 B도 같이 바뀌어야 하니까 useEffect 써야지”  
  
하지만 이건 대부분 derived state로 해결이 가능하다.  
예를 들어,   
  
const [filtered, setFiltered] = useState([]);    
    
useEffect(() => {    
  setFiltered(items.filter(...));    
}, [items]);  
  
위와 같은 코드는 언뜻 item이 바뀌면 필터된 상태를 바꿔야한다는 우리의 직관과 맞아보인다. 하지만 아래와 같이 쓰는 게 리액트의 의도에 더 맞다.  
  
const filtered = items.filter(...);  
  
상태를 하나 더 두는 순간 복잡도와 버그 가능성이 증가한다.  
  
---  
  
## 이벤트 vs Effect  
  
또 다른 흔한 실수는 다음과 같다.  
  
useEffect(() => {    
  if (submitted) {    
    sendData();    
  }    
}, [submitted]);  
  
언뜻 '제출하고자 하는 값'이 변경되면 sendData를 하라는, 간단한 함수고 틀린게 없어보인ㄷ. 하지만 이건 이벤트에서 처리해야 한다:  
  
function handleSubmit() {    
  sendData();    
}  
  
차이는 effect는 이미 일어난 변화에 대해 사이드 이펙트를 처리하는 것이지만 event는 사용자 행동에 반응한다는 점이다. 값을 제출하는건 결과적인게 아니라 유저의 행동이므로, event로 처리하는 게 더 맞다.  
  
  
---  
  
## useEffect가 진짜 필요한 순간   
  
여기까지 읽었다면 '그럼 왜 만들었고 언제쓰냐'라는 질문이 자연스레 따라오게 된다.  
  
다음 경우에는 useEffect가 필요하다.  
  
### 1. 외부 시스템과 연결  
  
useEffect(() => {    
  const connection = connect();    
  return () => connection.disconnect();    
}, []);  
  
### 2. 데이터 fetching  
  
useEffect(() => {    
  fetch('/api/data').then(setData);    
}, []);  
  
### 3. DOM 직접 조작  
  
useEffect(() => {    
  document.title = title;    
}, [title]);  
  
---  
  
## 핵심 정리  
  
useEffect를 쓰기 전에 이 질문 하나면 충분하다!  
  
“이건 React 외부와 관련 있는가?”  
  
- 그렇다 → useEffect  
- 아니다 → 다른 방법  
  
사실 요즘 데이터 페칭이나 외부 라이브러리도 자체적인 hook을 제공하지, 사용자가 useEffect를 쓰는 일은 더더욱 없다.   
  
useEffect를 직접 작성할 일은 정말 없다. 오히려 useEffect를 잘 활용한 커스텀 훅을 써서 useEffect 자체가 밖으로 잘 드러나지 않게 하는 게 좋을 것 같다.  

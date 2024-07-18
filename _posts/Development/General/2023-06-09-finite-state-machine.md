---  
tags:  
  - redux  
  - state  
share: "true"  
github_title: 2023-06-09-finite-state-machine  
title: Finite State Machine  
date: 2023-06-09  
categories:  
  - Development  
  - General  
---  
[https://ko.redux.js.org/style-guide/#treat-reducers-as-state-machines](https://ko.redux.js.org/style-guide/#treat-reducers-as-state-machines)  
  
- Redux는 finite-state-machine처럼 다뤄지면 좋다고 합니다.  
  
→ Finite-State machine(이하 FSM)이 뭘까요?  
  
## Sequential Logic과 Combinational Logic  
  
전기전자 분야의 로직 게이트를 다루다보면, 2가지 로직 설계가 있습니다.  
  
Sequential Logic과 Combinational Logic입니다.  
  
Sequential Logic은 state가 존재합니다. Combinational Logic과 달리 로직을 통과한 데이터 일부가 다시 로직에 들어가면서 만들어지게 되죠.  
  
이렇게 만들어진 현재 state와 들어온 인풋에 맞춰서 output을 내는 모듈이 sequential logic인 것입니다.  
  
리액트 코드로 따지면 이런거겠죠  
  
```tsx  
const getName = (input: string) => {  
	return input+'님';  
}  
```  
  
이게 combinational이고  
  
```tsx  
const [name, setName] = useStae('');  
  
const onChangeName = (input: string) => {  
	setName(input + name + '님');  
}  
```  
  
이게 sequential입니다. 순서가 존재한다는게 보이시나요?  
  
TMI: 리액트는 상태에 따라 다시 컴포넌트를 그리는 방식인데, low-level에서는 일정한 주기마다 on되는 clock 인풋을 주면, 다음 상태에 해당하는 값이 현재 상태에 반영됩니다. 여기서 D-flip flop이라는 걸 이용합니다.  
  
## FSM diagram  
  
이렇게 만들어진 state는 전기전자공학 분야에서는 아직까진 유한할겁니다. 아웃풋 비트와 인풋비트 수가 정해져있거든요. 그러면 유한한 상태가 만들어 지고 우리는 이걸 다이어그램으로 작성할 수 있습니다.  
  
이렇게 각 상태에 따른 출력과 상태가 변경되는 조건, 유한한 이벤트(리덕스에서 액션)이 있으면 초기상태가 주어졌을때 OUT과 NEXT_STATE만 있다면 모든 상태를 제어할 수 있습니다.  
  
## **리덕스에서 왜 fsm을 강하게 권고할까요?**  
  
FSM을 만든다는 마인드를 통해 우리는 예상치못한 값이 오는걸 방지하고, 불가능한 상태가 되는것을 막을 수 있습니다.  
  
예를 들어, 요청을 보낼 때입니다.  
  
상태는 pending, idle, succeed, failed라고 합니다.  
  
우리는 success시에 결괏값이 당연히 있어야한다고 생각합니다. pending에서는 로딩스피너가 돌아야한다고 생각하고요.  
  
success인데 값이 없거나, 갑자기 pending에서 idle로 가거나, failed이면서 succeed이거나 하는 상황이 없어야겠죠.  
  
우리는 finite state machine으로 리덕스를 다루고 설계하면서 안전하고 예상가능한 코드를 짤 수 있게됩니다.  
  
타입스크립트를 사용하면 위의 마인드셋이 좀 더 유리한데요, success일때만 value가 존재해야함을 type을 통해 제한해줄 수 있기 때문입니다. 각 상태에 따른 타입을 제한해주면서, 우리는 상태에 따라 자연스럽게 분리된 타입을 쓸 수 있어요.  
  
## TMI: Moore Machine and Mealy Machine  
  
moore machine은 ‘현재 상태’만이 다음 상태에 영향을 줍니다. 예를 들어 서명을 전송할 때 작성중인 서명은 ‘다음 상태’는 ‘현재 상태인 작성중’에만 의존하여 결정될 것입니다.  
  
한편, Mealy machine은 ‘현재 상태’와 ‘인풋’에 모두 영향을 받습니다. 대량전송에서 ‘진행중’인 작업은 ‘진행중이라는 현재 상태’와 ‘실패 카운트’라는 인풋에 따라 ‘DONE’ 또는 ‘DONE_WITH_FAILURE’로 가게 됩니다.  
  
## 마무리  
  
<aside> 🗣️ 그냥 일어나는 일은 없다. 일어나도록 만들어진 것이다. - John F. Kennedy  
  
</aside>
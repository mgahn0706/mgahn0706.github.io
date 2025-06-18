---  
tags:  
  - hci  
  - evaluation  
  - GOMS  
share: "true"  
github_title: 2025-05-27-evaluation-without-users  
title: 16. Evaluation without Users  
date: 2025-05-27  
categories:  
  - Lecture Notes  
  - Human Computer Interaction  
---  
**Motive**  
  
그… 제꺼 테스트해보고 싶은데 유저가 엄슴다 ㅠㅠ  
  
## Evaluating w.o. users!  
  
### Goal  
  
- Evaluate evolving design when `no users`  
- Catch problems that evaluation with only few users may not reveal  
  
### 1. Cognitive Walkthrough  
  
- Task-oriented technique  
- Path-through interface with pre-determined task and actions  
  
### 2. Action Analysis  
  
- Predict the time for `experts` . (GOMS)  
- Forces the designer to take a detailed look at the interface  
  
### 3. Heuristic Analysis (이번 글의 메인)  
  
- `Interface` oriented (not task)  
- Overall examination, not pre-determined.  
  
---  
  
## Cognitive Walkthrough  
  
A formalized way of imagining people’s thoughts and actions when they use an interface for ‘first time’ → 처음 쓰는 유저 페르소나에 집중하여 evaluation.  
  
→ `Walk up and Use` interfaces.  
  
### Requirements  
  
- 최소한의 UI는 구현되어 있어야힘.  
- Task description  
- Complete, written sequence of actions for completing task.  
  
### What you look for…  
  
- Will user know this action?  
- Will users see this control?  
- Will users know control does what they want? (Seven stages of action에서 Execution bridge에 해당  
  
### How to do cognitive walkthrough  
  
- Prototype 준비  
- 하나의 작업 선정.  
- believable story를 각 액션마다 지음  
  
→ 각 액션마다 believable story가 안나온다면, (뭔짓을 해도 유저가 이거 안누를 것 같다면..) 문제가 있는 거임  
  
---  
  
## Action Analysis  
  
- Allow designer to **predict** the **time** for **expert** to perform a task  
  
→ Too many steps to perform a simple task?  
  
→ Too long to perform task?  
  
→ Too much to learn about the interface?  
  
GOMS를 이용할 수 있으며, 수행시간 예측에 직접적 관련이 있음  
  
---  
  
## Heuristic Analysis  
  
a `usability inspection method` where **expert** evaluates UI against a set of **pre-defined heuristics or principles. (e.g. Normann)**  
  
- Rules of thumb (경험에 의한 규칙) that describes usable system.  
      
    - Design Principles  
    - Evaluate a design  
- 장점  
      
    Easy and inexpensive.  
      
    - Performed by experts  
    - No user required  
    - Catches many design flaws  
- 단점  
      
    More difficult than it seems  
      
    - Not a simple checklist.  
    - Cannot assess how well the interface will address user goals. (단순히 UI 사용성을 평가하지, 유저 목표를 잘 반영하는지는 평가하기 어려움)  
  
## Usability Engineering (Heuristic Evaluation)  
  
by Jakob Nielsen.  
  
- UI 디자인에 대한 disciplined approach 제공  
- 사용성 원리와 방법론에 대한 구조화된 과정을 포함한다.  
  
### We need many inspectors…  
  
Evaluators miss both easy and hard problems  
  
- 물론 좋은 평가자도 쉬운 문제를 놓치기도 하고  
- 안좋은 평가자도 어려운 문제를 발견하기도 한다.  
  
→ 여러 명 써라~ (3에서 5명)  
  
→ Check compliance with `usability principles`  
  
- 각 평가자는 독립된 환경에서 평가  
- 각자 다른 관점에서 여러번 평가  
  
---  
  
### Nielsen’s evaluation phases  
  
1. Pre-evaluation training  
    - Provide the evaluator with `domain` knowledge.  
2. Evaluation  
    - Get a feel for flow  
    - Focus on specific elements  
        - Multiple passes approach  
        - Create a list of all problems  
        - Rate severity  
3. Severity rating  
    - Establish ranking between problems.  
    - Reflects frequency, impact and persistence  
4. Debriefing  
    - Discuss outcome with design team.  
    - Suggest potential solution.  
    - Assess how hard things are to fix  
  
---  
  
## Nielsen’s heuristics: 10 general principles  
  
1. Simple and natural dialog  
2. Speak the users’ language  
3. Minimize user memory load  
4. Consistency  
5. Feedback  
6. Clearly marked exits  
7. Shortcuts  
8. Prevent errors  
9. Good error messages  
10. Provide help and documentation.  
  
---  
  
### Simple and natural dialog  
  
Minimalist design (less is more)  
  
- UI should be `simplified` as much as possible (reduce learning effort & errors)  
- UI should match the users’ task in natural way.  
  
→ Do not use “eye-candy” programs…  
  
- Logical flow에 맞춰서 정보를 보여줘야함  
- Simple is GOOD  
    - 관계가 없거나 거의 필요없는 정보는 없애거나 숨기기. → 좁은 스크린 공간을 싸움.  
    - Use window frugally  
        - Avoid complex window management  
  
---  
  
### Speak the users’ language  
  
- Match the real world!  
    - Use a language compatiblr with users’ conceptual model  
  
→ “Error: Connection timeout due to network congestion” 보다는 “Maximum user exceeded” 정도로 그들의 언어로 말하기.  
  
- Use meaningful icons and abbr.  
  
---  
  
### Minimize user memory load  
  
- **Recognition** rather than **recall**!  
  
→ Recognize things previously experienced.  
  
- Describe **expected input clearly.**  
    - DD-YYYY_MM 등. placeholder의 적절한 사용  
- Promote recognition over recall  
- Create orthogonal command systems  
    - Use small number of pervasive rules throughout UI  
    - 동일한, 일관성있는 규칙을 적용.  
    - 일반적인 command를 사용  
  
---  
  
### Consistency  
  
일관성을 지켜라.  
  
- Command Design  
    - 같은 액션은, 같은 상황에서 같은 효과.  
- Graphic Design  
    - Input format, output format  
- Flow Design  
    - Similar tasks는 유사한 방식으로 control 됨  
  
→ Least surprise to users! Consistency promotes skill aquistion.  
  
---  
  
### Feedback  
  
**Semantic**  
  
“Visibility” of system status  
  
- User should know “What’s going on?”  
  
→ but do not burden users…  
  
- Provide redundant information. 탭 선택 시 탭도 보여주고 커서로도 보여주기  
  
**Time**  
  
- Feedback은 최대한 빨리 줘야한다.  
      
    10s < : User will switch to another task  
      
    10s: Difficult to stay focus  
      
    1s: Delay but user’s flow is uninterrupt  
      
    .1s: Casuality  
      
- Solution?  
      
    - Hourglass cursor, short transaction.  
    - Estimate of time left. (should overestimate)  
  
---  
  
### Clearly marked exits  
  
Mark cleat exit → do not trap users.  
  
Cancle button or esc button for dialog.  
  
Universal undo  
  
---  
  
### Shortcuts  
  
- Flexibility & efficiency  
- For expert users!  
  
EX)  
  
- Keyboard and mouse accelerators  
- Toolbars and tool palettes  
- Navigation jump  
- Macros  
  
---  
  
### Prevent errors  
  
Error prevention > Error handling  
  
- Slips and mistakes  
  
(1) Mistakes (계획 오류)  
  
- Conscious decision with unforeseen consequences  
- 잘못된 mental model로 인해 발생 → 왜 이거 안돼요? 왜 엑셀처럼 안돼요? 이거 왜 안돌아가요? 원래 돼야하는거 아닌가요? << 아오…  
  
(2) Slips (실행 오류)  
  
- 버튼이 너무 작아서, 모드를 잘못 설정해서  
- 위 이유로 발생하는, user know what and how to do but `fail to do it correctly`  
- Misclick!  
  
Slip의 종류  
  
1. Capture error: 1, 2, 3, 4, … 10, J? Q? 너무 익숙하게 사용하는 패턴이라, 자주 사용하는 패턴이 의도한 동작 대신 실행된 경우.  
    - Make action undoable.  
    - Allow reconsideration by modal…  
2. Description Error: Intended action similar to others that are possible. 비슷한 액션을 해버리는 경우., wrong object physically near each other  
    - Rich feedback  
    - Undo  
    - Check for reasonable input  
3. Loss of activation: 엑션을 실행하다가 뭐하려고 했는지 까먹음  
    - If system knows goal, make it explicit.  
    - If not, allow user to see path taken (e.g. Breadcrumb)  
4. Mode error: 모드를 잘못 설정해서 생긴 에러. 그리기나 채우기 모드에 있는 줄 알았는데…  
    - 모드를 적게 만들면 됨 (modeless한게 베스트. 항상 같은 인풋, 같은 결과)  
    - make mode highly visible.  
  
→ Modeless, Undo rather than confirmation, check for reasonable inputs  
  
---  
  
### Forcing functions  
  
- Lockin mechanisms  
    - Keep user in a state until condition is met!  
- Lockout mechanisms  
    - Prevent user entering the state, user should remove constraint before start it.  
- Interlock mechanisms  
    - makes the state of two mechanisms mutually dependent. (전자레인지)  
  
---  
  
### Dealing with errors  
  
1. Ignore them (???)  
2. Correct automatically (ex. autocorrect)  
    - system is not always right  
3. Discuss it  
    1. But novice don’t know anything…  
4. Teach user  
    1. Office assistant  
  
→ Respect users’ feeling!  
  
---  
  
### Good Error messages  
  
Provide meaningful message!  
  
- Explain in the terms of user conceptual model  
- Dont make user feel stupid  
- Offer a way to correct problem  
  
---  
  
### Provide help and documentation  
  
Perpetual Intermediate!  
  
- Tutorial and start manual  
- Reference manual (for experts)  
- Reminders  
    - reference card, tooltips…  
- Show me videos  
- Wizards  
    - Users can feel they are losing control (얘가 뭔갈 다 해주네…)  
- Tips  
- Context sensitive help  
    - What user is working on.  
  
---  
  
## General UI Design Principles  
  
Ben shneiderman  
  
다른건 다 비슷한데 하나 다름  
  
“Cater to `universal usability` ”  
  
→ 특정 페르소나만 만족하는게 아니라 universal한 사용성을 만족하도록.
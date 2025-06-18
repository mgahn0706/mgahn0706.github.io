---  
tags:  
  - hci  
  - conceptual-model  
  - affordance  
  - direct-manipulation  
  - metaphor  
share: "true"  
github_title: 2025-05-14-conceptual-framework  
title: 13. Conceptual Framework  
date: 2025-05-14  
categories:  
  - Lecture Notes  
  - Human Computer Interaction  
---  
### Conceptual Frameworks를 배우자.  
  
- Norman’s seven stages of action model  
- Gulf of execution and Gulf of evalutation  
- Direct manipulation  
- Interface metaphor and mental models  
  
---  
  
### Why conceptual framework?  
  
- They help us `explain` and `predict` user behavior based on theories on **cognition**.  
  
우리는 이 세가지를 잘 align해서 효과적인 인터페이스를 만들어야 한다.  
  
- Design Model 디자이너가 의도한 시스템의 concept  
- User’s Model 유저가 시스템을 보고 이해한 mental understanding  
- System Image 유저에게 인터페이스를 통해 시스템이 보여주는 것  
  
A conceptual model in HCI refers to the **overall structure** and **behavior that the system conveys** to the user - shaping their **mental models.**  
  
---  
  
## Explaining User behavior!  
  
사용자가 시스템과 상호작용하면, 그들은 서로 다른 스테이지로 이루어진 cognitive process를 거친다.  
  
### Conecptual Framework의 장점  
  
(1) Understand how user approach task  
  
(2) Predict where confusion or failure may occur  
  
(3) Improve interface design by addressing these breakdowns.  
  
---  
  
## Norman’s Seven Stages of Action Model  
  
Explain the `cognitive` process of a user while performing a task  
  
### 1. Goal  
  
The desired outcome or state the user wants to reach  
  
“댓글에서 의견들이 뭔지 알고 싶다”  
  
### 2. Intention  
  
Chosen strategy to fulfill the goal  
  
“댓글의 의견 창으로 간다”  
  
### 3. Action Specification  
  
mapping the plan to specific actions, supported by the system  
  
댓글 탭의 ‘의견’ 탭 버튼을 보고 해당 버튼을 클릭해야겠다고 생각한다  
  
### 4. Execution  
  
Physically performing the action  
  
마우스를 움직여 댓글 탭의 ‘의견’ 탭 버튼을 누른다  
  
여기까지 goal - to -action  
  
→ 여기서 user intention과 available action이 잘 매핑이 안되면 breakdown 발생  
  
---  
  
### 5. Perception  
  
Noticing the system’s response  
  
의견 탭으로 이동하며 뜨는 그래프들을 본다  
  
### 6. Interpretation  
  
Understanding what that response means  
  
아 지금 각 의견들에 대한 클러스터와 댓글 변화가 떴구나  
  
### 7. Evaluation  
  
Comparing the outcome with the original goal  
  
이제 의견들에 대한 댓글을 볼 수 있네, 목표가 달성되었군  
  
→ poor `visibility`, ambiguous `feedback` , and mismatched `expectations` can cause failure  
  
---  
  
## Design questions to ask  
  
How easily can one determine the `function` of the device?  
  
- Tell what actions are possible?  
- Determine mapping from intention to physical movement?  
- Perform the action?  
- Tell what state the system is in?  
- Determine mapping from system state to interpretation?  
- Tell if system is in desired state?  
  
---  
  
## Cognitive Engineering  
  
Norman  
  
### Gulf of `Execution`  
  
- 어떻게 쓰는거지?  
- 뭘 눌러야 하지?  
- 이거 하고 싶은데…  
  
‘유저가 의도한 것’과 ‘시스템이 지원하는 것’에 대한 간극  
  
Solution?  
  
- Use clear affordance  
- Make actions visible and intuitive  
- Minimize the number of steps  
  
---  
  
### Gulf of `Evaluation`  
  
- 뭐야 제대로 눌린거 맞아?  
- 그래서 지금 어떻게 된거지? 뭐가 변한거지?  
- 내 작업이 성공한건가?  
  
‘시스템이 보여준 것’과 ‘유저가 이해한 것’의 간극  
  
Solution?  
  
- Provide immediate and meaningful **feedback**  
- make system **visible**  
- Avoid ambiguous indicators  
  
⇒ 두 gulf 모두 디자이너가 제어할 수 없는 영역임. individual의 문화적 관습, 기술적 지식에 영향. (e.g. 모바일뱅킹)  
  
⇒ Making actions visible and intuitive. Providing clear, timely and meaningful feedback.  
  
---  
  
## Distance in Meaning and Form of Expression  
  
실제 목표와 머릿속에 나타난 표현 사이에는 semantic distance가 있고, 머릿속의 표현과 표현이 실제로 나타나는 형식 사이에는 articulatory distance가 존재한다.  
  
Goal ↔ Intention : Semantic distance  
  
Intention ↔ Execution (Action specification): Articulatory distance  
  
Perception ↔ Evaluation (Interpretation): Articulatory distance  
  
Evaluation ↔ Goal : Semantic distance  
  
---  
  
## How to Bridge the Gulfs in interaction?  
  
From system side…  
  
- Provide **intuitive** interface with clear **feedback**  
- Ensure the system **reflects user goals and expectation**  
  
From user side…  
  
- Support the formation of accurate **mental models**  
- **Reduce** the **cognitive burden** on user required to operate the system.  
  
---  
  
## Direct manipulation  
  
An interaction style where users `directly act on visible objects` using `intuitive physical actions` , rather than issuing abstract commands.  
  
### Three principles  
  
- Continuous representation of the object, actions using meaningful visual metaphors (deag…)  
    - 마우스 드래그하면 연속적으로 렌더링한다.  
- Use of physical actions (e.g. clicking, dragging) instead of complex command syntax  
    - figma 쓰는데 move x. … 이런거 쓰지 않지.  
- **Rapid**, **incremental**, **reversible** actions with immediate visual feedback.  
  
### 기본 아이디어  
  
- 물체가 그 자체의 시각적 특성으로 이해된다  
    - Using good affordance  
    - Using good conceptual model  
- Action은 스크린에서의 효과로 이해된다.  
    - rapid and incremental  
    - reversible  
    - immediate visual feedback  
  
### 효과  
  
- Direct engagement  
    - The feeling of `working directly` on the task (직접 한다는 느낌)  
    - No need to know the implementation details  
- Display == Reality (WYSIWYG)  
- Fewer error messages..? (Constraint 기반. 다만 에러는 줄겠지만 답답할 수 있음)  
  
---  
  
## Grammatical Structure of Interface Language  
  
### Object-Action: User select → Perform action on it  
  
- `modeless`  
- Action always occur within the context of object  
    - 파일에게 더블클릭  
    - 물체를 드래그  
    - 객체를 선택  
  
### Action-Object: action mode select → specify object  
  
- Modal (the user need to stay in correct mode)  
- Mode error can be dangerous  
- effective for repetitive tasks  
    - 파일 열기 위해 메뉴를 누른다  
    - 그리기 도구를 누른 후 그린다  
  
---  
  
## Interface Metaphors  
  
Why use metaphors for design  
  
1. Leverages users `prior knowledges` of familiar, concrete real-world objects.  
2. Transfer this knowledge to `abstract` computer concepts  
3. Reduces the `learning curve` and improve `usability`  
  
Ex. 파일을 버리는 곳은 휴지통, 페인트 칠하기는 붓 커서  
  
### Conversation metaphor  
  
CLI systems, voice-based assistant,  
  
- 인터페이스는 언어 매체.  
- 유저는 인터페이스를 virtual world로 통하는 매체로 여김.  
- 내가 하려는 action을 언어적으로 설명  
  
ex. Siri, CLI, 리눅스 터미널  
  
### Model world metaphor  
  
GUI systems, direct manipulation system  
  
인터페이스 자체가 virtual `world` .  
  
해당 world가 명시적으로 표현됨.  
  
action을 설명하는게 아니라 객체를 직접 조작.  
  
ex. Figma  
  
---  
  
### Direct Engagement  
  
Model world metaphor를 사용하는게 필요조건  
  
- Allow user act on objects of interest.  
- Create feeling of control over semantic objects  
- Reducing awareness of the system or code  
  
---  
  
## Metaphors Caveats  
  
common pitfalls  
  
### Too limited!  
  
metaphor는 인터페이스의 가능성을 제한시킨다.  
  
- 데스크탑은 실시간 협업을 잘 은유하지 못한다  
  
### Too Powerful  
  
metaphor는 은유된 실제 제품에 대해 전부 다 될 것이라고 믿는다.  
  
- 대량전송 에디터에 수식 기능을 원한다…  
  
### Too literal or cute  
  
너무 metaphor에 치중한 나머지 tedious, confusing, gimmick을 넣는다  
  
- 휴지통을 열어서 파일을 버리려면 뚜껑을 열어야함 ㅋㅋ  
  
### Mismatched  
  
task와 user mental model과 align되어있지 않으면 혼란스럽다  
  
---  
  
## Direct Manipulation의 장단점  
  
### Good for intermediate users  
  
- 정확한 좌표 찍는 등 정확도에 유리  
- leverages `recognize` over `recall`  
  
### Limits of Explicit Interaction  
  
- How to automate, generalize task?  
- Manually repeat actions  
  
### Metaphor can be too restrictive  
  
- WYSIAYG  
- Limit access to hidden capabilities  
- can discourage exploration  
  
### Problems?  
  
- Consime valuable screen space  
- Must learn the meaning of visual representations  
- Misleading visual representations (ex. 돋보기 = 확대, 검색?)  
- Blind or vision-impaired people ?  
- Experts?  
- Small screens?  
  
---
---  
tags:  
  - validation  
  - design  
  - info-vis  
  - visualization  
share: "true"  
github_title: 2025-09-24-design-validation  
title: 5. Design Validation  
date: 2025-09-24  
categories:  
  - Lecture Notes  
  - Information Visualization and Visual Analytics  
---  
  
### Why Validate?  
  
- VIS design space is huge, and mostly ineffective.  
- it is valuable to think how to validate from the very beginning of the design process.  
  
---  
  
## Nested Model  
  
→ Guidance on when to use what validation method  
  
There is different threats to validity at each level of model!  
  
---  
  
## Threats  
  
1. Wrong Problem  
    - 실제로 존재하지 않은 문제였음.  
2. Wrong Abstraction  
    - 잘못된 추상화. task나 data 상정을 잘못함  
3. Wrong Encoding / Interaction technique  
    - encoding이나 interaction이 효과적이지 않음  
    - 패턴이 잘 안보이는 등 encoding이 비효율적임  
4. Wrong Algorith,  
    - Code is too slow  
  
---  
  
## Why we separate to four levels?  
  
- You can **separately analyze the question** of whether each level has been addressed correctly.  
- 실제 디자인 순서와 무관함  
- VIS design은 매우 높은, iterative refinement 과정임  
    - 하위 block에서 만족되지 않았으면, 상위 block으로 올라오는 등.  
    - design as re-design  
  
---  
  
### Let’s Drill-down!  
  
### Domain Situation  
  
- Group of target users. Domain of interest.  
- User-centered design  
  
**Identify situation blocks**  
  
1. user typically cannot articulate their needs  
2. Reach the needs of target users  
    - Via interviews, observation, research  
  
→ Detailed set of **questions or actions**  
  
- Problem being mischaracterized  
- **Interview** and **observe** target audience  
    - Field study  
    - Contextual Inquiry  
  
→ Validate: Adoption rate  
  
---  
  
### Data Task Abstraction  
  
Domain specific → Domain independent representation  
  
- Browsing, summarizing…  
  
**Design** abstract data block (derivation)  
  
- Determine which data type would support a visual encoding  
- age(quantitative) → categorical  
  
내 결정이 맞는지, plain table 등 baseline과 비교하여 justify해야한다.  
  
ex) early web browser ‘lost in hyperspace’ problem → cognitivity graph로 해결해야한다.  
  
- Task and data abstractions do not solve the topic of the target audience  
    - Must be tested after implement  
    - ex. 주식 도메인에서는 사실 두 데이터 비교를 하지 않는다.  
  
→ Let the target users try the tool. Collect evidence of utility!  
  
- Field study  
    - Different from domain  
        - Observe change of behavior  
  
---  
  
### Visual Encoding Idiom  
  
Decide on the specific way of creating, and manipulating the visual representation of the abstract data block.  
  
- Visual Encoding Idiom for controlling what users see  
- Interaction Idiom for how users change what they see  
  
Design Idiom Blocks  
  
- Should match the task / data abstraction! → Categorical - Bar chart  
- Consider visual perception and memory  
  
→ 실제 practice로 guideline이 연결되지 못하는 gap이 존재하는데 이것도 여기 속함.  
  
- Is the idiom effective?  
- Justify design of idiom  
    - 비교에는 small multiples가 좋다  
  
→ Lab study.  
  
→ Presentation and qualitative discussion of result  
  
Quality metrics: ex. # of edge crossings.  
  
---  
  
### Algorithm  
  
Design algorithm block  
  
- Speed, memory  
      
- Perceptual fusion (feedback within 100ms) → Causality  
      
- Time / Memory Performance  
      
- Complexity  
      
- Wall-clock time  
      
    - Scalability, Benchmarks  
  
---  
  
## Angles of Attack for Designing Vis  
  
### Top down  
  
- Problem-driven: search for existing idioms to solve the real world users’ problem → Design Study  
    - What idiom to choose?  
  
### Bottom up  
  
- Technique-driven: new encoding, new interaction을 잘 찾아서 domain을 잘 찾아 적용시키기.  
    - Your Idiom’s relationship between existing idioms?  
  
## Avoid mismatch!  
  
- 내 contribution claim과 validation 방법이 잘 Match 되어야함.  
  
ex. 그래픽 알고리즘을 향상시켰다. → 시간 감소 확인  
  
ex. 내가 task와 data abstraction을 잘 했나? 사람들이 실제로 웹 브라우저 비교를 하나? → 유저 스터디. 그들에게 시켜보기. (랩 세팅 x)  
  
### Only a subset!  
  
- Pick validation method according to contributio claims  
  
### Iterative Design Process  
  
- Vis design is highly iterative process.  
    - feedback and forward into refining blocks at other level  
    - levels are not in strict order  
    - revisit and redesign  
- Shortcut across inner level  
    - Rapid prototyping  
    - Wizard of OZ  
        - Lo-Fi stand ins so downstream validation can happen sooner
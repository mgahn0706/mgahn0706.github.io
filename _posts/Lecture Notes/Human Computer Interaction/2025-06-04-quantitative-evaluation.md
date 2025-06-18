---  
tags:  
  - hci  
  - evaluation  
share: "true"  
github_title: 2025-06-04-quantitative-evaluation  
title: 18. Quantitative Evaluation  
date: 2025-06-04  
categories:  
  - Lecture Notes  
  - Human Computer Interaction  
---  
## Quantitative vs Qualitative  
  
### Quantitative  
  
- Objectively measure human performance  
- more narrow focus  
- internal validity  
  
### Qualitative  
  
- Observe and develop understanding of human experience  
- Emphasis on preserving the richness of the non-numeric data  
- External validity  
  
---  
  
## Quantitative Evaluation is somehow scientific approach..  
  
Beyond user friendly.  
  
Specify user and tasks  
  
What to measure  
  
- Time to learn  
- speed of performance  
- error rate  
- user retention (how they remember from first learn)  
- Subjective satisfaction  
  
---  
  
## Quantitative Evaluation  
  
### Methods  
  
1. User event collections  
      
    ex. Mouse clicks…  
      
2. Controlled experiment  
      
    - Testable hypothesis  
    - Independent / dependent variables  
    - Can be reproduced (reliability)  
  
---  
  
## User Event Collection example  
  
Undo & erase & self-report 비율 분석  
  
→ Undo나 erase의 빈도만 보면 대부분의 self-report를 잡아낼 수 있다.  
  
---  
  
## Controlled Experiment  
  
Based on Practical problem and existing theory  
  
- Outcome  
    - Guidance for practitioners  
    - Refine theory  
    - Advice for experimenters  
  
### How to do it?  
  
1. State a lucid, testable hypothesis  
2. Identify independent and dependent variables (and controlled, randomized variable)  
3. Design the experimental protocol  
4. Choose the user population  
5. Apply for human subjects protocol review (IRB review)  
6. Run a couple user pilot tests  
7. Run the experiment (Don’t forget to debrief)  
8. Run statistical analysis  
9. Draw conclusions  
  
---  
  
## Note for Running the Experiment  
  
Is it ethical? Is it useful?  
  
Is it reliable?  
  
Is it valid?  
  
1. Does this experiment consider variations between subject?  
    - Enough samples, or blocked?  
2. Was this experiment biased?  
3. Does the experiment reflect real world situation?  
  
---  
  
### Independent Variables  
  
The things you `manipulate` independent of a subject’s behavior.  
  
ex) device type  
  
### Dependent Variables  
  
- variables dependent of a subject’s behavior.  
- The things you set out to quantitative measure.  
  
### Control Variables  
  
- Circumstance not under investigation that is `kept constant` while testing the effect.  
- More control → Less generalizable → Low external validity.  
  
### Random Variables  
  
- Circumstance that is allowed to vary randomly.  
- More variability means low internal validity, but high external validity!  
  
⇒ There is trade-off between control variables (internal) and random variables (external)!  
  
### Confounding Variable  
  
- 고려하지 않았으나 실험 결과에 영향을 준 variable. (악영향)  
- External factor that can affect the results of experiment.  
- Circumstance that varies **systemically** with independent variables.  
- Should be controlled or randomized to avoid misleading results!  
  
→ ex) GDP - Child’s weight  
  
- Correlates with both dependent and independent variables  
- Cause Type-I Error (거짓 양성, 실제로는 두 변수간 영향이 없는데 영향이 있는 것처럼 나옴)  
- Hurts internal validity  
  
Then how to control confounding variables?  
  
1. Case-control study  
    - 해당 case를 적용하지 않은 그룹을 만들어서 대조군 만들어 비교.  
2. Cohort study  
    - Homogeneous한 group 하나를 select하여, 여러 시간에 걸쳐서 지속적 조사  
3. Blocking  
    - Grouping experimental units that are similar.  
4. Randomization  
    - 각 test subject를 랜덤한 그룹에 넣어서 confounding variable 자체가 골고루 퍼지도록. (sample 수 많이 필요)  
  
---  
  
## Blocking  
  
- Group experimental units into `block` based on similarity.  
- Primary interest가 아닌, variability를 그룹화 시킨 뒤 각 그룹(block)에 절반 절반에 서로 랜덤하게 부여한다.  
  
→ 성별, 사람 등에 의한 selection bias가 감소할 수 있음  
  
ex) 두 종류의 깔창 테스트  
  
1. Randomize: User, and assign random shoe for 5 people each.  
2. Blocking: Make each user as block. Assign left or right shoe.  
  
Best practice  
  
- Should randomize in each block  
- Measure difference within the block  
- Block what you can; randomize what you cannot  
  
---  
  
## Design the experimental protocol  
  
### Between subjects:  
  
each subject runs one condition  
  
Pros:  
  
- Compare observed results between independent groups.  
- Can eliminate ordering and learning effects.  
  
Cons:  
  
- Need more subjects  
- Difference between subjects might introduce a bias.  
- Might allow confounding variables  
  
### **Within subjects:**  
  
each subject runs all conditions; comparing result within each subject.  
  
Pros:  
  
- Need less subjects  
- can eliminate variation (and confounding variable) due to difference between subject.  
  
Cons:  
  
- Be aware of ordering effect and, learning effect  
  
---  
  
## Run Experiment  
  
뭐 이거 어떻게 하는지는 Evaluation with user에서 잘 정리했지만…  
  
IRB Review Process를 꼭 거쳐야 한다!  
  
- Always run pilot first!  
- All subject should follow the same steps  
  
---  
  
## Choose the User Population  
  
Pick a well-balanced sample  
  
- Novice, experts…  
- age… gender…  
  
→ or maybe an independent model.  
  
Control subject variability  
  
→ Number of subjects (power analysis) N=20~30 이런거 정하기, 사전 논문 조사나 small scale로 구할 수 있음  
  
---  
  
## Run Statistical Analysis  
  
Properties of our population  
  
- Mean Variance…  
  
How different data sets relate to each other?  
  
Probability that our claims are correct  
  
Note: 유의수준(level of statistical significance) → p-value < alpha이면 우연으로 보기 힘들다. 통계적으로 유의미한 결과이다. 귀무가설을 기각한다.  
  
---  
  
### What test to use?  
  
Parametric test… → 특정 조건들이 몇개 있음  
  
Nonparametric test → 통계적으로 좀 안좋음  
  
---  
  
### Analysis of Variance (ANOVA)  
  
독립변수가 종속변수에 유의미한 영향을 끼쳤는가?  
  
즉, 평균이 유의미하게 다른가?  
  
→ 근데 왜 ANO”VA” 죠??  
  
평균만 가지고는 이게 ‘유의미한’ 차이가 있는지 알 수 없음. 분산이 유의미하게 작아야 두 평균이 ‘유의미하게’ 차이 있는지 알 수 있음.  
  
F 검정의 F-value: 그룹간 분산이 그룹 내 분산보다 큰 정도 = 크면 유의미하게 차이 있다.  
  
P-value: 귀무가설을 기각할 확률. 통계적으로 유의미할 확률. 우연이 아닐 확률  
  
s: significant  
  
ns: not significant  
  
---  
  
### Quantitative Approach outcome  
  
Focus on **low-level effect**  
  
- Captures patterns of use  
  
Pros  
  
- Provide objective measurements  
    - Strong internal validity  
  
Cons  
  
- Low external validity  
- Small differences may lack practical significance (even though it has high statistic significance)  
  
---  
  
### Qualitative Approach outcome  
  
Focus on **high-level** effect  
  
- Identifies user **flow**  
- Highlights **ambiguities** in task description  
- Reveal **contextual** insights  
  
Pros  
  
- Strong external validity (generalizable)  
  
Cons  
  
- Low internal validitiy  
- subjective interpretation
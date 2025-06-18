---  
tags:  
  - hci  
  - visualization  
share: "true"  
github_title: 2025-05-21-information-visualization  
title: 15. Information Visualization  
date: 2025-05-21  
categories:  
  - Lecture Notes  
  - Human Computer Interaction  
---  
## Data Visualization  
  
### Scientific visualization  
  
의학 시각화, 인체 단면 등 실제로 있는 무언가를 재현  
  
### Information Visualization  
  
Abstract Data를 재현하고 그림. persona마다 다르게 시각화하는게 유리할 때가 있음  
  
## 왜 굳이 External Representation?  
  
- data를 머리로 기억하면 한번에 7+- 2 개 밖에 working memory에 쓰지 못함.  
- 따라서, 직접 쓰면서 외부에 표현하면 working memory가 확장되는 효과가 있음  
  
### Why use visualization?  
  
- Senential vs Diagrammatic representation  
    - Efficiency of search for information  
    - Explicitness of information  
  
→ diagrammatic에서는 정보들이 적절한 위치에 잘 써있다.  
  
→ Diagram에서는 problem solving이 smooth traversal을 통해 진행될 수 있다.  
  
(+ little search for computation of elements)  
  
i.e. Pulley  
  
---  
  
## Visualization reveals `structures`  
  
ex. 추세선 그리기  
  
평균, 표준편차, 분산으로는 서로 같은 값이 나와도 실제 값들의 관계는 전~혀 다를 수 있음.  
  
통계적인 특성을 밝혀내는 데에 매우 유리하다.  
  
---  
  
## Definition  
  
> The use of computer-supported, interactive, visual representations of `abstract data` to amplify `cognition`  
  
---  
  
### Some historical infos…  
  
최초의 시각화 차트 (아마도)  
  
William Playfair - Invented line, bar, area and pie charts.  
  
Charles Joseph Minard - 나폴레옹의 전투 기록, 여러가지 정보를 한눈에 아주 효과적으로 시각화 한 사례  
  
1854 London Cholera Epidemic → 환자 발생지와 water source간 관계 파악  
  
Rose-petal diagram → 병원 내 감염이 더 많다. 시간에 따라 줄어드는 것을 효과적으로 보임  
  
---  
  
### Replative Perception  
  
우리는 실제 값보다 주변의 상댓값에 영향을 받는다.  
  
---  
  
### Expressiveness & Effectiveness  
  
- Expressiveness  
    - Vis idiom should express `all of` and `only` the information in the dataset attributes  
    - 새로운 정보를 추가하지도  
    - 제거하지도 마라  
  
‘길이’정보가 추가되어서 사람들에게 혼란. scatterplot 등이 더 적절하다.  
  
- Effectiveness  
    - 가장 중요한 특성은 가장 효과적인 channel로 표현해야한다.  
  
---  
  
## Dimension and power law  
  
### Steven’s Power Law  
  
p: perceived magnitude, a: actual magnitude  
  
$$ p = ka^\alpha $$  
  
$$ {p_1 \over p_2} = ({a_1 \over a_2})^\alpha $$  
  
alpha값이 작을수록, 실제보다 더 작게 percieve. → 실제론 2배가 되었지만, 2^0.99 정도로 인식한다는 뜻  
  
length는 1  
  
area는 1보다 작고,  
  
volume은 1보다 훨씬 작다. 실제로 2배를 해도 거의 똑같다고 느끼는듯.  
  
⇒ 즉 비율 비교가 중요한 데이터는 line으로 비교해야 왜곡이 적겠지?  
  
---  
  
### 그래서 어떤 representation을 써야하는데  
  
task에 따라 매우 다르다. (인지하는 사람에 따라서도!)  
  
1. 정확한 값을 보여줘야 한다 → 숫자  
2. peak에 비해 얼마인가 → bar와 피크 표시  
3. 시간에 따라 얼마나 변하는가 → line graph  
4. 내 것에서 어떤게 용량을 많이 차지하고 있는가 → Treemap. (비율 판단에 좋음) + hierarchy에도 좋아서 색깔로 추가 정보 줄 수 있다.  
  
---  
  
## 왜곡 발생.  
  
Hidden peak을 발견하기 어렵다.  
  
---  
  
## Weber’s Law  
  
Position Perception > Length perception이라 바로 파악하기가 어렵다.  
  
$$ {\Delta S \over S} =k(constant) $$  
  
차이를 인식하는 능력은 절대적인 차이가 아니라 비율에 달려 있습니다.  
  
---  
  
## Preattentive Processing  
  
Cognitive processing done pre-attentively, without focusing attention.  
  
- Less than 200~250ms  
  
ex) Popout effect, segmentation effect  
  
### Popout effect  
  
- Easily detected regardless of the number of distractors.  
- Color makes them popout!  
  
ex)  
  
- Orientation, Curved, shape, size, color, light/dark…  
- Not pre-attentive: Parallelism, Juncture  
  
**Popout effect is useful for task that…**  
  
1. Target detection  
2. Segmentation - Boundary detection  
3. Region tracking (distinctive moving group trace)  
4. Counting  
  
→ but, you need to use only one color… (surrounded color do not pop)  
  
### Law of Preattentive display  
  
1. Must stand out on some simple dimension.  
    1. color  
    2. shape  
    3. motion.,,  
  
위로 갈수록 양적인 인지가 정확함. 아래로 갈수록 부정확.  
  
### Visual encoding (effectiveness) principles  
  
어떤 것(어떤 채널)로 인코딩해야 효과적인가  
  
데이터의 종류마다 다르다!  
  
## Design Principles  
  
Shneiderman’s guideline, tufte’s principles, feynman-tufte principle…  
  
### Design Guidelines  
  
- Visual presentation of query components & results (in text-based situation)  
- Rapid, incremental, reversible actions (direct manipulation)  
- immediate and continous feedback  
- Selection by pointing (not typing)  
- Reduce errors  
- Visual information seeking `mantra` (주문을 외우듯)  
    - Overview first → zoom and filter → details on demand  
  
### Tufte’s Design Principle  
  
1. Tell the truth  
    1. Graphical Integrity  
2. Do it effectively with clarity, precision ,,,  
    1. Design Principles/aesthetics  
3. **Simple design, intense content**  
    1. Feynman-Tufte principle  
  
---  
  
## Measuring Misrepresentation  
  
Visual attribute should be directly proportional to data value.  
  
(Lie factor) = (Size of effect in graphic) / (Size of effect in data)  
  
→ 1이 아니라면 거짓됨  
  
### Distortion in Multi-dimensional projection  
  
2d로 바꾸는 순간 무조건 데이타가 손실/왜곡 된다.  
  
→ Distortion  
  
Try to preserve the characteristics of the original data as most as they can.  
  
- Cluster structure, outlier, distance between points…  
  
→ commonly scatterplot  
  
### Distortions  
  
1. Missing neighbors  
  
원래는 옆에 있었는데 더이상 가까이 있지 않음. 연관성이 안보임  
  
1. False neighbors  
  
원래는 연관성이 없는 데이터끼리 옆에 붙어버림.  
  
- CheckViz  
    - 다양한 차원-감소를 테스트해보면 PCA, NLM등은 false neighbors가 높고 DD-HDS, CCA는 Missing neighbors가 높음을 알 수 있다.  
  
### Distortion in Groups!  
  
cluster-cluster 간 관계에서도 유사한데, missing group, false group으로 평가할 수 있음  
  
## Back to Design Principles..  
  
### Data-ink ratio  
  
(Data-ink ratio) = (Data ink) / (Total ink used in graphic)  
  
= (데이터 표현 시 써야하는 잉크 양) / (실제로 쓴 잉크 양)  
  
= 얼마나 redundant하지 않게 잉크를 썼는가?  
  
**Data-ink ratio = 데이터 표현의 효율성**  
  
→ 그래프에서 불필요한 장식이나 중복을 제거하고 핵심 정보에 집중하도록 디자인하라는 원칙입니다.  
  
### Chartjunk  
  
- Pie chart 에서 가운데 뚫기 → angle perception 부정확  
- 막대그래프 아래 자르기. 3d 막대그래프 (근데 2d여도 되는 경우)  
- External visual elements  
  
### Use small multiples  
  
- 동일한 그래픽 요소를 반복. → 가까이 배치하여 차이점 강조하기  
- 비교가 쉽고 한눈에 잘 보임 (invite comparison)  
  
### Utilize Narratives of space and time  
  
이건 뭐 계속 나오네  
  
### Use Negative space  
  
띄우고, 비울 떄는 적절히 비워서 효과적인 디자인 해야한다~
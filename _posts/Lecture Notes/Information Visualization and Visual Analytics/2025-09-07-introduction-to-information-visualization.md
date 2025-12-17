---  
tags:  
  - info-vis  
  - visualization  
  - visual-encoding  
  - task  
  - preattentive  
  - design  
share: "true"  
github_title: 2025-09-07-introduction-to-information-visualization  
title: 1. Introduction to Information Visualization  
date: 2025-09-07  
categories:  
  - Lecture Notes  
  - Information Visualization and Visual Analytics  
---  
## InfoVis vs. SciVis  
  
### Scientific Visualization  
  
- Visualization that deals with `physical` data.  
- Ex: MRI scans, climate models  
- has smaller design space (bound to physical space)  
  
### Information Visualization  
  
- Visualization that deals with `abstract` data  
- Ex: Treemap, hierarchical cluster …  
- has larger design space  
  
<aside>   
  
Why use an External Representation?  
  
- Finding the `aritifical memory` that best supports our natural means of `perception`.  
- It expands our `working memory` to help decision-making.  
- Problem solving can proceed through a smooth traversal with diagrammatic representations. </aside>  
  
---  
  
## Power of Visualization  
  
- Visualization can reveal `interesting structures` that tabular data can’t.  
    - Correlations, outliers, skewness…  
  
- Statistical characteristic of dataset is powerful approach….but  
    - losing information through summarization. → Hide the true structure.  
    - Over-simplified!  
  
---  
  
## Definition of Visualization  
  
> The use of computer-supported, interactive, visual representations of `abstract` data to amplify `cognition`  
  
> Finding the `artificial memory` that best supports our natural means of perception.  
  
> Provide tools that present data in a way to help people understand and gain `insight` from it  
  
---  
  
### InfoVis Reference Model  
  
- RawData → DataTables (Data transformation)  
    - 엑셀에서 데이터 attributes 선택  
    - Derive  
    - Filtering, aggregating  
    - formatting  
- DataTables → Visual Structures (Visual Mappings)  
    - Position, size, color…  
    - e.g. map ‘circle radius’ to ‘population’ in a bubble chart  
- Visual Structures → Views (View transformations)  
    - Zoom & Pan  
    - Brushing, sorting…  
  
---  
  
## History  
  
1. William Playfair (1759~1823)  
    - Invented pie, line, bar, area charts  
2. Napoleon’s Chart  
3. 1854 London Cholera Epidemic  
4. Rose-petal diagram  
  
---  
  
## Perception for InfoVis  
  
### Relative Perceptions  
  
- 사람들은 상대적인 값으로 감각을 인지함.  
- Do not let context(distortions) affect decision-making.  
  
### Two Criteria of Evaluating Graphical designs  
  
### Expressiveness  
  
- Vis idiom(=chart) should express `all of` and `only` the information in the dataset attributes.  
- 더도말고 덜도말고 표현할 것만 표현해라  
  
### Effectiveness  
  
- Most important attribute should be encoded with the most `effective channels`  
- 가장 중요한 특성은 가장 효과적인 채널을 쓰도록.  
  
**→ Steven’s Power Law**  
  
$$ {{p_1}\over{p_2}}=({{a_1}\over{a_2}})^\alpha $$  
  
$\alpha$가 1에 가까우면 정확한 perceived. 1보다 작으면 실제 비율보다 더 작게 perceived됨. (e.g. 면적과 부피는, 길이보다 $\alpha$값이 작음)  
  
### Effectiveness of Visual Encoding  
  
1. Position  
2. Length  
3. Angle, Slope  
  
… (Area, Volume, Color, Density)  
  
**Channel effectiveness varies by data types**(ordinal, quantitative, nominal)  
  
- Quantitative  
    1. Position  
    2. Length  
    3. Angle  
    4. Slope  
- Ordinal  
    1. Position  
    2. Density  
    3. Saturation  
    4. Hue  
- Nominal (Categorical)  
    1. Position  
    2. Hue  
    3. Texture  
    4. Connection  
  
---  
  
### Which Representation is best?  
  
→ It depends on `task`  
  
(e.g.  
  
- Users need to know exact value → Number  
- Users need to know trend → Line chart  
- Users need to know hierarchical data ratio → Treemap)  
  
---  
  
### Weber’s Law  
  
크기가 큰 것을 비교할 때는 차이가 커야한다.  
  
→ 크기 차이를 강조하려면 시각적으로 작아야한다.  
  
---  
  
## Preattentive Processing  
  
Cognitive operations done preattentively, less than 200ms!  
  
- Popout effects  
- Segmentation effects  
  
Preattentive task가 되려면  
  
- Easily detected `regardless of number of distractors`  
- vs. Tiime-consuming visual search  
  
Task 종류 → Target detection, segmentation, region tracking, counting (like sevens)  
  
---  
  
### Surrounded colors do not pop out!  
  
→ need to use simple hues (only two)  
  
---  
  
### Laws of Preattentive display  
  
- Must stand out on some simple dimension  
- Lessons for highlighting - one of each  
  
---  
  
## Design Guidelines  
  
- Visual Information seeking Mantra  
    - Overview first, zoom and filter, details on demand  
  
### Tufte’s Design Principles  
  
- Tell the truth (Graphical integrity)  
- Do it effectively with clarity  
- Simple design, intense content  
  
---  
  
### Lie factor  
  
- Visual attribute value는 data attribute value에 비례해야한다.  
- Lie factor = (Size of graphic) / (size of data)  
  
---  
  
### Data-ink ratio  
  
- We need to maximize this  
- Data-ink ratio = (Data ink) / (Total ink used in graphic)  
  
→ Avoid chartjunk (extraneous visual elements)  
  
---  
  
### Use small multiples  
  
- Repeat visually similar graphical elements  
  
---  
  
### Utilize narratives of space and time  
  
- Story-telling!  
- Tell a story of position and chronology through visual elements  
  
---  
  
### Negative spaces  
  
---
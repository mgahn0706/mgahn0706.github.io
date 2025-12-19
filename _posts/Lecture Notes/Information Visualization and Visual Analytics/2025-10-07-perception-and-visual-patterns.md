---  
tags:  
  - perception  
  - visualization  
  - visual-encoding  
  - info-vis  
  - gestalt-principle  
  - preattentive  
share: "true"  
github_title: 2025-10-07-perception-and-visual-patterns  
title: 7. Perception and Visual Patterns  
date: 2025-10-07  
categories:  
  - Lecture Notes  
  - Information Visualization and Visual Analytics  
---  
## Gestalt Laws  
  
- the whole is different from the sum of its part  
- leaving a set of descriptive principles, without a model of perceptual processing.  
  
### The Principle of Pragnanz  
  
- Fundamental principle of gestalt perception  
- Law of simplicity, law of good figure  
- tend to order our experience in a manner that is  
    - Regular  
    - Orderly  
    - Symmetric  
    - Simple  
  
## Principles  
  
1. Emergence  
    1. the dog is perceived as a whole. (without explicit edges)  
2. Reification  
    1. more explicit spatial experience  
3. Multistability  
4. Invariance  
  
## Gestalt Principles  
  
### Grouping  
  
1. Proximity: associated with nearby elements  
      
2. Similarity: associated with similar elements  
      
3. Continuity: Preference for continuous, unbroken, smoothest contours with the simplest possible  
      
4. Common Fate: things moving together  
      
5. Closure  
      
6. Common Region  
      
7. Connectedness  
      
  
### Perception of Form  
  
1. Closure: form complete, closed figure increase regularity  
2. Area/Figure and Group/Relative Size: smaller one is figure  
3. Symmetry: we tend of perceive objects as symmetrical shape in spite of distance  
  
---  
  
### Gestalt Laws can mislead  
  
→ Natural Camouflage  
  
## Examples  
  
### Grouping  
  
helping users parse the display into subunits  
  
→ 2D space에 data가 품고 있는 구조, dimension을 파악 후 mapping한다.  
  
### Hierarchy  
  
provide a context for each piece of information  
  
→ similarity, proximity  
  
e.g. mac vs windows  
  
Data 간의 Hierarchy가 실제 data 구조, 디자인과 잘 맞아야함  
  
### Balance  
  
harmonious global arrangement.  
  
→ visual weight를 고려하여 디자인.  
  
modal에서 오른쪽 아래에 confirm 버튼 넣기  
  
### Human Size Perception  
  
- Straight line > Curved line > Sharp line  
  
즉, curved line, sharp line은 좀 더 과장해서 그려야 visual weight이 맞아진다. (optical adjustment)  
  
---  
  
## Human Visual System  
  
- Visual attention: mechanisms that help determine which regions of an image  
- Detailed vision for shape and color → foveal vision (약 1도)  
- Motion은 주변시야에서도 감지 가능  
- Fixation-saccade cycle  
  
### Fixation-Saccade Cycle  
  
- Fixation: 자세한 정보가 필요할 때 잠깐 멈추는 period  
- Saccade: 새로운 location으로 이동할 때 flicking하는 것.  
- Bottom-up: information from fixation → mental experience  
- Top-down: current mental states(task and goals) → Guiding saccade.  
  
### Expectation and memory  
  
Current state는 아주 중요한 역할을 한다.  
  
- Role of memory and expectations.  
- 무엇을 기대하고있는지에 따라서 해당 물체나 장면에 대해 기억하는게 달라짐.  
  
## Preattentive Tasks  
  
### Postattentive Amnesia  
  
Previewing do not make search faster!  
  
human vision is not optical camera.  
  
→ Postattentive search was as slow as traditional search.  
  
그래서 결국 시각화 디자인에 적용하려면…  
  
- 대부분의 시각화는 novel하다. (대부분 처음보는 chart일 것이다)  
- LTM으로 콘텐츠가 commit되기 힘들다.  
- preattentive methods가 data exploration에 있어서 매우 중요하다.  
  
### Preattentive Tasks  
  
- low-level, fast-acting visual process에 의해 빠르게 감지되는 시각적 feature  
- Precede focused attention  
    - within a single fixation  
  
1. Target detection  
2. Boundary detection  
3. Region Tracking  
4. Counting and estimation  
  
→ Motion is very preattentive. (retina 영역에 있어도 detect가능). Unintended attention  
  
### Laws of preattentive display  
  
1. 간단한 차원에서 stand out해야한다.  
    - color  
    - simple shape  
    - motion  
    - depth  
2. lessons for highlighting → 섞으면 안됨  
  
각 channel 마다 더 overrule하는 게 있음  
  
when mixed, hue >> shape  
  
hue << brightness (which I disagree)
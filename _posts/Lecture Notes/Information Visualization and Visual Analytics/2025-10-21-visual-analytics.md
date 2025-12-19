---  
tags:  
  - visual-analytics  
  - info-vis  
  - visualization  
  - conceptual-model  
share: "true"  
github_title: 2025-10-21-visual-analytics  
title: 10. Visual Analytics  
date: 2025-10-21  
categories:  
  - Lecture Notes  
  - Information Visualization and Visual Analytics  
---  
## Definition  
  
The science of analytical reasoning faciliated by interactive. visual interfaces.  
  
### Visual Analysis  
  
- The **procedure** in which analysts make reasonings  
  
### Visual Analytics  
  
- The system, framework, or discipline of visual analysis.  
- Integral approach of combining visualization, human factors, and data analysis.  
  
## Early systems  
  
- Cluster and calendar based visualization  
- Hierarchical clustering explorer  
- XMDV Tool  
- GGOBI  
  
## Why Interaction?  
  
- Helps analysis to view data more comprehensively  
- Helps to correct perceptual errors (in 3d data)  
  
## Visual Analytics Models  
  
### KDD process  
  
- Waterfall model  
- data mining community  
### InfoVis Pipeline  
  
- Waterfall again  
  
### Views on Visualization  
  
- Explains why wee need interaction  
  
### Knowledge Generation Model  
  
---  
  
### Implications of Visual Analytics model  
  
- Visual Analytics is an **interactive**, and **iterative** process  
- They aim to support `knowledge generation` and `decision-making`  
- Collaboration between analysts and machines  
  
---  
  
## What is important then?  
  
### Scalability  
  
Shape, threshold, better performance.  
  
→ need for causality. attention.  
  
1. **Computational Scalability**  
  
- Precomputation  
    - 미리 계산해 놓자. 내가 드랍율 미리 계산해 놓은 것 처럼.  
    - 미리 aggregation이나 clustering 해도 좋다.  
- Query  
    - 검색 속도도 빨라야한다.  
    - 미리 다 계산해놓으면 빠르겠지만, 메모리 이슈가 있겠지  
- Rendering  
  
ex. t-SNE → BH t-sne → GPGPU t-sne  
  
1. Visual scalability  
  
- Overplotting  
    - change visual encoding. (opacity)  
    - subsampling  
    - Aggregation  
        - density maps  
  
### Observation-Level Interaction  
  
- Manipulate data point and visual patterns directly (DND)  
- Require domain knowledge  
- Updates parameters to match user intent  
    - escape scalability issue  
  
→ Blend parameter with observation-level interactions  
  
- consider parameter as interactive data  
- Enable parameter affect visual patterns.  
    - Leverage both approaches
---  
tags:  
  - task  
  - abstraction  
  - info-vis  
  - visualization  
share: "true"  
github_title: 2025-09-19-task-abstraction  
title: 4. Task Abstraction  
date: 2025-09-19  
categories:  
  - Lecture Notes  
  - Information Visualization and Visual Analytics  
---  
  
---  
  
## Why abstract Task?  
  
`domain-specific` 한 방법보다는 `abstract` 하게 task를 고려해야한다.  
  
→ 그렇지 않으면, 도메인마다 너무 task가 달라짐.  
  
## Actions  
  
- High-level: Analyze  
- Mid-level: Search  
- Low-level: Query  
  
hierarchical하게 나눠짐. 각 수준에 따른 선택은 독립적이며, 모든 action은 각 3개의 수준에서 설명가능하다.  
  
---  
  
## High-level: Analyze  
  
### Consume  
  
(1) Discover  
  
- Find new knowledge that is not previously known  
    - `generate` new hypothesis, or `verify` existing hypothesis.  
- For Scientific inquiry  
  
(2) Present (=explain)  
  
- The communication of information that is already understood (보고용)  
- e.g. Infographic  
- Output of discover → input of present  
  
(3) Enjoy  
  
- Motivated by user enjoyment  
- Casual  
  
### Produce  
  
(1) Annotate (=tag)  
  
- attaches temporary info  
  
(2) Record  
  
- save or capture as persistent  
  
(3) Derive (=transform)  
  
- To produce new data elements based on existing elements  
- Changing type of data (aggregation)  
- transform with additional info  
- using arithmetic/statistic/logical operations  
  
→ Do not draw what you are given  
  
---  
  
## Mid-level (Search)  
  
high level을 수행하려면 먼저 search를 수행해야함  
  
||Target Known|Target Unknown|  
|---|---|---|  
|Location Known|Lookup|Browse|  
|Location Unknown|Locate|Explore|  
  
---  
  
## Low-level (Query)  
  
target을 search를 통해 찾았다면, QUERY해야힘.  
  
ex. 선거 결과  
  
(1) Identify  
  
- 서울 관악구의 선거 결과 확인  
  
(2) Compare  
  
- 서울 관악구와 동작구의 결과 비교  
  
(3) Summarize / Overview  
  
- 전체적인 투표 결과 분포 확인  
  
---  
  
## Targets  
  
### All-data level  
  
(1) Trends (=patterns)  
  
- high-level pattern  
- increase, decrease…  
  
(2) Outliers  
  
(3) Features  
  
- Particular structures of interest  
- Task-dependent definition  
    - e.g. clusters  
  
### Attribute Level  
  
(1) One attribute  
  
- Individual values  
- extremes  
  
(2) Multiple attributes  
  
- Dependency (인과관계)  
    - association  
- Correlation (상관관계)  
- Similarity  
  
### For specific dataset  
  
- Network data  
    - paths  
- Spatial data  
    - shape  
  
---  
  
## Practice Analysis!  

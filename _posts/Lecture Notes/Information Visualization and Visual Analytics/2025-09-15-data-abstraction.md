---  
tags:  
  - info-vis  
  - abstraction  
  - visualization  
share: "true"  
github_title: 2025-09-15-data-abstraction  
title: 3. Data Abstraction  
date: 2025-09-15  
categories:  
  - Lecture Notes  
  - Information Visualization and Visual Analytics  
---  
# What?  
  
### Why do data semantics and types matter?  
  
Data attributes define real-world meaning. (e.g. Basil, 7, S, Pear)  
  
## Type of the data: Structural interpretation  
  
### Data Level: `Data Types`  
  
- item, attribute, link, position, grid  
  
### Dataset Level: `Dataset Types`  
  
- How data types combined into larger structure  
- table, tree, field or sampled value  
  
### Attribute Level: `Attribute Types`  
  
- What kind of mathematical operations are meaningful?  
  
→ Variable, dimension  
  
---  
  
## Data Types  
  
1. Attribute: Specific property that can be measured, observed, or logged. (variable or dimension)  
2. Item: individual entity that is discrete  
3. Link: relationship between items  
4. Grid: specifies the strategy for sampling continuous data in terms of both `geometric` and `topological` relationships  
5. Position: spatial data, providing a location  
  
---  
  
## Dataset Types  
  
Collection of info that is the target of analysis.  
  
- Tables: Attributes+ Items  
- Networks and Trees: Items + Links + Attributes  
- Fields: Grids(positions) + Attributes  
- Geometry: Items + Positions  
- Clusters, sets, lists: Items  
  
---  
  
### Tables  
  
Items + Attributes (= field, variable, dimension)  
  
Cell contains value  
  
- quantitative  
      
- nominal  
      
- ordinal  
      
- Multidimensional table: Indexed with multiple keys (cannot index with one key; SSN?)  
      
  
### Networks and Trees  
  
Items + Attributes + Links  
  
Well-suited when there is some `relationship` between items  
  
- Node(item) → can have associated attributes  
- Link : relation between items  
  
### Fields  
  
Data created by sampling on grids  
  
→ measurement of `continuous` domain  
  
- Spatial Fields: cell structures based on sampling at spatial positions  
    - non-spatial data: abstract data  
    - Scivis: Spatial data is `given` with dataset (세포 위치가 정해져 있듯)  
    - InfoVis: Designer가 space 사용에 대한 부분을 `choose` 한다.  
  
(1) Spatial Fields: For SciVis. Spatial positions are given with the dataset.  
  
(2) Grid Types: Grid needs (1) Geometry: location and (2) Topology: how each cell connected  
  
- Uniform Grid  
- Rectlinear grid (non-linear)  
- Structured grid (curvlinear grid): geometry location should be specified  
- Unstructured grid): topological and gemoetry should be informed  
  
### Geometry  
  
- Specifies info about the shape of items, with explicit spatial positions (maps, geography)  
- Often includes hierarchical structure (ex. 행정구역)  
- GDP에 따른 나라 크기 distortion → 여전히 영국으로 인식되도록.  
  
### Combinations  
  
set: unordered group of items  
  
list: ordered items  
  
cluster: group based on attribute similarity  
  
path: ordered set + link  
  
compound network: network with associated tree  
  
---  
  
## Data Abstraction  
  
- Domain specific to GENERIC  
- translate domain-specific terms into words as `generic` as possible  
  
## Data Availability  
  
- Static file: available at once  
- Dynamic streams (ex. 실시간으로 변하는 Network)  
  
---  
  
## Attribute Types  
  
Categorical, ordered (ordinal, quantitative)  
  
→ ordering direction (sequential, diverging, cyclic)  
  
다른 책: Hierarchical attributes: within an attribute, or between multiple attributes (ex. ms, us, ns)  
  
---  
  
### Levels of measurement  
  
(1) Nominal: only named  
  
- Name, categorical  
  
(2) Ordinal: can be ordered  
  
- Rank, Size  
  
(3) Interval: distance is meaningful  
  
- Temperature  
  
(4) Ratio: Absolute zero  
  
- Weight  
  
---  
  
## Semantics (Key / Value)  
  
for attributes  
  
### Key Attribute  
  
index used to look up value attributes  
  
- Implicit keys: keys are simply index in a row of the table  
- Explicit keys: UUID, unique ordinal or categorical keys  
  
### In Fields… however  
  
- Each cell represents `continuous data` distributed over domain.  
- Defined as `mapping from keys` to `values`  
- Multi `variate` structure depends on : # of value attribute  
- Multi `dimenstion` structure depends on: # of key attribute  
  
Scalar field, vector field, tensor field.  
  
## Semantic (Temporal)  
  
- temporal attribute: related to time  
- Complicated to handle  
    - Multiscale: ns to decade  
    - weeks don’t fit into months  
- Time-varying semantics: time is key attribute.  
    - not always spaced at uniform intervals! (응급실 등)  
- Dynamic
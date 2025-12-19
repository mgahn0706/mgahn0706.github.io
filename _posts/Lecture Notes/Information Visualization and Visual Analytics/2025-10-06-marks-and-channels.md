---  
tags:  
  - mark  
  - channel  
  - info-vis  
  - visualization  
  - design  
  - gestalt-principle  
  - preattentive  
share: "true"  
github_title: 2025-10-06-marks-and-channels  
title: 6. Marks and Channels  
date: 2025-10-06  
categories:  
  - Lecture Notes  
  - Information Visualization and Visual Analytics  
---  
## Why marks and channels?  
  
Every complex visual idiom can be broken into two orthogonal(?) components  
  
→ Marks and Channels  
  
## Marks  
  
- Basic graphical element.  
- Classified with their spatial dimension  
    - Point, Line, Area, Volume  
    - Actually, area and volume are also channel itself. (그럼 orthogonal 아닌거 아닌가…하지만 넘어갑시다)  
  
### Marks as Items/Nodes  
  
- Points  
- Lines  
- Areas  
  
### Marks as Links  
  
- Containment  
- Connection  
  
by Jacques Bertin  
  
---  
  
## Channels  
  
- A way to control the `appearance` of marks.  
      
- human perceptual system has two fundamentally different kinds of sensory modalities  
      
    - Identity (저게 뭐지)  
    - Magnitude (양 비교)  
- Position  
      
    - Horizontal, Vertical, Both  
- Color  
      
- Shape  
      
- Size  
      
    - Length, area, Volume  
- Tilt  
      
  
## So… Marks and Channels again?  
  
- Marks → geometric primitives  
- Channels → control appearance of marks  
- Interactions (they are dependent each other) (아니 그럼 더더욱 orthogonal한게 아니자너) → Shape and Size channels cannot be used  
    - `Area` marks are fully constrained. (state or province…)  
        - Cannot be sized or shape coding.  
    - `line` mark convey position and length.  
        - can only be size coded in 1D  
    - `point` marks only convey position.  
        - can be sized or shape coded.  
  
Note: this is vertical:position channel with line mark.  
  
---  
  
Note: People gaze at marks’ height  
  
---  
  
## Expressiveness and Effectiveness  
  
(3번째 나오는 중)  
  
- Expressiveness  
      
    - Vis idiom should express `all and only` information in the data attributes.  
    - match channel and data characteristics (identity channel, magnitude…)  
- Effectiveness  
      
    - Most important attributes should be encoded in most effective channels  
    - ex. Vis → Task → 5 Attribute가 제일 중요하다 → 중요도에 따라 effective channel을 Mapping 해야한다.  
    - 그럼 그 중요도는 어떻게 순위를 매길 것인가  
        - Accuracy  
        - Discriminability  
        - Separability  
        - Popout  
      
    ---  
      
  
    즉, expressiveness는 왼쪽 오른쪽 타입을 data type에 잘 맞추라는 거고,  
      
    effectiveness는 중요한 attribute에 대해 위쪽에 있는걸 쓰라는 말이겠군.  
      
  
---  
  
## Accuracy  
  
### Steven’s Power Law  
  
Channel accuracy by data type!  
  
### Crowdsourced Results  
  
- Position  
    - Bar chart within group  
    - Stack chart at bottom  
    - Bar chart between groups  
    - Stack chart both top  
    - Stack chart within group  
- Angle  
    - Pie Chart  
- Areas (Circular)  
- Areas (Rectangular)  
  
→ 어느정도 기존 연구와 동일한 순서임  
  
---  
  
## Discriminability  
  
Line width → only a few  
  
- Resolution을 1~2px 단위로 설정할 수 없다.  
  
## Separability, Integrality  
  
- Position + Hue: Fully Separable  
- Red + Green: Integral Hue  
  
  
  
---  
  
## Preattentive Processing (Popout)  
  
- Cognitive operations done preattentively, without focused attention  
  
→ popout effect, segmentation effect  
  
- Parallel processing on many individual channels  
    - speed independent on # of distractor  
    - speed depends on channel and amount of channel difference  
- Serial search depends on # of distractor → Almost all combination  
  
---  
  
## Gestalt Psychology  
  
the whole is different from the sum of its parts.  
  
→ How it affects?  
  
1. Containment  
2. Connection  
3. Proximity (spatial region이 비슷하면 하나의 group)  
4. Similarity (같은 shape, color면 하나의 group)  
  
---  
  
## Graphic Design  
  
### Contrast  
  
guide the users’ attention to key element by contrast  
  
→ preattentive  
  
### Repetition  
  
create visual consistency  
  
### Alignment  
  
important, because position is most effective channel!  
  
→ Creates visual connection  
  
## Weber’s Law  
  
- Perceptual system mostly operates with relative judgements, not absolute.  
  
→ Perceived change is propitional to relative stimuli.  
  
원래 길이가 길면 그 차이를 더 크게 줘야한다. (원 자극이 컸다면 차이를 just noticeable하게 해주기 위해 더 큰 변화를 줘야함)  
  
$$ \frac{\delta I}{I} = K $$  
  
  
I is intensity.  
  
---  
  
## Lightness Constancy  
  
Luminance는 perceived lightness와 무관하다.  
  
→ 검은 종이가 밖에 있는 것과 흰 종이가 실내에 있는것.  
  
1. Photoreceptor adaptation: 막대세포와 원추세포가 알아서 적응함  
2. Relative coding: 주변 환경에 비해 얼마나 밝은지 해석 (비율 고려)  
3. Perceptual Consistency: 벽이 흰색인걸 알고 있다면 그 기억을 이용
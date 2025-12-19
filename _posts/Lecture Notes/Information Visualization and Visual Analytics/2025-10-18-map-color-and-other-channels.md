---  
tags:  
  - info-vis  
  - visualization  
  - color  
  - design  
  - channel  
share: "true"  
github_title: 2025-10-18-map-color-and-other-channels  
title: 8. Map Color and Other Channels  
date: 2025-10-18  
categories:  
  - Lecture Notes  
  - Information Visualization and Visual Analytics  
---  
## Design Choice for Mapping → Colors  
  
## Rods and Cones  
  
- Rods  
    - 막대세포  
    - active at low light levels  
    - one wavelength sensitivity function  
    - 100 million rod receptors  
- Cones  
    - 원뿔세포  
    - 3 cone response signals  
    - three types  
    - 6 million  
    - focused in the center of vision (fovea)  
  
---  
  
## Terms  
  
### Luminance (조도)  
  
- Physically measured amount of light (lux로 측정되는 그것)  
  
### Brightness (밝기)  
  
- Perceived amount of light  
- non-linear (adaptation, contrast)  
  
### Lightness (명도)  
  
- Perceived refelctance of a surface  
- depends on a reference light  
- white surface is light, black surface is dark  
  
### Hue  
  
- color  
  
### Saturation  
  
- Perceived intensity of specific color  
- vividness  
  
---  
  
### We change meters  
  
eye sensitive over 9 orders of magnitude  
  
5 orders of magnitude → room ~ sunlight  
  
- Receptor bleach and become less sensitive  
  
→ We’re not light meters. 우리는 Meter를 바꾼다.  
  
- 신경체계는 신호의 차이를 계산한다.  
- 정확한 숫자 값을 계산하지 않는다.  
  
## Color Vision  
  
Rod: black-white. Low light settings  
  
Cone: color, normal light setting  
  
- Three opponent channel  
    - Red-green  
    - Blue-yellow  
    - Black-white  
- Luminance: high resolution  
- Chromaticity: low resolution  
  
---  
  
## Color Space  
  
Mathematical ways to describe color  
  
1. RGB: computationally easy. poor mechanics  
2. HSL: Hue, Saturation, Lightness  
    - Pseudo-perceptual  
3. HSV: Hue Saturation Value(for gray scale)  
4. CIEXYZ → 인간의 원뿔세포를 모델링하여, 인간이 인식 가능한 색상을 표현하기 위한 것이 있음.  
  
---  
  
## Three Independent Channel  
  
Retina contains three type of color receptors with different absorption spectra  
  
Input * Con → Three Values  
  
자극 그래프와 각 response 곡선을 곱하고, 적분하여 전체 값을 구한다.  
  
### Ambiguity in trichromacy  
  
→ input stimuli가 달라도 최종 인식된 값을 같게 만들 수 있다.  
  
matamerism.  
  
---  
  
## Model of Standard Observer  
  
Color matching experiment  
  
이 자극이면 평균적으로 이런 r,g,b를 갖더라.  
  
→ Color matching function 정의.  
  
### Primary Colors of Light  
  
- Red, green and blue (원뿔세포의 종류에 따라 r, g, b에 가까운 색에 반응하기 때문)  
    - L cones: 65%  
    - M cones: 33%  
    - S cones: 2%  
  
→ Color matching experiment에서 R을 음수로 해야하는 경우가 있음. (반대쪽에 R쏴주는 식으로 구현)  
  
### CIERGB Color System  
  
- Based on experimental results  
- R, G, B color를 사용하면 negative primary color를 사용하는 구간이 존재한다.  
  
→ Normalize  
  
경계는 단색광. (보라색 제외)  
  
사실 이 map은 perceptually uniform하지 않다.  
  
→ equally size step appear equal to our visual systems. (CIElab, CIEluv)  
  
---  
  
## Color Space  
  
HSL: popular color space.  
  
- pseudo-perceptual  
- L is different from true luminance  
  
→ L_a_n*  
  
좀 더 perceptual한 것을 반영.  
  
## Color Theory  
  
Luminance: physical light  
  
- Brightness: Perceptual light  
  
Saturation: Perceived intensity of specific color  
  
Hue: Wavelength  
  
### Luminance  
  
- As magnitude channel?  
    - Suitable for ordered data types  
    - But not accurate → quantitative에 부적합함.  
        - 많아야 5개임.  
    - resolving detail을 위해 밝기 대비.  
        - luminance가 비슷하면 글도 안읽힘. 3:1은 기본이고, 작은 텍스트라면 10:1  
  
→ Luminance is different from brightness  
  
- Brightness(밝기)는 인식된 것임. context와 환경에 강한 영향.  
  
### Saturation  
  
Magnitude of saturation  
  
- Low accuracy. 3단계 정도.  
  
크기 채널과 관련 있음  
  
- 사이즈가 찾을 때 saturation 알기 어려움  
- 밝고, 선명한 컬러는 작은 영역에  
- 흐린 파스텔 톤은 넓은 영역에  
  
### Hue  
  
as an identity channel  
  
- categorical data, grouping에 효과적.  
    - Spatial position 다음으로 효과적임 (nominal 한정)  
    - 특정 순서 없음. (빨주노초파남보는 학습된 것임)  
- 크기 챈널과 역시 인터랙션함  
    - 작으면 색깔 안보임  
- Continuous region에서 fine distinctions.  
- discontinuous에서는 lower accuracy. 약 6~7레벨  
  
### Cross-Cultural color naming  
  
→ consistent across culture  
  
white/black → red → ( green or yellow ) → blue → brown → ..  
  
### Color Categories  
  
Task: Name the colors!  
  
Only 8 hues named out of 210 colors. Small # of labels.  
  
### Color Coding  
  
Large areas: low sat. enough  
  
Small areas: high sat is needed.  
  
→ Break isoluminance with borders!  
  
Must have `luminance contrast` with background for details.  
  
### Transparency  
  
Interacts with other three channels  
  
- luminance, saturation, (hue). 투명도 바꾸면 이것도 사실상 바뀌는 것임.  
- Superimposed layers에 자주 사용.  
    - glassmorphism도 이와 유사한 듯.  
  
## Colormaps  
  
speicifies a mapping between color and value  
  
- Categorical  
- Ordered (sequential, diverging)  
- Continuous  
- Segmented  
  
### Color Brewer  
  
- Sequential scheme  
    - dark for high  
- Diverging scheme  
    - mid-range critical values and extremes at both ends of the data range  
- Qualitative scheme  
    - difference between class  
  
### Categorical Colormap  
  
- Encode categories at colors  
- 6 ~12 color max.  
  
**Difficulties in categorical colormaps**  
  
→ color should be close in luminance (major difference in salience, ensure against background)  
  
→ color should be different in luminance (distinguished even in black and white, color blind)  
  
**Resolve**  
  
- Distinguish bars in large region next to each other. vs distinguising non contiguous small regions  
  
→ not enough colors?  
  
1. reduce # of bins  
2. Use additional visual channels  
  
### Ordered Colormap  
  
Rainbow colormap is poor. 😟  
  
- Diverging: Two hues at end points, with neutral at midpoint  
- Sequential: Grayscale / Control saturation and brightness og single hue  
  
How many hues to use in ordered colormaps?  
  
→ Depends on what level should be emphasized (high, mid, low…)  
  
1. Many hues → Mid-level neighborhood structures are emphasized.  
    - Low-frequency are highlighted  
        - segmentation  
    - Easily discuss subranges  
2. Two hues (diverging) → High-level structures are emphasized  
    - Continuity  
    - Diverging color map  
  
### Again, Rainbow colormap is poor!  
  
easily namable color…but  
  
1. Hues don’t have implicit perceptual order  
2. Scale is not perceptually linear.  
3. `Fine detail` can not be perceived with only hues  
  
→ 사실 노란색 부분이 의미 없을 수 있다.  
  
→ 데이터 semantic 구조와, perception 구조가 다를 수 있다.  
  
따라서, 단조 증가 luminance colormap을 사용하고, multiple hue를 semantic에 맞게 사용하자.  
  
- popular interpolation은 perceptually nonlinear하다  
    - 물론 이걸 linear하게 바꾼 연구는 있지만, 칙칙해서 안쓴다.  
  
Then how to use?  
  
- Segmented rainbow colormaps are good categorical data.  
- Deliberately bin the data explicitly  
- or let eyes create bins  
  
## Color Deficiency  
  
- Deuteranope (green defict)  
- Protanope (red-green)  
- Tritanope (blue-yellow)  
  
Why color blindness?  
  
→ red green, yellow blue, black white 고장나기 쉬움  
  
- Most colorblind는 적록색맹이다. red-green color scheme을 쓰지 말자.  
  
## Size Channel  
  
- effective for ordered data  
- Affect most channels  
    - saturation, lhue  
    - shape  
    - orientation  
- 길이는 정확한, 넓이 부피는 부정확함  
- 더 큰 채널은 subsumes함  
  
## Angle Channel  
  
- Orientation of a mark  
- Sequential, diverging, cyclic  
- Accuracy is not uniform!  
    - vertical, horizontal, diagonal은 정확함  
    - 하지만, 다른건 아주 형편이 없음  
  
이런 orientation resolution은 45도일 때 최대임. 즉, 90도에 가까이 하면 이게 올라가는지 내려가는지 알기 어려움. aspect ratio가 중요하다 이말이다.  
  
---  
  
## Curvature, Shape Channel  
  
- Curvature: 아주 부정확함. 쓰지 마라.  
- Shape:  
    - point and line 위에서 identity channel로 작동 가능  
    - size와 shape에 strong interaction  
  
## Motion Channel  
  
- Direction , velocity, frequency  
- Salient, separable from other states  
    - Draws too much attention.  
        - 그래서 bi-state로 쓰는게 좋음. (움직인다, 안움직인다)  
- Used for `highlighting`  
    - blinking (의료 도메인에서 변화 파악)  
    - transitory vs ongoing  
  
## Texture and Stippling Channel  
  
Texture  
  
- Very small-scale pattenrs  
- Categorical attributes (order도 가능.. density 조절하면 됨)  
  
Stippling  
  
- Fill in regions of drawing with small strokes  
- Used at older printing tech. (점묘화 같음)
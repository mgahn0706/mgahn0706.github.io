---  
tags:  
  - glyph  
  - html  
share: "true"  
github_title: 2023-05-23-what-is-glyph-tag  
title: What is <glyph> tag  
date: 2023-05-23  
categories:  
  - Development  
  - Web  
---  
  
 아이콘이 fontello.svg에서 <glyph>로 선언되어있는 것을 보았다.  
  
glyph는 처음 보는 태그다. 얘는 뭐하는 친구일까.  
  
  
  
SVG로 웹 폰트를 해결하고자 나온 친구.  
  
SVG font에서 하나의 Glyph를 지정하기 위해 나온 tag입니다. 이제 Deprecated 되었습니다.  
  
하나의 glyph 태그는 폰트에서의 ‘글리프’ 를 정의합니다.  
  
폰트에서 하나의 글자 단위를 글리프라고 하는데, svg를 이용한 폰트에서 하나의 글리프를 정해줍니다.  
  
```  
<svg  
  width="400px"  
  height="300px"  
  version="1.1"  
  xmlns="<http://www.w3.org/2000/svg>">  
  <!-- Example copied from <https://www.w3.org/TR/SVG/fonts.html#GlyphElement> -->  
  <defs>  
    <font id="Font1" horiz-adv-x="1000">  
      <font-face  
        font-family="Super Sans"  
        font-weight="bold"  
        font-style="normal"  
        units-per-em="1000"  
        cap-height="600"  
        x-height="400"  
        ascent="700"  
        descent="300"  
        alphabetic="0"  
        mathematical="350"  
        ideographic="400"  
        hanging="500">  
        <font-face-src>  
          <font-face-name name="Super Sans Bold" />  
        </font-face-src>  
      </font-face>  
  
      <missing-glyph><path d="M0,0h200v200h-200z" /></missing-glyph>  
      <glyph unicode="!" horiz-adv-x="80" d="M0,0h200v200h-200z"></glyph>  
      <glyph unicode="@" d="M0,50l100,300l400,100z"></glyph>  
    </font>  
  </defs>  
  <text  
    x="100"  
    y="100"  
    style="font-family: 'Super Sans', Helvetica, sans-serif;  
             font-weight: bold; font-style: normal">  
    Text using embedded font!  
  </text>  
</svg>  
```  
  
폰트 자체를 svg로 정의해서 쓸 수 있고, 정의할 때 글리프(글자 1개)를 지정해주는 것이 glyph 태그입니다.  
  
위의 예시에서, `<glyph unicode=”!” ></glyph>`를 통해서 느낌표의 폰트를 지정해주는 것을 확인할 수 있습니다.  
  
제가 봐쏜 코드에서는 [fontello](https://fontello.com/)를 이용해 커스텀 아이콘을 폰트로써 이용하기 위해 사용했습니다.  
  
### 참고자료  
  
---  
  
[https://developer.mozilla.org/en-US/docs/Web/SVG/Element/glyph](https://developer.mozilla.org/en-US/docs/Web/SVG/Element/glyph)
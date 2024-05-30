---  
tags:  
  - glasmorphism  
  - design  
share: "true"  
github_title: 2023-10-16-glassmorphism  
title: Glassmorphism  
date: 2023-10-16  
categories:  
  - Development  
  - HCI  
---  
  
  
**개요**  
유리의 디자인적인 특성을 이용하는 스타일.  
오브젝트에 반투명, 또는 투명한 느낌을 주어 유리에 비치는 듯하게 하는 디자인 스타일을 말한다.  
  
Window Vista와 macOS에서 `Acrylic` 이라는 이름으로 사용되어 많은 인기를 끌게 되었다. 당장 mac의 아래 부분도 글래스모피즘이 적용되었다.  
  
[Acrylic material - Windows apps](https://learn.microsoft.com/en-us/windows/apps/design/style/acrylic)  
  
아크릴을 적용하여 깊이(depth)를 추가하고 시각적인 계층을 설정할 수 있다.  
  
**구성요소(조건)** 단순히 투명도나 블러 처리를 한다고 다 유리가 되지는 않는다.  
  
[UX Collective](https://uxdesign.cc/glassmorphism-in-user-interfaces-1f39bb1308c9)에서는 조건을 아래와 같이 얘기한다.  
  
> 조건  
>   
> - Transparency (frosted-glass effect using a Background Blur)  
> - Multi-layered approach with objects floating in space  
> - Vivid colors to highlight the blurred transparency  
> - A subtle, light border on the translucent objects.  
  
배경 블러를 통한 투명도 조절, 공간상에서 떠있는 오브젝트, 블러를 강조하기 위한 vivid한 컬러, 아주 얇고 약한 border를 조건으로 뽑는다.  
  
  
![](../../assets/img/posts/Pasted%20image%2020240530141718.png)  
  
위 그림은 앞서 언급한 4가지 조건을 만족한 예쁜(?) 글래스모피즘이 적용된 카드이다.  
  
구현 시 확인해야할 사항들은 아래에 잘 정리되어있었다.  
  
[https://brunch.co.kr/@everiwon/10](https://brunch.co.kr/@everiwon/10)  
  
이런 글래스모피즘을 사용하는 케이스는 2가지가 있다.  
  
- Background  
  
![](../../assets/img/posts/Pasted%20image%2020240530141513.png)  
- In-app  
  
![](../../assets/img/posts/Pasted%20image%2020240530141459.png)  
  
background는 배경과 다른 창을 표시하여 애플리케이션 창 사이에 깊이를 추가할 수 있는 것을 볼 수 있다. 한편, in-app 형식으로 사용한다면 앱 프레임 내부에 깊이감을 주고, 포커스와 계층을 제공할 수 있다.  
  
단, 이미 글래스모피즘을 적용한 곳에 또다른 글래스모피즘을 적용하지 않을 것을 권고하고 있다.  
  
**그렇다면 이런 글래스모피즘은 언제 사용하는게 좋을까?**  
  
- 스크롤과 같은 interaction 시 콘텐츠가 겹칠 수 있는 표면에 사용하면 좋다  
- 팝업, 플라이아웃, 빠르게 닫히는 UI에 background 글래스모피즘을 사용하면 좋다.  
  
위의 케이스는 헤더(토스 등)에서 잘 볼 수 있었다.  
  
![](../../assets/img/posts/Pasted%20image%2020240530141429.png)  
  
  
아래의 케이스는 macOS 등에서 ‘곧 닫힐만한 것’을 표현하는데 많이 볼 수 있었다.  
  
![](../../assets/img/posts/Pasted%20image%2020240530141328.png)  
이런 글래스모피즘은 프로덕트 디자인뿐만 아니라 디자인 전 영역에 잘 쓰이고 있다.   
  
참고자료  
[https://learn.microsoft.com/en-us/windows/apps/design/style/acrylic](https://learn.microsoft.com/en-us/windows/apps/design/style/acrylic)
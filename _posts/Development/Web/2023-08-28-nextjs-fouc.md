---  
tags:  
  - web  
  - nextjs  
share: "true"  
github_title: 2023-08-28-nextjs-fouc  
title: Next.js의 Flash of Unstyled Content 해결하기  
date: 2023-04-25  
categories:  
  - Development  
  - Web  
---  
### 찾아보거나 알게된 배경  
  
---  
  
Next.js와 Styled Component를 같이 사용하고 있는 개발환경에서, 자꾸 페이지를 로드할때 마다  
  
스타일 적용이 안된 화면이 깜빡깜빡 나타났다 없어지는 현상이 생겼다.  
  
### 요약  
  
---  
  
**Flash of Unstyled Content(FoUC)**  
  
위 현상은 페이지의 <style/> 이 페이지 로드 시 나타나지 않아 잠시동안 스타일 적용 안된 페이지가 나타나는 현상을 말합니다.  
  
**Why?**  
  
Next.js는 Server-side rendering으로, 서버에서 미리 페이지를 render해서 주기 때문에 HTML 렌더링이 클라이언트에게 오기 전에 이루어진다. 그런데 css-in-js를 사용하는 경우 Hydration 시의 js 코드를 바탕으로 스타일링이 되기 때문에 그 잠깐의 시간동안 style 적용이 안된 화면이 나타나게 된다.  
  
**Why should I fix this?**  
  
UX에 안좋다. 😕  
  
다행히도 styled-component는 SSR을 지원한다.  
  
[Architecture: Next.js Compiler](https://nextjs.org/docs/architecture/nextjs-compiler#supported-features)  
  
위와 같이, nextjs.config 파일에서 compiler 설정에 `styled-component: true` 를 설정해주면 ssr을 간단하게 적용할 수 있다.  
  
그 후 document.js에 아래 예시처럼 설정해줄 것을 설명해주고 있다.  
  
```jsx  
import Document, { DocumentContext } from 'next/document'  
import { ServerStyleSheet } from 'styled-components'  
  
export default class MyDocument extends Document {  
  static async getInitialProps(ctx: DocumentContext) {  
    const sheet = new ServerStyleSheet()  
    const originalRenderPage = ctx.renderPage  
  
    try {  
      ctx.renderPage = () =>  
        originalRenderPage({  
          enhanceApp: (App) => (props) =>  
            sheet.collectStyles(<App {...props} />),  
        })  
  
      const initialProps = await Document.getInitialProps(ctx)  
      return {  
        ...initialProps,  
        styles: [initialProps.styles, sheet.getStyleElement()],  
      }  
    } finally {  
      sheet.seal()  
    }  
  }  
}  
```  
  
성공적으로 개선되었다.  
  
다른 css-in-js 스타일링 라이브러리가 어떻게 하는지는 다음에 알아보도록 하겠습니다.  
  
### 참고자료  
  
---  
  
[https://nextjs.org/docs/architecture/nextjs-compiler#supported-features](https://nextjs.org/docs/architecture/nextjs-compiler#supported-features)  
  
[https://nextjs.org/docs/app/building-your-application/styling/css-in-js](https://nextjs.org/docs/app/building-your-application/styling/css-in-js)
---  
tags:  
  - nextjs  
  - route  
  - web  
share: "true"  
github_title: 2023-07-09-dynamic-router-in-nextjs  
title: Next.js에서 Dynamic Router 활용하기  
date: 2023-07-09  
categories:  
  - Development  
  - Web  
---  
### 찾아보거나 알게된 배경  
  
---  
  
Next.js를 사용하는데, URL params에 들어있는 값을 가져와야하는 경우가 생겼다.  
  
Next.js는 디렉토리 구조가 곧 라우터인데 `modusign/document/{id}` 형식의 경우에는 파일을 일일이 만들어 줄 수 없는 노릇이다. 파일구조는 정적일 수 밖에 없는데 어떻게 동적으로 라우팅을 할 수 있을까  
  
### 요약  
  
---  
  
한줄요약: 파일 명을 대괄호로 감싼다. ex) [id].tsx  
  
`menu/{id}` 의 형식으로 데이터를 받고 싶다면 menu 폴더에 [id].tsx 파일을 넣으면 된다.  
  
이때 `const { id } = router.query` 를 이용하여 쿼리에서 값을 받아올 수 있다.  
  
추가로, 이용하고자 하는 값이 하나의 param이 아닌 경우나, `/id/a/b/c` 같이 여러가지가 붙어있는 경우도 가능하다.  
  
`[…id]`.tsx 파일을 만든다면 배열로 router.query에서 각 값들을 가져올 수 있게 된다.  
  
Next 좋아요 👍  
  
### 참고자료  
  
---  
  
[https://nextjs.org/docs/pages/building-your-application/routing/dynamic-routes](https://nextjs.org/docs/pages/building-your-application/routing/dynamic-routes)
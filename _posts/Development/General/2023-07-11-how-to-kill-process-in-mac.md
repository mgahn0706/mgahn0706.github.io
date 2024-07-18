---  
tags:  
  - process  
  - port  
share: "true"  
github_title: 2023-07-11-how-to-kill-process-in-mac  
title: How to kill process in Mac  
date: 2023-07-11  
categories:  
  - Development  
  - General  
---  
### 찾아보거나 알게된 배경  
  
---  
  
개발 중, `yarn start` 로 로컬 서버를 돌리려고 했다.  
  
그런데, 이미 port 3000이 있다면서 3001에 돌릴 것인지 물어보는 메시지가 나왔다.  
  
어떻게하면 3000 포트의 프로세스를 죽일 수 있을까?  
  
### 요약  
  
---  
  
```jsx  
$ lsof -i tcp:3000  
$ kill -9 PID  
```  
  
상세 설명  
  
- `lsof` : list of files; 시스템에서 열린 파일 목록을 확인할 수 있으며, 사용하고 있는 프로세스를 알 수 있다.  
- `-i` : 특정 IP를 select한다는 의미의 옵션이다.  
- `tcp:3000`: 포트가 3000인 곳 → tcp이면서 3000 포트를 사용하는 곳의 ip만을 골라서 프로세스들을 보여줘  
  
여기서 나온 PID를 확인하여 kill 해주면 된다  
  
- `-9` : kill의 옵션이다. Kill은 프로세스에 어떤 signal을 보내는데 9번 옵션이 `SIGKILL(프로세스 죽이기)` 이다.  
  
### 참고자료  
  
---  
  
[https://stackoverflow.com/questions/39322089/node-js-port-3000-already-in-use-but-it-actually-isnt](https://stackoverflow.com/questions/39322089/node-js-port-3000-already-in-use-but-it-actually-isnt)
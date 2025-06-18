---  
tags:  
  - git  
share: "true"  
github_title: 2024-06-24-git-filter-branch  
title: Git-filter-branch  
date: 2024-06-24  
categories:  
  - Development  
  - General  
---  
### 요약  
  
---  
  
git revision history를 주어진 조건에 맞추어 필터할 수 있게 하는 깃 명령어.  
  
필터를 통해 tree나 각 commit의 정보를 바탕으로 브랜치를 필터할 수 있다.  
  
필터를 아무것도 적용하지 않고 실행한다면 아무 영향이 없을 것이다. 그럼에도 git의 버그등을 고칠 때 사용할 수 는 있다고 한다.  
  
rewritten된 history는 이전 브랜치들과 다른 이름을 가질 것이라서 기존 브랜치를 커버할 수 없다.  
  
즉, 커밋 몇개 없애겠다고 git-branch-filter 쓰면 안된다.  
  
레포 분리와 같이 특수한 경우에만 사용하는 것이 좋으며, 그렇지 않은 경우에는 그냥 커밋을 하는게 더 좋을 수 있다.  
  
### 필터 옵션  
  
---  
  
`—setup <command>` : 커맨드를 시작하기 전에 한 번 실행되는 command  
  
`--subdirectory-filter <dir>` : 주어진 디렉토리를 touch(해당 디렉토리 하위의 파일 수정 등)한 커밋만 남긴다. 이번 레포 분리하면서 쓸 커맨드는 이거일듯  
  
`--env-filter <command>` : 커밋이 실행되는 환경을 수정해야할때 유용. (ex. env, author, committer name 등)  
  
`--tree-filter <command>` , `--parent-filter` , `--commit -filter` 등 여러 조건으로 필터링할 수 있으니 브랜치의 커밋을 필터해야할 때 찾아보면 좋다.  
  
[Git - git-filter-branch Documentation](https://git-scm.com/docs/git-filter-branch#_options)  
  
### 예시  
  
---  
  
`git filter-branch --subdirectory-filter form-cms -- --all`  
  
### 참고자료  
  
---  
  
[https://git-scm.com/docs/git-filter-branch](https://git-scm.com/docs/git-filter-branch)
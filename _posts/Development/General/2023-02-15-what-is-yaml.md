---  
tags:  
  - yaml  
  - workflow  
share: "true"  
github_title: 2023-02-15-what-is-yaml  
title: YAML이 뭘까요  
date: 2023-02-15  
categories:  
  - Development  
  - General  
---  
  
배포 workflow를 YAML로 관리하는 것을 보고 YAML이 무엇인지 알아보기로 했다.  
  
### 요약  
  
---  
  
- What is YAML.  
      
    YAML은 JSON의 불편한 점을 보완하기 위해 나온 JSON의 superset이다.  
      
    Superset이기 때문에 JSON과 기본적으로 같다. 좀 더 편리해졌다.  
      
    - 주석을 달 수 있게 되었다. JSON에서는 달 수가 없어 이 설정파일이 뭔지 알기 힘들다  
    - 모든 문자열에 “”(따옴표)가 강제되지 않게 된다.  
    - 중괄호를 꼭 감싸줄 필요가 사라졌다.  
    - 쉼표로 각 프로퍼티들을 모두 구분해주지 않아도 된다.  
- How  
      
    ```yaml  
    on:  
    	push:  
    		branches:  
    			- 'main' #main에 push 될 때라는 뜻이다. 이렇게 주석도 쓸 수 있다  
    jobs:  
    	build:  
    		runs-on: ubuntu-latest  
    		timeout-minutes: 10  
    		steps:  
    			- uses: actions/...  #배열 아이템은 - 로 구별한다.  
    			- name: BuildExample  
    				run : blah blah	#객체는 들여쓰고 ':' 를 쓰는 것으로 구분한다.   
    ```  
      
  
위 YAML의 JSON 표현은 아래와 같다.  
  
```json  
{  
"on": {  
			"push": {  
					"branches": [ "main" ]   
			}  
},  
"jobs": {  
			"build" : {  
						"runs-on" : "ubuntu-latest",  
						"timeout-minutes": 10,  
						"steps": [  
							{ "uses": "actions/..."},  
							{ "name" : "BuildExample",  
								"run" : "blah blah"  
							}  
						]  
				}  
		}  
}  
```  
  
~~아휴 귀찮아~~  
  
한번 써보니 왜 YAML이 나오게 되었는지 바로 알게 되었다.  
  
띄어쓰기와 인덴트가 문법으로 들어간다. 파이썬과 비슷하다는 생각이 들었다.  
  
- 어디에 사용될까  
      
    GitHub Action 설정파일에 사용하고 있다. 주석등을 달아 코드 의도를 드러내기도 쉽고. 읽고 쓰기 간편해서 사용되고 있다.  
      
  
→ 설정파일에 적합하다면 왜 npm에서 package.yaml을 안쓰고 package.json을 기본으로 쓸까?  
  
[https://github.com/npm/npm/issues/3336](https://github.com/npm/npm/issues/3336)  
  
[https://github.com/npm/npm/issues/5901](https://github.com/npm/npm/issues/5901)  
  
5년전에 논쟁하고 있었다. “주석기능도 있고 config 파일로 YAML이 더 적합하니 추가하자” 와 “이미 잘 되고 있으니 굳이 추가하지 않는다”의 의견이 갈렸다. 🤔  
  
- 단점  
    - 인덴트로 구분하기 때문에 depths가 많아지면 읽기 힘들다  
  
### 참고자료  
  
---  
  
[https://yaml.org/](https://yaml.org/) [https://www.redhat.com/en/topics/automation/what-is-yaml](https://www.redhat.com/en/topics/automation/what-is-yaml)
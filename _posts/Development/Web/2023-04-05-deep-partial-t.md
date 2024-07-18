---  
tags:  
  - typescript  
share: "true"  
github_title: 2023-04-05-deep-partial-t  
title: DeepPartial<T>  
date: 2023-04-05  
categories:  
  - Development  
  - Web  
---  
### 요약  
  
---  
  
Partial<T>는 어떤 type T에 대하여 모든 property를 optional하게 바꿔줍니다.  
  
```  
type Partial<T> = {  
    [P in keyof T]?: T[P];  
};  
```  
  
위와 같이 구현됩니다. 각 프로퍼티가 optional 하게 변경되는 것을 볼 수 있습니다.  
  
```tsx  
interface Document {  
	id: string;  
	signer: string;  
	requester: string;  
};   
  
const a : Document = {  
	id: "11111",  
	requester: "force"  
}; // ERROR: Property 'signer' is missing in type '{ id: string; requester: string; }' but required in type 'Document'.  
  
const b : Partial<Document> = {  
	id: "22222",  
	requester: "force"  
} // OK, signer는 optional이기 때문  
```  
  
DeepPartial<T>는 어떤 type T에 대해 하위 property를 모두 포함하여 optional하게 바꿔줍니다.  
  
typescript에서 바로 지원해주는 건 아니고, 각 라이브러리에서 제공하는 경우가 많습니다.  
  
```tsx  
type DeepPartial<T> = T extends Function ? T : T extends Array<infer U> ? _DeepPartialArray<U> : T extends object ? _DeepPartialObject<T> : T | undefined  
```  
  
```tsx  
interface Document {  
	id: string;  
	attachment: {title: string; id: string;}  
}  
  
const a : Partial<Document> = {  
	id: "11111",  
	attachment: {title: "제목"}  
}; // ERROR : Property 'id' is missing in type '{ title: string; }' but required in type '{ title: string; id: string; }'.  
  
const b : DeepPartial<Document> = {  
	id: "22222",  
	attachment: {title: "제목"}  
}; // OK  
```  
  
이런 Utility Type을 적절히 사용하면 중복되고 유사한 type 정의를 줄일 수 있고, 좀 더 명확하게 type을 설정할 수 있게됩니다.  
  
### 참고자료  
  
---  
  
[https://www.typescriptlang.org/docs/handbook/utility-types.html](https://www.typescriptlang.org/docs/handbook/utility-types.html)
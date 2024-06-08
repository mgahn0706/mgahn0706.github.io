---  
tags:  
  - redis  
  - server  
share: "true"  
github_title: 2023-07-24-what-is-redis  
title: Redis가 뭔가요  
date: 2023-07-24  
categories:  
  - Development  
  - Server  
---  
Redis는 `메모리 기반 key-value store` 입니다.  
  
**NoSQL: key-value** 먼저, SQL과 NoSQL에 대해서 알아보았습니다.  
  
![](../../assets/img/posts/Pasted%20image%2020240603130631.png)  
  
  위와 같이 row와 column으로 이루어진 데이터베이스를 관계형 데이터베이스(Relational Database)라고 합니다. 이 데이터베이스를 관리하기 위한 언어가 SQL (structured query language) 입니다. SQL을 통해 데이터의 생성, 검색, 수정, 삭제 를 수행할 수 있습니다.  
  
그렇다면, NoSQL은 무엇일까요? NoSQL은 기존 RDB에 부가적인 기능을 더 제공해줍니다. NoSQL에는 여러 종류가 있지만, Redis는 그 중 Key-value 데이터베이스를 다루고 있습니다.  
  
**Redis REDIS는 Re**mote **Di**ctionary **S**erver의 약자로, **원격 Dictinary 자료구조 서버** 라는 뜻입니다. key로 데이터를 조회하여 값을 얻을 수 있는데, key는 string 타입입니다.  
  
Redis는 Memory 위에서 작동합니다.  
  
> To achieve top performance, Redis works with an **in-memory dataset**. Depending on your use case, Redis can persist your data either by periodically [**dumping the dataset to disk**](https://redis.io/topics/persistence#snapshotting) or by [**appending each command to a disk-based log**](https://redis.io/topics/persistence#append-only-file). You can also disable persistence if you just need a feature-rich, networked, in-memory cache.  
  
그렇기때문에 Disk에서 불러오는 것보다는 훨씬 데이터 입출력이 빠를 것입니다.  
  
또, In-memory database 특성 상 데이터가 휘발될 것이라 예상했는데 따로 설정을 통해 disk에 저장하여 영속성을 챙길 수 있다고 합니다.  
  
데이터를 실시간으로 업데이트 할 수 있고 복제도 할 수 있습니다.  
  
다만, 메모리가 비싸서 값이 많이 나가고, 캐시 데이터를 자주 지워줘야하는데 이를 잘못 사용하다가 문제가 발생할 위험이 높습니다.   
  
저는 메시지 큐(BullMQ)를 사용하기 위해서 Redis를 선택하였습니다.  
  
### 참고자료  
  
---  
  
[https://redis.com/redis-enterprise/data-structures/](https://redis.com/redis-enterprise/data-structures/)
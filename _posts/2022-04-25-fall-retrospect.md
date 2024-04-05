---  
tags:  
  - reflection  
share: "true"  
github_title: 2022-04-25-fall-retrospect  
title: 2021년 가을학기를 마치며  
date: 2022-04-25  
categories:  
  - Self Reflection  
  - Semester  
---  
  
  
2022년 4월에 쓰는 2021년 2학기 회고록. 요즘 컴공쪽 프론트엔드 코딩만 하다보니 전공지식이 풍화해가는걸 느낀다. 이렇게라도 복기해봐야지.  
  
---  
  
###   **논리설계 및 실습**  
  
![](https://t1.daumcdn.net/keditor/emoticon/friends1/large/012.gif)  
  
  ~기억이 안나~  
  
기본적인 low-level에서의 논리를 다룬다. AND, OR Gate에서부터 K-map, Encoder와 Decoder 등 중간고사에서는 비메모리 분야를 다뤘다. 이후 기말에서는 메모리가 들어간 회로를 다루는데, PLA, RAM과 ROM, Comparator, Shifter, Flip-Flop 등을 다룬다. 더 나아가 컴퓨터 아키텍처쪽도 찍먹한 것으로 기억한다. 개념만 기억나고 회로 구성은 하나도 기억 안난다...컴공 친구들과 비교하면 우리는 물리적인 상태까지 좀 더 다루는 것 같다. RAM의 상태에 따라 전하 충전 여부정도 더 다루는 듯. 대신 컴공 친구들은 베릴로그를 좀 더 일찍 다룬다. 그 외의 차이는 없는 듯!  
  
[##_Image|kage@z4IDd/btrzX0ske4z/2vTksRKTI6iCFA5akmyu00/img.png|CDM|1.3|{"originWidth":665,"originHeight":734,"style":"alignCenter","width":372,"height":411,"caption":"요런거 10문제 정도 풀면 됨"}_##]  
  
  시험에서는 K-map 그리기, state diagram 설정해서 회로 만들기...그런거 10문제 정도를 타임어택으로 본 기억이있다. 회로이론때는 타임어택때 멸망했는데 논리설계는 노하우가 생겼는지 어려운거 잘 걸러가며 풀어서, 성적은 극혐하는 타임어택 시험치고 잘 나왔다. 물론 내가 잘한 것보다 수강생 200명이 다같이 망한 사실이 더 크지만.  
  
  실험은 비대면으로 실험 5주차까지는 솔직히 꿀빨면서 했다. 원래라면 빵판에다 해야하는 것 같은데 Circuit Lab이라는 온라인 회로 설계 사이트에서 파워포인트마냥 슥슥 그리고 보고서 제출하면 됐다. 비대면이었기에 기회실과 달리 보고서를 빡세게 쓸 필요는 없었다. 다만 6주차인가부터 베릴로그를 이용한 코딩을 해야했는데 그때 쫌 빡셌음.  
  
  논설실의 꽃은 프로젝트다. 매년 기상천외한 주제를 주는걸로 유명하다. 작년에는 블랙잭 구현으로 기억한다. 근데 올해는 나름(?) 쉬운 과제가 나왔다. **엘리베이터 회로 구현**이었는데 고딩때 많이 생각해놓은거라 시작은 어렵지 않게 할 수 있었다.  
  
[##_ImageGrid|kage@b2HQnm/btrzZ5soOP8/H1gXDo0oUvRAxZhe0sSOC0/img.png,kage@cAnytP/btrzYUZdPwp/eqIZ4glR6nRtzE69tW1mKk/img.png,kage@bkoRVk/btrzWr4Mj8A/jimRBYl4K2zShrdAPCPMg0/img.png|data-origin-width="1296" data-origin-height="927" data-is-animation="false" width="563" height="402" data-widthpercent="49.25" style="width: 48.1049%; margin-right: 10px;",data-origin-width="939" data-origin-height="1280" data-is-animation="false" style="width: 25.2418%; margin-right: 10px;" data-widthpercent="25.84",data-origin-width="905" data-origin-height="1280" data-is-animation="false" style="width: 24.3278%;" data-widthpercent="24.91"|당시 고생한 흔적들..._##]  
  
 난이도가 극악은 아니었고 악...악 정도였다. 덕분에 베릴로그는 참 잘 쓸 수 있다.  
  
[##_ImageGrid|kage@mBvGt/btrz0uZJ6fv/PrQxJxdjKFpHk5fG8BJKp1/img.png,kage@cCaHUk/btrzZAlQ6R8/Yjp5cXn774RKyR7pfwrewK/img.png|data-origin-width="1440" data-origin-height="1015" data-is-animation="false" style="width: 43.5372%; margin-right: 10px;" data-widthpercent="44.05",data-origin-width="1247" data-origin-height="692" data-is-animation="false" style="width: 55.3%;" data-widthpercent="55.95"|당시 성공 장면 ㅠㅠ_##]  
  
  전날 새벽 5시에 완성해서 기숙사에서 제출한 기억이 난다. 물론 그 다음날 자구기 시험을 바로 공부한 기억이 있다. 어째 추억이 다 과제나 플젝에서 나온다. 참 슬픈 일이다.   
  
[##_Image|kage@TgAVD/btrzUzuLelr/K28B6zKYdTcr1vdfE6rKOk/img.png|CDM|1.3|{"originWidth":502,"originHeight":503,"style":"alignCenter","width":352,"height":353,"caption":"암튼 됨."}_##]  
  
  구조는 정말 이상했고, 엘리베이터 사용자의 경험은 정말 무시한 코드였으나...암튼 돌아감. 암튼 됨 ㅋㅋ  
  
전체적으로 마인크래프트 레드스톤 다룬다고 보면 된다. 잼민이때 많이 해서 그런지 은근 나랑 잘 맞았다. 아키텍처쪽은 사실 고려하지 않고 있었는데 꽤나 매력적인 분야였다. 근데 디시설 듣기는 너무 무섭다 ㅎㅎ. 진로의 폭이 넓어졌다.  
  
---  
  
### **기초전자기학및연습**  
  
![](https://t1.daumcdn.net/keditor/emoticon/friends1/large/047.gif)  
  
  2학년 2학기가 되어서야 보통 사람들이 생각하는 "전기 전자"에 대한 물리학 지식을 겉핥기하게 되었다. 여태 전공은 공학과 실습에 초점이 맞춰져있다면 이건 쌩 물리학과 이론에 초점이 맞춰져있다. 1~2학년때 배워온 벡터 미적분을 활용해서 전기장, 자기장의 여러 solution을 푸는 방법을 배웠다. 기전연에서는 time-varying을 다루는 가우스법칙까진 다루진 않았다. 찍먹만 함 ㅇㅇ. 교수님께서 계산기 쓰는 계산보다는 physical meaning을 중요시 여겨서 물리학 전공 치고는 PDE같은 계산을 많이 안했다.   
  
  실습은 Matlab으로 여러 상황에서의 전자기장이나 에너지 등등을 시뮬레이션하는 거였다. matlab이랑 하나 더 썼는데 기억이 안나네. 실습은 딱 신기한 정도. 매트랩이 새로운 언어는 아니어서 CS적으로 배우거나 그런건 없었고 그냥 이론적으로 배운 전자기학 지식을 시뮬레이션해보고 "오..."하는 정도였다.  
  
  전자기학을 찍먹해보는 강의였고 성적은 전공 중에서 제일 잘...나왔지만 재밌고 흥미로워서라기보다는 계산이 아닌 의미 지향적인 문제가 많이 나와서 그런 것 같다. 그래도 공부 제일 많이 했는데 성적 잘 나와서 좋았다. 과연 내가 전자기학과 양자역학쪽으로 갈 것인가?는 잘 모르겠다. 양자컴퓨팅에도 관심이 있긴...한데 과연?  
  
---  
  
### **자료구조의 기초**  
  
  컴퓨터 전공자와 비전공자를 슬슬 가르기 시작하는 과목을 듣게 되었다. 첫번째 전공 선택 과목이다. 다양한 자료구조를 배운다. Time Complexity의 개념에서부터 Linked list, Stack, Queue, Tree, Hash, Sorting, Graph, topological sort, MST, Dijkstra, Bloom filter를 배웠다. 저 안에서도 엄청 나뉜다. 특히 트리...자료구조의 전반적인 개념과 분석법. 장단점, 간단한 구현 방법들에 대해서 배운다. 자료구조의 활용보다는 좀 더 time/space complexity나 수학적인 이론에 초점이 맞춰져있었다. 알고리즘은 따로 배우니까 그런듯?  
  
  이 강의 덕분에 매번 애매하게만 알고있었던 트리, 해시, 그래프에 대해 알게 되었다. 공부할때도 재밌었던 기억이 있는...데 논리설계때문에 시험공부를 충분히 못한 기억은 있다 ㅎㅎ. 퀴즈 3번정도를 평소에 봐서 다행이지...  
  
  실습은 3번 있었는데 하나는 Tree balancing, 또 하나는 Hash Table에서의 probing, 마지막은 merge sort 였던 것으로 기억한다. Tree는 AVL tree remove 통으로 날려서 70점인가 받았고 뒤에 2개 어찌저찌 잘해냈음 ㅇㅇ.  
  
  그리고 재밌어서 한 과목때문인지 성적도 들인 노력에 비해 전체적으로 잘나왔다. 매번 q2 넘은거는 첨이다.   
  
컴텍의 길을 좀 더 확고히 할 수 있었다. 컴공갈껄 그랬나.. 근데 아키텍쳐쪽도 재밌어서 어떻게 할지 모르겠네...    
  
근데 몇개월지난 지금은 기억이 안남... 그래도 구글링하면 다시 떠오르긴 한다.  
  
여담이지만 영강이었는데 교수님이 영어를 잘하셨다. 나도 영어 잘하고 싶다.  
  
---  
  
### **선형대수학**  
  
  수학1때 선형대수학 파트를 열심히 안했고...공학수학1도 미분방정식만 열심히 했지 선대 파트는 그냥 외운 느낌이라 수리과학부 전선인 선형대수학을 수강신청했다. 전기과 선형대수도 있지만 좀 더 수학적인 인싸이트를 받고 싶어 ~(좀 더 쉽다고 해서)~ 선택해보았다. 처음 접해보는 수학과 전공이라 좀 신기했다.  
  
  공학수학이나 공대에서는 문제 풀이와 활용법이 중요한 반면에 이 과목에서는 증명과 정리가 쏟아져 나왔다. 문제도 주어진 Theorem을 이용해서 새로운 사실을 증명하는 것이었다. 연습문제를 풀수록 '아 수학이 이렇게 발전되어온건가'라는 생각이 들었다. 프리드버그로 나갔는데 책 자체는 쉬웠다. 내가 공부를 안해서 글치...  
  
  얘는 첨으로 재수강 가능한 학점이 나왔다....ㅎㅎ ㅠㅠㅠ 이미 공학수학에서 애매하게 안 상태로 풀다가 B-를 받은 나는 차라리 재수강하겠다는 마음으로 기말을 봤다. 재수강할때는 근데 빨라야 2025년일텐데 다 까먹지 않을까...? 그래도 필기한게 있고 얻은게 없지는 않으니 나름 괜찮았다.   
  
---  
  
### **전기정보세미나2**  
  
  전기정보세미나1의 연장선이다. 교수님들께서 연구실에서 무슨무슨 연구를 하신다~ 설명. 학부생 2학년따리의 지식으로는 거의 이해할 수 없었지만, 그래도 대충 이런거 하는구나 정도는 알 수 있었다. 작년보다 인공지능과 딥러닝을 쓰는 연구실이 많아졌다. 특히, 새로오신 교수님 중에서 컴퓨터 비전과 통신쪽 연구하시는 분이 많이 계셨다. 이런 것도 요즘 기술 연구의 흐름을 따라가는 것일까. 랩인턴도 해보고싶은데, 어디서 할지 아직 못정했다.  
  
---  
  
그 외에도 영상 동아리도 했고, 와플스튜디오라는 개발 동아리의 루키 과정을 거쳤다. 사실 이게 더 빡셌음 ㅋㅋ ㅠㅠ  
  
와플에서 한 프로젝트 후기는 또 따로 적어봐야할듯. 자꾸 기록을 안해놓으니까 까먹네요.
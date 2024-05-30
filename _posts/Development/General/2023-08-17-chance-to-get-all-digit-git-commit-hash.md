---  
tags:  
  - fun  
  - math  
share: "true"  
github_title: 2023-08-17-chance-to-get-all-digit-git-commit-hash  
title: Chance to get All-digit Git Commit Hash  
date: 2023-08-17  
categories:  
  - Development  
  - General  
---  
### 배경  
  
---  
  
커밋을 했는데 깃헙에서 표시된 커밋 해시의 앞의 첫 8자리가 모두 숫자였다! 흔치 않은 일이었던 것 같은데 실제 확률은 얼마나 될까  
  
### 요약  
  
---  
  
1. git commit hash는 SHA1 을 사용한다. 변경사항에 따라서, unique한 string을 뱉는 것이다. 문자열은 16진수로, 0~9와 a~f까지로 표현되어있다.  
2. 구하고자 하는 상황의 문자열의 길이는 항상 8로 동일하다. 따라서, 우리는 각 자리에 문자가 정해질 때, 알파벳인지 숫자인지의 확률이 모두 같고, 독립적인지 확인하면 ‘모두 숫자인 커밋 해시’ 확률을 구할 수 있다.  
3. 아래와 같이 stackoverflow에서 가져온 php를 실행한다.  
  
```php  
<?php  
  
$n = '';  
$modu = 'I love Modusign';  
  
for ($i=0; $i<100000; $i++) {  
   $n .= sha1($i . $modu, false);  
}     
  
$count = count_chars($n, 1);  
$sum = array_sum($count);  
  
foreach ($count as $k => $v) {  
    echo chr($k)." => ".($v/$sum)."\\n";  
}   
  
?>  
```  
  
실행 결과,  
  
```php  
0 => 0.06258175  
1 => 0.062556  
2 => 0.06254075  
3 => 0.062574  
4 => 0.06249275  
5 => 0.06262275  
6 => 0.062561  
7 => 0.06240775  
8 => 0.06272775  
9 => 0.06224675  
a => 0.0624735  
b => 0.062325  
c => 0.062454  
d => 0.0624095  
e => 0.06254  
f => 0.06248675  
```  
  
확률의 차이는  
  
$10^{-4}$ 수준으로 균등하다고 보는 게 좋을 것 같다. 또, 확률을 구할 때 ‘한 SHA1알고리즘에서 생성된 문자열에 있는 특정 문자 개수’를 구했으므로, 만약 숫자나 영어가 나올 확률이 서로 독립이 아니라면 확률이 균등하게 나오지 않았을 것이다. 모두 확률이 같은 독립시행이므로 확률을 단순히 곱해서 계산할 수 있을 것이다.  
  
4. 0~f 의 16개 문자 중, 숫자는 10개, 문자는 6개이다. 따라서, 앞의 8자리가 모두 숫자일 확률은  
  
(10/16)^8 ~= **2.3% ,** 커밋 50번 정도 하면 1번쯤 나올만한 확률이다. 생각보다 높다.  
  
추가로, 모두 문자가 나올 확률은 **0.4%** 로, 250번 커밋했을 때 1번 쯤 나올 수 있다.  
  
### 참고자료  
  
---  
  
[https://stackoverflow.com/questions/11768809/randomness-of-hashing-functions-such-as-sha1](https://stackoverflow.com/questions/11768809/randomness-of-hashing-functions-such-as-sha1)
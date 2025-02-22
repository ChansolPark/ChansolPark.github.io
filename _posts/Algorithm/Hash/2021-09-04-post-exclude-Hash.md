---
title: "Hash"
classes : wide
categories:
  - Hash
tags:
  - Hash
---

<br>
<h1>
- 해시 (Hash)
</h1>
<br>

- 해시는 컴퓨터 공학에서 매우 근본이 되는 알고리즘 중 하나.

  <br>

 - 해시란 임의의 크기를 가진 값을 고정크기에 값에 대응 시키는 함수이다.
  
  <br>
  
 - 입력 값이 같으면 출력되는 값도 항상 같아야 한다.
  
  <br>

 - 두개의 입력값이 같은 출력값을 가질수 있고 그 경우에 '충돌'이 일어났다고 한다.
  
  <br>

 - 하나의 입력값이 두개의 출력값을 가질 수는 없다. 
  
  <br>

   - 해시는 수학적 함수의 정의를 만족해야 하기 때문이다.
  
  


```c
/*
	해시 함수의 종류들은 다양하고 쓰임새도 다양하다. 
  크게는 암호학에 사용되는지 아닌지로 구분한다고 한다.
*/ 
```

  <br>
  <br>
<h1>
- 균일성
</h1>

- 해시의 출력값이 고르게 분포되는 정도를 말함.
   - 균일성은 높을수록 좋다.
  
  <br>

- 균일성의 측정은 카이제곱 검정을 이용. 
  - 결과가 0.95 ~ 1.05 사이면 균일성이 높은 해시함수라고 판단한다.
  
  <br>
- 눈 사태 효과
   - 눈 사태가 작은 눈덩이에서 시작해 엄청난 눈사태로 이어지듯 
   - 입력값의 사소한 차이에도 출력값에는 커다란 차이가 일어나는 것을 말한다.
  

  <br>
  <br>



```c
/*
	검색, 삽입, 삭제의 최악의 경우는 O(N)으로 해시 함수의 충돌이 일어난 경우의 시간복잡도라고 이해하였다.
    이 경우 빠르다 할순 없지만 해시테이블의 크기를 소수로 해주고 충분히 크게해주면 충돌의 경우는 굉장히 적다고 한다.
*/ 
```


---
title: "Vector"
categories:
  - C++
classes : wide
tags:
  - Template STL Library
---
   
<br>
<h1>
Vector 란
</h1>
<br>
  
- 템플릿 STL 라이브러리에 포함되는 컨테이너이다.

- 어떤 자료형도 넣을 수 있는 동적 배열이다. 

  - 요소 수가 증가함에 따라 자동으로 메모리를 관리해 준다는 점에서 기존 배열과 차이가 있다.

<br>
<h2>
Vector의 동적 메모리 관리 방식
</h2>
<br>

- 벡터에는 벡터의 크기값을 저장하는 Capacity와 Size변수가 있다. 

- 벡터의 Size는 실제 값이 들어있는 벡터의 크기를 말한다. 

  - ex) {1, 2, , , ,} 일 경우 Size = 2
  
<br>

- 벡터의 Capacity는 실제 메모리에 할당된 벡터의 크기값을 말한다.

  - 벡터의 요소 수가 증가함에 따라 재 할당이 일어나게 되는데, 재할당의 기준이 Size > Capacity 이다.

<br>
<h2>
Vector의 사용 지침
</h2>
<br>

- 벡터는 색인을 알고있을 경우 순서와 상관없이 임의적 접근이 가능하다. 

  - 색인을 알고 있다면 어떠한 요소를 찾을때 앞에서부터 찾을 필요가 없다.

<br>

- 그러나 벡터의 중간에 요소를 삽입, 삭제 할 경우 뒷 요소의 밀림/당겨짐 연산으로 인하여 느리다.  

- 또한 요소수의 증가가 빈번히 이뤄질 경우 재할당 과 요소 복사에 드는 비용을 무시할 수 없다. 

  - Vector를 사용할때 최대 크기를 알고있다면 Reserve함수를 이용해 크기를 정의하고 사용하길 권장한다. 

    - 재할당으로 인한 문제점을 해결할 수 있다.
  
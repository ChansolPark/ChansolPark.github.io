---
title: "Map"
categories:
  - C++
classes : wide
tags:
  - Template STL Library
---
   
<br>
<h1>
Map 란
</h1>
<br>
  
- 템플릿 STL 라이브러리에 포함되는 컨테이너이다.

- Key (색인)와 Value (값)의 쌍을 하나의 요소로 가지는 컨테이너이다. 

  - ex) 

  ```cpp

  std::map<std::string, int> exMap;
  exMap["EX"] = 10; // 요소 삽입 Key = EX, Value = 10

  ```

  - 키는 중복될 수 없다.

  - C++에서의 기본 Map은 이진 탐색트리 기반 자동 정렬되는 컨테이너이다.


<br>
<h2>
Map의 장점
</h2>
<br>

- std::list, std::vector보다 탐색 속도가 더 빠르다.

  - 순차 탐색하는 list와 vector와 달리 이진 탐색 트리 기반인 Map이 더 빠르다.
    - list, vector = O(N) | map = O(log N)
  
  - 자동으로 정렬됨

<br>


<br>
<h2>
Map의 단점
</h2>
<br>

- 해쉬 맵이 아님. 따라서 O(1)이 아님.
  - O(1) Map을 지원하기 위해 나온 것이 Unordered_Map.

<br>
<h2>
Unordered_Map
</h2>
<br>

- 해쉬 맵 기반의 컨테이너

  - std::map 과는 달리 O(1)을 지원. (이유는 Hash Post 참고)

- 자동 정렬되지 않음.

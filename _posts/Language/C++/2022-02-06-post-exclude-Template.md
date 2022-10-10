---
title: "Template"
categories:
  - C++
classes : wide
tags:
  - Template
---
   
<br>
<h1>
Template 란
</h1>
<br>
  
- Java와 Csharp에서의 제네릭 메서드 / 클래스와 비슷한 개념

- STL 컨테이너 또한 템플릿이다. 

- 코드가 자료형마다 중복되는 현상을 피할 수 있다.

<br>
<h1>
Template 작동 원리
</h1>
<br>

- 템틀릿이 인스턴스화 될 때 마다 컴파일러가 코드를 생성해준다.
  - 템플릿에 사용된 자료형의 가짓수에 비례해 exe파일의 크기가 증가한다.

<br>
<h1>
Template 특수화
</h1>
<br>

- 특정한 템플릿 매개변수를 받도록 커스터마이즈 할 수 있다.
  - ex)
  ```cpp
  template <class T>
  class Example<bool, T>  // bool 형을 받도록 커스터마이즈

  ```
 
- 출처 :  POCU 아카데미 강의
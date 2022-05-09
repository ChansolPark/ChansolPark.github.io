---
title: "Chapter2"
categories:
  - EffectiveCpp
tags:
  - C++
---

<h1>

- Chapter2 : 생성자, 소멸자 및 대입 연산자 

</h1>

<h2>
- C++가 은근슬쩍 만들어 호출해 버리는 함수들에 촉각을 세우자
</h2>

  -  컴파일러는 경우에 따라 클래스에 대해 기본 생성자, 복사 생성자, 복사 대입 연산자, 소멸자를 암시적으로 만들어 놓을 수 있다.

<br>

<h2>
- 컴파일러가 만들어낸 함수가 필요 없으면 확실히 이들의 사용을 금해 버리자.
</h2>

  -  컴파일러에서 자동으로 제공하는 기능을 허용치 않으려면, 대응되는 멤버 함수를 private로 선언한 후에 구현은 하지 않은 채로 두자. Uncopyable과 비슷한 기본 클래스를 쓰는 것도 한 방법이다.

<br>

<h2>
- 다형성을 가진 기본 클래스에서는 소멸자를 반드시 가상 소멸자로 선언하자.
</h2>

  -  다형성을 가진 기본 클래스에는 반드시 가상 소멸자를 선언해야 한다. 즉 어떤 클래스가 가상 함수를 하나라도 갖고 있으면, 이 클래스의 소멸자도 가상 소멸자여야 한다.

  - 기본 클래스로 설계되지 않았거나 다형성을 갖도록 설계되지 않은 클래스에는 가상 소멸자를 선언하지 말아야 한다.

<br>

<h2>
- 예외가 소멸자를 떠나지 못하도록 붙들어 놓자
</h2>

  -  

<br>
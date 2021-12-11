---
title: "Virtual Table"
categories:
  - C++
tags:
  - Polymorphism
---
   
<br>
<h1>
Virtual table 이란
</h1>
<br>
  
  - Virtual table은 클래스 내부에 있는 모든 가상 멤버 함수들의 주소값을 기록해둔 테이블이다. 
  
<br>

  - 클래스 당 1개씩 존재한다.

<br>

  - 개체를 생성할때 해당 클래스의 Virtual table 주소도 같이 저장된다.

<br>

  - Jump table 혹은 Lookup Table이라고도 불린다.  

<br>

<h1>
- Virtual table 작동 방식
</h1>


 - 비 가상 함수라면 다음과 같은 코드의 Speak 함수의 결과 값은 이럴 것이다. 
  
<br>

```c++
class Animal
{
  // ~~
public :
  void Speak(); // Speaking..
}

class Cat : Animal
{
  // ~~
public :
  void Speak(); // Meow !
}

void main()
{
  Animal* A = new Cat();
  A->Speak(); // Speaking..
}
```
  
<br>

- 하지만 가상 함수라면 Speak 함수의 결과 값은 다를 것이다.
  
<br>

```c++
class Animal
{
  // ~~
public :
  virual void Speak(); // Speaking..
}

class Cat : Animal
{
  // ~~
public :
  void Speak(); // Meow !
}

void main()
{
  Animal* A = new Cat();
  A->Speak(); // Meow !
}
```
  
<br>

결과 값이 달라지는 이유는 위에서 설명했듯 객체가 생성될때 해당 클래스의 가상테이블의 주소를 같이 저장하는데,

가상 함수를 호출할 경우 가상 테이블을 통해 함수를 호출한다. 

Animal 포인터를 통해 Speak 함수를 호출하여도 저장된건 Cat 클래스의 Virtual Table이고, 

Cat의 Virtual Table에 있는 Speak 함수를 호출해 Meow가 출력되게 된다. 

  
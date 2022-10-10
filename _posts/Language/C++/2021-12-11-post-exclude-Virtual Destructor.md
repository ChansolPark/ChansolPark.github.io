---
title: "Virtual Destructor"
categories:
  - C++
classes : wide
tags:
  - Destructor
  - Polymorphism
---
   
<br>
<h1>
Virtual Destructor 이란
</h1>
<br>
  
  - Virtual Destructor는 가상 함수와 특별히 다른 내용은 없는 것으로 알고 있다. 
  
<br>

  - 하지만 Virtual Destructor는 메모리 누수 관리에 있어 매우 중요하게 쓰인다. 
 
<br>

 <br>
<h1>
Virtual Destructor와 메모리 누수
</h1>
<br>


  - 다음 코드를 한번 봐보자. (Pocu Academy의 Code)
  
```c++

class Animal
{
public:
  ~Animal();

private:
  int mAge;
}

class Cat : public Animal
{
public:
  ~Cat();
private: 
  char* mName;
}

Cat::~Cat()
{
    delete mName;
}
```

  - 난 처음에 이 코드를 보고 '뭐가 문제인거지? 문제가 없는 것 아닌가 ?' 라고 생각했었다. 
  
```c++
void main()
{
  Cat* A = new Cat();
  delete A;
}
```

  - 이렇게 사용되면 문제가 없겠지만.. 만약 


```c++
void main()
{
  Animal* A = new Cat();
  delete A;
}
```

 - 이렇게 사용된다면 Cat의 소멸자가 아닌 Animal의 소멸자가 호출되며 메모리 누수가 발생한다. 

 - 이 문제점을 해결해 줄 수 있는 것이 바로 가상 소멸자이다. 
   
```c++

class Animal
{
public:
  virtual ~Animal();

private:
  int mAge;
}

class Cat : public Animal
{
public:
  ~Cat();
private: 
  char* mName;
}

Cat::~Cat()
{
    delete mName;
}

```
```c++
void main()
{
  Animal* A = new Cat();
  delete A;
}
```

- 가상 소멸자를 사용한다면 Animal 포인터의 소멸자를 호출하여도 Cat 클래스의 소멸자가 호출될 것이다. (Virtual Table Post 참고)

- 덧붙여서 모든 소멸자를 가상 소멸자로 만들것을 추천한다고 한다. 

- 하지만 그다지 내키지 않는 것은 사실이다. 
  - "가상 함수의 경우 정적 바인딩 방식에 비해 느리고 지금 내가 만들고 있는 클래스는 따로 상속될 일도 없을 듯한데 넣어야하나?" 하고 말이다. 

<br>

- 그러나 내가 작성한 클래스가 후에 다른 사람이 상속하지 않으란 보장이 없고 성능 저하도 메모리 누수가 가져오는 악영향에 비하면 양호하다는 점때문에, 

- 모든 소멸자는 가상 소멸자로 사용하기를 권고한다고 Pope 아저씨 (Pocu Academy 강사)는 말한다.
  
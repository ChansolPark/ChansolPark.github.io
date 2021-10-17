---
title: "Object"
categories:
  - CSharp
tags:
  - Object
  - Boxing, UnBoxing
---




  
<br>
<h1>
Object
</h1>
<br>
  
  - Object
    - Object는 C#에서 사용되는 값 형식, 참조 형식 등 모든 데이터 형식이 상속받는 형식이다.
    - 사용자가 지정한 형식도 Object를 상속받는다. 
    - int 형 변수에서 .Eqauls 같은 함수가 사용 가능한 이유도 Object 때문이다.
      - ex) int a = 0; a.Equals(5)


  - ArrayList
    - 매개변수를 Object로 받는 배열과 유사한 자료구조이다.
      - Object를 매개변수로 하기 때문에 모든 형식을 저장 할 수 있어 범용성이 좋다.
    - 하지만 Boxing, UnBoxing이 일어남에 따라 데이터 양이 많을 경우 성능저하의 우려가 있다. 


  <br>

```cs
int i = 123;
object o = i;
```

- Boxing
  
  - 위 코드와 같은 처리를 할 경우 Object는 참조 형식인 반면 int는 값 형식이므로 

    - 힙 메모리에 새로운 오브젝트를 생성 후 해당 오브젝트의 값에 i를 대입하여 

    - i값을 가진 오브젝트를 o에 대입하는 Boxing이 일어나게 된다.
  
    -  i가 가진 값과 o가 가진 값은 서로 다른 메모리를 사용하므로 o의 값이 변경되어도 i의 값은 변하지 않는다.
  
  <br>

 ```cs
int i = 123;
object o = i;
int j = (int)o;
```

- UnBoxing
  - int j 에 o를 대입하면 박싱되었던 o에 저장된 값을 j에 대입해줘 UnBoxing이 일어난다.
   
  - UnBoxing에는 조건이 있는데
    - Boxing 되었던 오브젝트만 UnBoxing 할 수 있다.
    - Boxing된 자료형과 UnBoxing 하여 값을 받는 변수는 자료형이 같아야 한다. 
  
  <br>
  
- Boxing, UnBoxing 비용

  - MSDN에서는 Boxing과 UnBoxing의 성능저하 우려에 대해 이렇게 적혀있다. 

    - Boxing 및 unboxing은 계산을 많이 해야 하는 프로세스입니다. 

    - 값 형식이 boxing되면 완전히 새로운 개체가 생성되어야 합니다. 

    - 이 - 작업은 단순 참조 할당보다 20배나 오래 걸립니다. 

    - unboxing 시 캐스팅 프로세스는 할당의 4배에 달하는 시간이 소요될 수 있습니다. 

  - MSDN에서는 해결책으로 다음과 같은 방안을 제시한다.

    - System.Collections.Generic.List<T>와 같은 제네릭 컬렉션을 사용하는 경우 값 형식을 boxing하지 않을 수 있습니다. 
  



  
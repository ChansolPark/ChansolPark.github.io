---
title: "Implement_Stack"
categories:
  - Implement (구현)
tags:
  - data structure
  - C++
---

직접 구현해본 Stack 클래스

```C++

using namespace std;

#include <iostream>

class StackArray {

private :

    int* stackArr;
    int length;
    int top;

public :

    StackArray(int n)
    {
        length = n;

        stackArr = new int[length];

        for (int i = 0; i < length; i++)
        {
            stackArr[i] = 0;
        }

        top = -1;
    }

    int Push(int _num)
    {

        // 오버 플로우 발생
        if (top + 1 == length)
        {
            cout << "overflow." << endl;
            return -1;
        }


        top++;

        stackArr[top] = _num;


        cout << "Pushed  : " << _num << endl;
        return 0;
    }
    int Pop()
    {
        
        // 언더 플로우 발생
        if (top == -1)
        {
            cout << "underflow." << endl;
            return -2;
        }


        int temp = stackArr[top];

        stackArr[top] = 0;
        top--;

        cout << "Poped : " << temp << endl;
        return temp;
    }

    void Print()
    {
        for (int i = 0; i < length; i++)
        {
            cout << stackArr[i] << "   ";
        }

        cout << endl;
    }
};
```


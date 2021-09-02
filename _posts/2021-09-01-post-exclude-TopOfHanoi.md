---
title: "Algorithm_TopOfHanoi"
categories:
  - Algorithm
tags:
  - recursion Algorithm
  - C++
---

- 재귀함수를 이용한 하노이의 탑 구현
```C++
void hanoi(int n, int start, int end, int other)
{

    if (n == 1)
    {
        cout << n << "을 " << start << "에서" << end << "로 이동" << endl;
        moveCnt++;
        return;
    }

    hanoi(n - 1, start, other, end);
    cout << n << "을 " << start << "에서" << end << "로 이동" << endl;
    moveCnt++;

    hanoi(n - 1, other, end, start);
    }
  ```
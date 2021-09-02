---
title: "Algorithm_Fibonachi"
categories:
  - Algorithm
tags:
  - recursion Algorithm
  - C++
---

재귀함수를 이용한 피보나치 값 계산 코드

```C++

int fibo(int n1, int n2, int leftNum)
{

	if (leftNum == 0)
	{
		return -1;
	}

	cout << n1 + n2 << endl;
	
	return fibo(n2, n1 + n2, leftNum - 1);
	}
```
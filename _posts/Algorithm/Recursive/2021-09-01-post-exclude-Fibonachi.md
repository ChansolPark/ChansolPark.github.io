---
title: "Fibonachi"
classes : wide
categories:
  - Recursive
tags:
  - C++
---
<br>
재귀함수를 이용한 피보나치 값 계산 코드

```cpp

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
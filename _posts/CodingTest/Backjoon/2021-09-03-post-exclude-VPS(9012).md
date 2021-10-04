---
title: "VPS(9012)"
categories:
  - Backjoon
tags:
  - C++
---

<h1>
9012 : 괄호
</h1>

Link : https://www.acmicpc.net/problem/9012

<br>
풀이 코드

```cpp
#include <iostream>
using namespace std;

bool solution(string str);
int main()
{
	int length;
	cin >> length;

	string* str = new string[length];

	for (int i = 0; i < length; i++)
	{
		cin >> str[i];
	}

	for (int i = 0; i < length; i++)
	{
		cout << (solution(str[i]) ? "YES" : "NO") << endl;
	}
	return 0;
}

// True = 1
bool solution(string str)
{
	// 좌측 가로의 갯수를 카운트 할 변수
	int leftCount = 0;

	for (int i = 0; i < str.size(); i++)
	{
		switch (str[i])
		{
			// 좌측 괄호 카운트 증가
		case '(':
			leftCount++;
			break;
			// 좌측 괄호 카운트 감소
		case ')':
			// 불 균형 이라면
			if (leftCount == 0)
			{
				return 0;
			}
			leftCount--;
			break;
		default:
			break;
		}
	}

	// 짝이 맞아 떨어진다면
	if (leftCount == 0)
		return 1;
	
	return 0;
}
```


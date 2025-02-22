---
title: "Find_PrimeNumber"
categories:
  - Math
classes : wide
tags:
  - C++
---
<br>

<h1>
- 소수 찾기 프로그램
</h1>

- 에라토 스테네스의 체를 이용한 소수 찾기 프로그램

- 에라토 스테네스의 체
  - '소수는 약수가 없다 = 소수의 배수는 소수가 아니다.' 라는 점을 이용한 소수를 구하는 알고리듬.
  
    - 2부터 소수를 구하고자 하는 구간의 모든 수를 나열한다.

    - 2부터 시작해 1씩 증가하며 자기 자신(N)을 제외한 N의 배수를 모두 지운다.

    - 1증가 후 지워진 수라면 PASS 한다.

    - 위의 과정을 반복하면 구하는 구간의 모든 소수가 남는다.
  <br>
  <br>

- 구현 코드
  
```cpp
#include <iostream>
#include <array>

using namespace std;

// 에라토스테네스의 체를 이용한 소수 찾기 프로그램
// 소수에 해당하는 배열내의 인덱스에 1값을 대입하는 프로그램
int main()
{
	array <int, 100> a;

	// 배열에 값 할당
	for (int i = 0; i < a.size(); i++)
	{
		// 소수는 2부터 시작
		if (i >= 2)
		{
			a[i] = 1;
		}
		else
		{
			a[i] = 0;
		}
	}
	// 2~ 99번까지 값이 1로 초기화 되어있는 상태.

	for (int i = 2; i < a.size(); i++)
	{
		if (a[i] == 1)
		{
			// n의 x 2 부터 0값을 대입하기 위해 i * 2
			// j에 i의 배수의 값을 넣기위해 증감식에 += i를 해줌.
			for (int j = i * 2 ; j < a.size(); j += i)
				a[j] = 0;

			cout << i << " " << endl;
		}
	}
	// 배열에는 소수에 해당하는 인덱스만 1값이 들어있다.
	
	

	return 0;
}
  ```
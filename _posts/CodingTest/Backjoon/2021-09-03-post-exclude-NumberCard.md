---
title: "NumberCard 2"
categories:
  - Backjoon
classes : wide
tags:
  - BinarySearch algorithm
  - C++
---

<h1>
Number Card 2
</h1>

Link : https://www.acmicpc.net/problem/10816

<br>
풀이 코드

```cpp

#include <iostream>
#include <algorithm>
using namespace std;

int main()
{

	ios_base::sync_with_stdio(false);
	cin.tie(NULL);
	// 숫자카드의 정보받기

	int numsLength;
	cin >> numsLength;

	int* nums = new int[numsLength];

	for (int i = 0; i < numsLength; i++)
		cin >> nums[i];

	// 정렬 
	sort(nums, nums + numsLength);

	// 찾을 값 받기

	int findLength;
	cin >> findLength;

	int* findNums = new int[findLength];

	for (int i = 0; i < findLength; i++)
		cin >> findNums[i];


	// 반복문 돌면서 찾고자하는 값이 몇개인지 찾아서 출력
	for (int i = 0; i < findLength; i++)
	{
		// upper_bound는 찾는 값보다 큰 값의 첫번째 인덱스를 반환
		// lower_bound는 찾는 값이 중복이라면 첫번째 인덱스를 반환
		// upper - lower은 중복값의 갯수를 말한다.
		cout << upper_bound(nums, nums + numsLength, findNums[i]) - lower_bound(nums, nums + numsLength, findNums[i]) << " ";
	}
	return 0;
}

```


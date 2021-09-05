---
title: "BinarySearch (Spined Array)"
categories:
  - Implement (구현)
tags:
  - Search Algorithm
  - C++
---
<br>
직접 구현해본 회전된 배열에서의 이진 탐색

```cpp
#include <iostream>

using namespace std;

int BinarySearch(int nums[], int findNum, int l, int r);

int main()

{

	int ababArray[10] = { 4,5,6,7,8,1,2,3,9,10 };
	// 선조건 : int형의 자료만 입력 받음
	BinarySearch(ababArray, 9, 0, 9);
}

/*
*	회전된 배열에서의 이진 탐색의 관건은 

<br>
*	일반 이진탐색

*	가운대 값 기준 큰지 작은지 계산해서 방향을 정함

<br>
*	회전 배열의 경우 

*  center를 기준으로 정렬되어있는 방향을 찾고 (왼쪽 아니면 오른쪽 한곳은 무조건 정렬되어있다.)
*  정렬되어 있는 방향에 찾는 값이 있다면 일반 이진 탐색처럼 작동하고
*  정렬되어 있는 방향에 찾는 값이 없다면 반대 방향을 인자 값으로 넘겨줌으로써
*  반복한다.
*  결국 함수를 반복하면서 양 뱡향중 정렬되어 있는 곳만 검색을 해나간다.
*  둘중 한곳은 꼭 정렬이 되어있기 떄문에.
*  그렇게 값에 가까워지며 값을 찾게 된다.
* 
*  요약 : 
*  center값을 구하면 방향이 두개가 나오는데
*  둘중 정렬된 방향을 토대로 정렬된 방향에 값이 있는지 검사후 없으면 
*  정렬되지 않은 방향을 반으로 나눠
*  나뉜 두 방향중 정렬된 방향에 값이 있는지
*  없으면 반복하여 점점 값에 가까워지는 방식이다.
*/


int BinarySearch(int nums[], int findNum, int l, int r)

{

	if (l > r)
	{
		cout << "찾는 값이 배열내에 없음.";
		return 0;
	}

	int center = (l + r) / 2;


	// 탐색이 정상적이라면
	if (nums[center] == findNum)
	{
		cout << "탐색 성공." << endl;
		cout << "인덱스 위치 : " << center << endl;
		return 0;
	}

	// 회전 기준점이 센터의 오른쪽에 있음
	if (nums[l] < nums[center])
	{

		// 센터의 왼쪽편에 값이 있는지 (정렬되어있으니 그냥 검색하면 됨)
		if (findNum >= nums[l] && findNum <= nums[center])
		{
			return BinarySearch(nums, findNum, l, center - 1);
		}

		// 없다. 값이 회전축이 있는 오른쪽구역에 있는 상황
		else
		{
			return BinarySearch(nums, findNum, center + 1, r);
		}
	}

	// 회전 기준점이 센터의 왼쪽에 있음
	else
	{

		// 센터의 오른쪽편에 값이 있는지 (정렬되어있으니 그냥 검색하면 됨)
		if (findNum >= nums[center] && findNum <= nums[r])
		{
			return BinarySearch(nums, findNum, center + 1, r);
		}
		
		// 없다. 값이 회전축이 있는 왼쪽구역에 있는 상황
		else
		{
			return BinarySearch(nums, findNum, l, center - 1);
		}
	}
}
```C++
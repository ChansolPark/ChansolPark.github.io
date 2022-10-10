---
title: "Dynamic_Programming"
classes : wide
categories:
  - Dynamic
tags:
  - Dynamic_Programming
---

<br>
<h1>
- 동적 계획법 (Dynamic_Programming)
</h1>
<br>

- 동적 계획법

  - 복잡한 문제를 하위 문제로 쪼개서 재귀적으로 푸는 기법 
 
 <br>

 - 메모이제이션
  
   - 계산 결과를 캐시에 저장해 중복되는 계산을 개선하기 위한 기법<br> 
  
   - 좋은 예로 피보나치 수열에서의 메모이제이션 기법 저용이 있음.
  
   - Top Down 동적 계획법

     - 복잡한 문제 (루트)에서 시작해 하위 문제를 풀어나가는 방식. 
  <br><br><br>

 - 타블레이션
   - Bottom-Up 동적 계획법

     - 가장 하위 문제 (리프) 부터 시작해 복잡한 문제까지 풀어나가는 기법 

     - Top Down 방식보다 보통 더 빠름

       - 재귀 함수 호출을 피할 수 있음 
  

- 동적 계획법을 이용한 배낭 문제 풀이
Link : https://www.acmicpc.net/problem/12865


```cpp
using namespace std;
#include <iostream>

struct Object
{
	int size;
	int price;
};

int Answer(Object* objects, int objectLength, int bagSize);

int main()
{
	Object recoder;
	recoder.size = 5;
	recoder.price = 5;

	Object book;
	book.size = 4;
	book.price = 2;

	Object deer;
	deer.size = 11;
	deer.price = 6;

	cout << Answer(new Object[]{ recoder, book, deer }, 3, 15);

	return 0;
}

int Answer(Object* objects, int objectLength, int bagSize)
{
	int answer = 0;
	int** bag_Board = new int* [objectLength];

	int past_Num = 0;
	int now_Num = 0;

	// 동적 할당
	for (int i = 0; i < objectLength; i++)
	{
		bag_Board[i] = new int[bagSize];

		for (int j = 0; j < bagSize; j++)
			bag_Board[i][j] = 0;
	}

	
	for (int i = 0; i < objectLength; i++)
	{
		for (int j = 0; j < bagSize; j++)
		{
			// 첫번쨰 오브젝트가 아니라면
			if (i > 0)
			{
				// j가 size이상이면
				if (objects[i].size - 1 <= j)
				{
					// 과거의 최상의 값을 가져옴
					past_Num = bag_Board[i - 1][j];
					// j에 현재 오브젝트의 size 값을 뺴고도 자리가 남는지 여부 검사 후 대입
					now_Num = j - objects[i].size >= 0 ? bag_Board[i - 1][j - objects[i].size] + objects[i].price : objects[i].price;

					// 둘중 큰 값 대입
					bag_Board[i][j] = past_Num >= now_Num ? past_Num : now_Num;

				}
				// 아닐경우 j에 해당하는 전 인덱스 i -1의 값을 대입
				else
				{
					bag_Board[i][j] = bag_Board[i - 1][j];
				}

			}
			//첫번째 오브젝트라면
			else
			{
				// j는 0부터 시작하므로 size -1한 값의 이상이 될때 값 대입
				if (objects[i].size - 1 <= j)
					bag_Board[i][j] = objects[i].price;
			}


		}
	}
  
  // 구한 값 대입
	answer = bag_Board[objectLength - 1][bagSize - 1];

	for (int i = 0; i < objectLength; i++)
	{
		delete[] bag_Board[i];
	}

	return answer;
}
```


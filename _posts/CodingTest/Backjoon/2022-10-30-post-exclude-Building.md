---
title: "고층건물"
classes: wide
categories:
  - Backjoon
tags:
  - Bruteforce
  - C++
  
---

- 고층건물 : https://www.acmicpc.net/problem/1027

<br>

핵심 풀이 아이디어를 찾는데 좀 오래 걸렸던 문제였다. 고민하던 중, 문제의 지문에 '선분'이라는 단어가 사용된 점에 착안 해 직선의 기울기를 이용해 문제를 풀었다.

<br>
풀이 코드 :

``` cpp

#include <iostream>
#include <vector>

using namespace std;

int main()
{
	vector<int> Buildings;

	int BuildingCount;
	cin >> BuildingCount;

	for (int i = 0; i < BuildingCount; ++i)
	{
		int Height;
		cin >> Height;
		Buildings.push_back(Height);
	}

	int MaxResult = 0;
	for (int i = 0; i < Buildings.size(); ++i)
	{
		int Result = 0;

		// Left
		{
			bool bFirst = true;
			float LastViewAngle = 0;
			for (int Left = i - 1; Left >= 0; --Left)
			{
				const int CurrentBuildingHeight = Buildings[i];
				const int TryLookBuildingHeight = Buildings[Left];

				float ViewAngle = static_cast<float>(TryLookBuildingHeight - CurrentBuildingHeight) / abs(Left - i);

				// 첫 빌딩이거나 전 빌딩보다 기울기가 더 높다면 (시야에 식별 된다면)
				if (bFirst == true || ViewAngle > LastViewAngle)
				{
					bFirst = false;
					LastViewAngle = ViewAngle;
					++Result;
				}
			}
		}
		
		// Right
		{
			bool bFirst = true;
			float LastViewAngle = 0;
			for (int Right = i + 1; Right < Buildings.size(); ++Right)
			{
				const int CurrentBuildingHeight = Buildings[i];
				const int TryLookBuildingHeight = Buildings[Right];

				float ViewAngle = static_cast<float>(TryLookBuildingHeight - CurrentBuildingHeight) / abs(Right - i);
				// 첫 빌딩이거나 전 빌딩보다 기울기가 더 높다면 (시야에 식별 된다면)
				if (bFirst == true || ViewAngle > LastViewAngle)
				{
					bFirst = false;
					LastViewAngle = ViewAngle;
					++Result;
				}
			}
		}
		
		if (Result > MaxResult)
		{
			MaxResult = Result;
		}
	}

	cout << MaxResult;
}

```
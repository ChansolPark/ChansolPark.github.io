---
title: "방의 갯수"
categories:
  - Programmers
classes : wide
tags:
  - C++
---

  
<br>
<h2>
- 방의 갯수 : https://school.programmers.co.kr/learn/courses/30/lessons/49190
</h2>
<br>

한번 호기심에 [Level5] 문제에 도전해보고 싶어 [Level5] 문제 중 가장 합격률이 높은 문제에 도전해보았다. 해당 문제에서의 핵심 풀이 아이디어는 2개였는데, 그 중 내가 찾아낸 아이디어는 "중복되지 않은 이동 경로로 특정 좌표에 재 방문할경우 하나의 방이 생성된다" 이다. 해당 아이디어를 찾고 "풀었다 !" 라고 생각했지만, 1 x 1 사각형 안에서 ⌧모양처럼 X로 선을 그릴 경우 한번의 이동으로 두개의 방이 생성되는 경우가 있어 해당 예외에 대한 해결책이 필요했다. 영겹의 고민끝에.. 난 결국 해당 해결책을 찾아내지 못해 답을 보았는데, "모든 선의 입력을 두배로 늘려 1 x 1 사각형에서의 문제를 2 x 2 사각형으로 만들어 해결한다" 라는 아이디어를 보고 정말 감탄했던 기억이 난다. 

해당 문제에서의 "문제의 입력을 조작해 해결한다"라는 아이디어는 평소 입력 값을 상수처럼 대하던 나에게 틀을 깨준, 너무 재밌는 문제였다.


<br>
풀이 코드

```cpp


#include <string>
#include <vector>
#include <unordered_map>

using namespace std;

using namespace std;

struct FPoint
{
	int X;
	int Y;

	FPoint() :
		X(0),
		Y(0)
	{}

	bool operator!=(const FPoint& InPoint) const
	{
		return !operator==(InPoint);
	}
	bool operator==(const FPoint& InPoint) const
	{
		return X == InPoint.X && Y == InPoint.Y;
	}

	struct HashFunction
	{
		size_t operator()(const FPoint& point) const
		{
			size_t xHash = std::hash<int>()(point.X);
			size_t yHash = std::hash<int>()(point.Y) << 1;
			return xHash ^ yHash;
		}
	};
};

FPoint GetNextPosition(int InArrow, const FPoint& InPosition);

int solution(vector<int> arrows)
{
	int answer = 0;

	unordered_multimap<FPoint, FPoint, FPoint::HashFunction> VisitedPoint_Map;

	FPoint LastPosition;
	FPoint CurrentPosition;

	for (const int arrow : arrows)
	{
		// 두번씩 반복되도록 (대부분 한번 선을 그릴때 면이 하나씩 늘어나지만,
		// 1 x 1 사각형 안에서 ⌧모양처럼 X로 선을 그릴 경우, 한번 선을 그릴때 면이 2개가 늘어나는 예외가 있어 모든 선의 이동 길이를 두배로 늘려 해당 예외를 제거한다.
		for(int i = 0; i < 2; ++i)
		{
			CurrentPosition = GetNextPosition(arrow, CurrentPosition);

			//  방문한적이 있는 좌표에 방문했다면
			if (VisitedPoint_Map.find(CurrentPosition) != VisitedPoint_Map.end())
			{
				// 중복된 선을 그렸는지 확인
				auto FindRange = VisitedPoint_Map.equal_range(CurrentPosition);
				bool bOverlapLine = false;
				for (auto itr = FindRange.first; itr != FindRange.second; ++itr)
				{
					// 중복된 선을 그렸다면
					if (itr->second == LastPosition)
					{
						// 중복 여부 True
						bOverlapLine = true;
						break;
					}
				}

				// 중복 검사를 통과했다면
				if (bOverlapLine == false)
				{
					// 면의 갯수를 증가
					++answer;

					// 지금 그린 선을 추가
					VisitedPoint_Map.emplace(CurrentPosition, LastPosition);
					VisitedPoint_Map.emplace(LastPosition, CurrentPosition);
				}
			}
			else
			{
				VisitedPoint_Map.emplace(CurrentPosition, LastPosition);
				VisitedPoint_Map.emplace(LastPosition, CurrentPosition);
			}

			LastPosition = CurrentPosition;
		}
	}

	return answer;
}

FPoint GetNextPosition(int InArrow, const FPoint& InPosition)
{
	FPoint NextPosition = InPosition;

	// X 좌표 이동
	switch (InArrow)
	{
		case 1:
		case 2:
		case 3:
		{
			++NextPosition.X;
		}
		break;

		case 5:
		case 6:
		case 7:
		{
			--NextPosition.X;
		}
		break;
	}

	// Y 좌표 이동
	switch (InArrow)
	{
		case 0:
		case 1:
		case 7:
		{
			--NextPosition.Y;
		}
		break;

		case 3:
		case 4:
		case 5:
		{
			++NextPosition.Y;
		} 
		break;
	}
	return NextPosition;
}

```


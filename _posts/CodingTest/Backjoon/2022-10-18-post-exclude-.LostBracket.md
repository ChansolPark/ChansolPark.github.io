---
title: "일어버린 괄호"
classes: wide
categories:
  - Backjoon
tags:
  - Greedy
  - C++
  
---

- 일어버린 괄호 : https://www.acmicpc.net/problem/1541

<br>

주어진 식에 괄호를 적절히 배치 해 최소의 값을 만들어 내는 문제이다. 어떻게 풀까 열심히 고민한 결과, '-' 부호 뒤부터 괄호를 열어, '-'부호를 만나거나, 식이 끝나는 곳에 괄호를 닫아주면 되는 규칙을 찾아내 해결했다. 
<br>

위에 서술한 규칙대로 괄호를 배치 ex) 
1. 55-50+40 -> 55-(50+40) = -35
2. 55-50+40-50+40 -> 55-(50+40)-(50+40) = -125

<br>
풀이 코드 :

``` cpp

#include <iostream> 
#include <vector>
#include <algorithm>

using namespace std;

struct FCityLinkInfo
{
	uint32_t City_Index;
	uint32_t City_OilPrice;

	FCityLinkInfo() :
		City_Index(0),
		City_OilPrice(0)
	{}

	bool operator < (const FCityLinkInfo& InOther) const
	{
		return City_OilPrice < InOther.City_OilPrice;
	}
};

struct FCityDistanceInfo
{
	uint64_t Distance_ForNextCity;

	FCityDistanceInfo() :
		Distance_ForNextCity(0)
	{}
};

int main()
{
	ios::sync_with_stdio(false);
	cin.tie(nullptr);
	cout.tie(nullptr);

	uint64_t Result = 0;

	uint32_t Citys_Num;
	cin >> Citys_Num;

	// 각 도시의 거리 정보를 저장
	vector<FCityDistanceInfo> City_Distanceinfos_Vector(Citys_Num, FCityDistanceInfo());
	for (uint32_t i = 0; i < Citys_Num - 1; ++i)
	{
		cin >> City_Distanceinfos_Vector[i].Distance_ForNextCity;
	}

	// 해당 도시의 인덱스 번호, 주유소 비용 정보를 저장
	vector<FCityLinkInfo> CityLinks_Vector(Citys_Num, FCityLinkInfo());
	for (uint32_t i = 0; i < Citys_Num; ++i)
	{
		CityLinks_Vector[i].City_Index = i;
		cin >> CityLinks_Vector[i].City_OilPrice;
	}

	// 주유소 비용 순으로 정렬
	sort(CityLinks_Vector.begin(), CityLinks_Vector.end());

	// 필요 비용 계산
	{
		// 마지막 도시는 기름 구매가 필요없기 때문에 마지막 도시를 초기값으로 설정
		uint32_t CheckingIndex = Citys_Num;

		// 주유소 비용이 낮은 순으로, 해당 최소 주유비용 도시부터 남은 거리만큼 기름을 구매
		for (const FCityLinkInfo& CityLink : CityLinks_Vector)
		{
			// 이미 구매 완료된 영역이라면
			if (CityLink.City_Index >= CheckingIndex) { continue; }

			// 현재 도시부터 아직 구매하지 않은 거리에 대한 기름을 구매
			for (uint32_t i = CityLink.City_Index; i < CheckingIndex; ++i)
			{
				// 현재 도시의 기름 가격 * 앞으로 가야할 거리
				Result += CityLink.City_OilPrice * City_Distanceinfos_Vector[i].Distance_ForNextCity;
			}

			// 구매 완료 도시 인덱스 갱신
			CheckingIndex = CityLink.City_Index;

			// 필요한 기름을 모두 구매했다면 반복문 종료
			if (CheckingIndex == 0)
			{
				break;
			}
		}
	}

	// 결과 값 출력
	cout << Result;
}

```
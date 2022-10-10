---
title: "Greedy_Algorithm"
classes : wide
categories:
  - Greedy
tags:
  - Greedy
---

<br>
<h1>
- 그리디 (탐욕) 알고리즘 (Greedy_Algorithm)
</h1>
<br>

- 그리디 알고리즘

  - 미래의 결과는 상관없이 현재 마주한 선택지의 최적의 값만을 선택하는 탐욕 알고리즘

    - ex) 공복상태에서 매우 소량의 치즈 조각이 있는 상태라면 치즈로 쥐 트랩을 설치해 쥐를 잡는게 일반적지만,
      - Greedy 알고리즘이라면 일단 치즈를 먹는다.
      
  
  <br>

  - 근사 알고리듬

    - 항상 최적의 답을 내진 않으나, 그에 근사한 답을 얻을 수 있음.
 
 <br>

 - 그리디 알고리즘을 이용한 배낭 문제 풀이 (물건들 중 가장 비싼것부터 선택)
Link : https://www.acmicpc.net/problem/12865


```cpp
using namespace std;
#include <iostream>
#include <vector>
#include <algorithm>

struct Object
{
	int size;
	int price;
};

bool objectCompare(Object a, Object b);

int Answer(vector<Object> objects, int bagSize);

int main()
{
	vector<Object> items(3);
	items[0].size = 5;
	items[0].price = 5;

	items[1].size = 4;
	items[1].price = 2;

	items[2].size = 11;
	items[2].price = 6;

	cout << Answer(items, 15);

	return 0;
}

int Answer(vector<Object> objects, int bagSize)
{
	int answer = 0;

	// 카운터
	int priceCount = 0;
	int sizeCount = 0;

	// 가격을 기준으로 내림차순 정렬
	sort(objects.begin(), objects.end(), objectCompare);

	// 0번부터 순차적으로 가방에 집어넣음 (비싼 순서대로)
	for (int i = 0; i < objects.size(); i++)
	{
		// 사이즈 카운터 + 집어넣을 물건의 사이즈 가 가방 사이즈보다 크지 않다면
		if (sizeCount + objects[i].size <= bagSize)
		{
			sizeCount += objects[i].size;
			priceCount += objects[i].price;
		}
		// 가방이 가득 참
		else
			break;
	}

	answer = priceCount;

	return answer;
}

// 정렬의 기준점이 될 값을 정하는 함수
bool objectCompare(Object a, Object b)
{
	return a.price > b.price;
}
```


---
title: "단체사진 찍기"
categories:
  - Programmers
classes : wide
tags:
  - C++
---

  
<br>
<h2>
- 단체사진 찍기 : https://school.programmers.co.kr/learn/courses/30/lessons/1835
</h2>
<br>

백 트래킹 기법을 이용해 문제 자체는 큰 어려움 없이 풀었던 것 같다. 다만 분명 틀린 부분을 못 찾겠는데, 자꾸 틀림 판정이 나와서 2시간 정도 막혔었다.. 다른 분들의 후기를 들어보니, 여러 테스트케이스에 대해 Solution함수가 여러번 호출되는데, 각 Solution 함수 호출 시 내가 선언한 전역변수의 초기화가 정상적으로 이뤄지지 않아 틀렸던 것이였다. 그래서 해당 전역 변수 (Rule_Vector) 를 로컬 변수로 변경하니 문제가 해결되었다.

<br>
풀이 코드

```cpp

#include <iostream>
#include <string>
#include <unordered_map>
#include <vector>

using namespace std;

enum
{
	CHARACTER_LENGTH = 8
};

struct FRule
{
	char Character_A;
	char Character_B;
	int Distance;
	bool bEqual;
	bool bLess;
	bool bGreater;
	FRule() :
		Character_A(0),
		Character_B(0),
		Distance(0),
		bEqual(false),
		bLess(false),
		bGreater(false)
	{}
};

vector<char>Characters = { 'A', 'C', 'F', 'J', 'M', 'N', 'R', 'T' };

int BackTracking_Search(const vector<FRule>& InRule, const unordered_map<char, int>& InArrangement);

// 전역 변수를 정의할 경우 함수 내에 초기화 코드를 꼭 작성해주세요.
int solution(int n, vector<string> data)
{
	int answer = 0;

	vector<FRule> Rule_Vector;
	Rule_Vector.reserve(n);
	for (string temp : data)
	{
		FRule Rule;
		Rule.Character_A = temp[0];
		Rule.Character_B = temp[2];

		switch (temp[3])
		{
		case '=':
			Rule.bEqual = true;
			break;
		case '<':
			Rule.bLess = true;
			break;
		case '>':
			Rule.bGreater = true;
			break;
		}

		Rule.Distance = atoi(&temp[4]);
		Rule_Vector.push_back(Rule);
	}

	const unordered_map<char, int> Arrangement;
	answer = BackTracking_Search(Rule_Vector, Arrangement);

	return answer;
}

int BackTracking_Search(const vector<FRule>& InRule, const unordered_map<char, int>& InArrangement)
{
	// 조건 검사
	for (const FRule& Rule : InRule)
	{
		// 아직 조건 검사 대상 캐릭터가 배치되지 않았다면 Skip
		if (InArrangement.find(Rule.Character_A) == InArrangement.end() || InArrangement.find(Rule.Character_B) == InArrangement.end()) { continue; }

		int Distance = abs(InArrangement.at(Rule.Character_A) - InArrangement.at(Rule.Character_B)) - 1;

		if (Rule.bEqual == true)
		{
			if (Rule.Distance != Distance)
			{
				return 0;
			}
		}
		else if (Rule.bLess == true)
		{
			if (Distance >= Rule.Distance)
			{
				return 0;
			}
		}
		else if (Rule.bGreater == true)
		{
			if (Distance <= Rule.Distance)
			{
				return 0;
			}
		}
	}
	
	if (InArrangement.size() == CHARACTER_LENGTH)
	{
		return 1;
	}

	int Result = 0;

	for (char Character : Characters)
	{
		// 이미 등록된 캐릭터라면 Skip
		if (InArrangement.find(Character) != InArrangement.end()) { continue; }

		unordered_map<char, int> Arrangement = InArrangement;
		Arrangement.emplace(Character, Arrangement.size());
		Result += BackTracking_Search(InRule, Arrangement);
	}

	return Result;
}

```


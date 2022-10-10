---
title: "N-Queen (9663)"
classes : wide
categories:
  - Backjoon
tags:
  - BackTracing
  - C++
---

백 트래킹의 기초 문제인 N과 M을 푼 후, 자신만만하게 시작했는데.. 오후 5시 부터 새벽 2시까지 못 풀었다.. 분명 내가 생각한 로직이 맞는 것 같은데.. 그래서 구글링을 해보니 해당 좌표의 대각선에 Queen이 있는지를 O(1)에 판단 할 수 있는 방법이 있는데, 난 O(N)이 걸리는 방법을 사용해 시간초과가 계속 났던 것이였다. 정말 힘든 문제였다..

``` cpp

#include <iostream>
#include <vector>

using namespace std;

struct FPosition
{
	int Column;
	int Row;
};

int Success_Counter = 0;

void Search(const vector<FPosition>& InQueensArea, const int InRow, const int InSearch_Depth);
bool IsIn_QueensArea(const vector<FPosition>& InQueensArea, const int InRow, const int InColumn);

int N;

int main()
{
	cin >> N;

	const vector<FPosition> QueensArea;

	Search(QueensArea, 0, 0);

	cout << Success_Counter;
}

void Search(const vector<FPosition>& InQueensArea, const int InRow, const int InSearch_Depth)
{
	// 지정한 목표에 도달했다면
	if (InSearch_Depth == N)
	{
		++Success_Counter;
		return;
	}

	for (int Column = 1; Column <= N; ++Column)
	{
		// 다른 퀸의 영역이 아니라면 퀸 착점
		if (IsIn_QueensArea(InQueensArea, InRow + 1, Column) == false)
		{
			// 퀸 배치 추가
			{
				vector<FPosition> QueensArea = InQueensArea;
				FPosition Position;
				Position.Row = InRow + 1;
				Position.Column = Column;
				QueensArea.push_back(Position);

				Search(QueensArea, InRow + 1, InSearch_Depth + 1);
			}
		}
	}
}

bool IsIn_QueensArea(const vector<FPosition>& InQueensArea, const int InRow, const int InColumn)
{
	// 게임보드를 벗어났다면 
	if (InRow < 1 || InRow > N || InColumn < 1 || InColumn > N) { return true; }

	// 다른 퀸의 영역이라면

	for (int i = 0; i < InQueensArea.size(); ++i)
	{
		// 같은 행에 위치해있다면
		if (InQueensArea[i].Column == InColumn) { return true; }

		// 좌상단 -> 우하단 대각선 확인
		if (InColumn - InRow == InQueensArea[i].Column - InQueensArea[i].Row) { return true; }


		// 좌하단 -> 우상단 대각선 확인
		if (InColumn + InRow == InQueensArea[i].Column + InQueensArea[i].Row) { return true; }
	}
	
	return false;
}
```
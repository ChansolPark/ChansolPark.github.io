---
title: "구슬탐색2"
classes: wide
categories:
  - Backjoon
tags:
  - BFS
  - C++
  
---

- 구슬탐색 : https://www.acmicpc.net/problem/13460

<br>
BFS 로직 구상자체는 어렵지 않았으나.. 구현 양이 많아 힘든 문제였다. 그래도 대학생시절에 포기했던 문제를 해결하니 성취감이 이루 말 할 수 없다 !!

<br>
풀이 코드 :

``` cpp

#include <iostream> 
#include <queue>

using namespace std;

enum
{
	GOALIN = 0,
	MAX_BOARDSIZE = 10,
	OVERDEPTH = 10
};

struct FPosition
{
	uint8_t X;
	uint8_t Y;

	FPosition() :
		X(0),
		Y(0)
	{}

	FPosition(const uint8_t InX, const uint8_t InY) :
		X(InX),
		Y(InY)
	{}

	void operator=(const int InValue)
	{
		X = InValue;
		Y = InValue;
	}
	bool operator==(const FPosition& Other) const
	{
		return X == Other.X && Y == Other.Y;
	}
	bool operator==(const int Value) const
	{
		return X == Value && Y == Value;
	}
	bool operator!=(const FPosition& Other) const
	{
		return !operator==(Other);
	}
	bool operator!=(const int Value) const
	{
		return !operator==(Value);
	}
};

enum class EDirection
{
	NONE = 0,
	UP,
	DOWN,
	LEFT,
	RIGHT
};

struct FSearchInfo
{
	FPosition RedBall;
	FPosition BlueBall;
	uint8_t Depth;
};

FPosition GetNextPosition_ByDirection(const EDirection& InDirection, const FPosition& InPosition);

void RotateBoard(const EDirection& InDirection, const FSearchInfo& InSearchInfo);

void RollingBalls(const EDirection& InDirection, FPosition& InRedBall, FPosition& InBlueBall, const uint8_t InDepth);

void Fail();

void Success(const uint8_t InDepth);

bool GameBoard[MAX_BOARDSIZE][MAX_BOARDSIZE];

queue<FSearchInfo> SearchList;

FPosition Goal;

int main()
{
	ios::sync_with_stdio(false);
	cin.tie(nullptr);

	FPosition RedBall;
	FPosition BlueBall;

	// 문제 입력
	{
		int Row_Length;
		int Column_Length;
		cin >> Row_Length;
		cin >> Column_Length;

		for (int Row = 0; Row < Row_Length; ++Row)
		{
			for (int Column = 0; Column < Column_Length; ++Column)
			{
				char Char;
				cin >> Char;

				if (Char == '#')
				{
					GameBoard[Row][Column] = false;
				}
				else
				{
					GameBoard[Row][Column] = true;

					if (Char == 'O')
					{
						Goal.X = Column;
						Goal.Y = Row;
					}
					else if (Char == 'R')
					{
						RedBall.X = Column;
						RedBall.Y = Row;
					}
					else if (Char == 'B')
					{
						BlueBall.X = Column;
						BlueBall.Y = Row;
					}
				}
			}
		}
	}

	// 검색
	{
		SearchList.push(FSearchInfo{ RedBall, BlueBall, uint8_t(1) });

		while (SearchList.empty() == false)
		{
			const FSearchInfo SearchInfo = SearchList.front();
			SearchList.pop();

			// 시도 횟수 초과일 경우
			if (SearchInfo.Depth > OVERDEPTH)
			{
				Fail();
			}

			// 탐색
			RotateBoard(EDirection::UP, SearchInfo);
			RotateBoard(EDirection::DOWN, SearchInfo);
			RotateBoard(EDirection::LEFT, SearchInfo);
			RotateBoard(EDirection::RIGHT, SearchInfo);
		}
	}
	
	// 모든 경우를 다 탐색했으나 답이 없을때
	Fail();
}

// 보드를 기울임
void RotateBoard(const EDirection& InDirection, const FSearchInfo& InSearchInfo)
{
	/* 해당 최적화가 없어도 0ms가 나와서 제외
	{
		 // 왔던 방향으로 다시 돌아가는 경우는 무시 (탐색이 필요하지 않음)
		 if (InSearchInfo.Direction == ReverseDirection(InDirection)) { return; }
	}*/

	// 변동사항을 저장할 변수 선언
	FPosition RedBall = InSearchInfo.RedBall;
	FPosition BlueBall = InSearchInfo.BlueBall;

	// 기울어진 방향으로 구슬을 굴림
	RollingBalls(InDirection, RedBall, BlueBall, InSearchInfo.Depth);

	// 두 구슬에 변동이 없다면 (해당 방향으로 움직임 불가능)
	if (RedBall == InSearchInfo.RedBall && BlueBall == InSearchInfo.BlueBall)
	{
		return;
	}
	// 골인 한 구슬이 있다면
	else if (RedBall == GOALIN || BlueBall == GOALIN)
	{
		// 빨간 공만 골인에 성공했다면
		if (RedBall == GOALIN && BlueBall != GOALIN)
		{
			Success(InSearchInfo.Depth);
			return;
		}
	}
	else
	{
		// 이동된 위치에서 탐색
		SearchList.push(FSearchInfo{RedBall, BlueBall, uint8_t(InSearchInfo.Depth + 1) });
	}
}

// 기울어진 방향으로 공을 굴림
void RollingBalls(const EDirection& InDirection, FPosition& InRedBall, FPosition& InBlueBall, const uint8_t InDepth)
{
	bool bRedBall_Moved = true;
	bool bBlueBall_Moved = true;

	// 두 공 모두 움직임이 멈출때까지 반복
	while (bRedBall_Moved == true || bBlueBall_Moved == true)
	{
		// 공 움직임 여부 초기화
		bRedBall_Moved = false;
		bBlueBall_Moved = false;

		// RedBall
		{
			const FPosition& NextPosition = GetNextPosition_ByDirection(InDirection, InRedBall);

			// 골인하지 않았고, 이동이 가능하다면 (게임보드와 충돌하진 않는지, 다른 공의 위치는 아닌지)
			if (InRedBall != GOALIN && GameBoard[NextPosition.Y][NextPosition.X] == true && NextPosition != InBlueBall)
			{
				bRedBall_Moved = true;
				InRedBall = NextPosition;

				if (InRedBall == Goal)
				{
					// 구멍에 빠졌으니 게임 보드에서 제외
					InRedBall = GOALIN;
				}
			}
			else
			{
				bRedBall_Moved = false;
			}
		}

		// BlueBall
		{
			const FPosition& NextPosition = GetNextPosition_ByDirection(InDirection, InBlueBall);

			// 골인하지 않았고, 이동이 가능하다면 (게임보드와 충돌하진 않는지, 다른 공의 위치는 아닌지)
			if (InBlueBall != GOALIN && GameBoard[NextPosition.Y][NextPosition.X] == true && NextPosition != InRedBall)
			{
				bBlueBall_Moved = true;
				InBlueBall = NextPosition;

				if (InBlueBall == Goal)
				{
					// 구멍에 빠졌으니 게임 보드에서 제외
					InBlueBall = GOALIN;
				}
			}
			else
			{
				bBlueBall_Moved = false;
			}
		}
	}
}

// 이동 후의 위치를 구함
FPosition GetNextPosition_ByDirection(const EDirection& InDirection, const FPosition& InPosition)
{
	switch (InDirection)
	{
	case EDirection::UP:
	{
		return  FPosition(InPosition.X, InPosition.Y - 1);
	}
	break;
	case EDirection::DOWN:
	{
		return  FPosition(InPosition.X, InPosition.Y + 1);
	}
	break;
	case EDirection::LEFT:
	{
		return  FPosition(InPosition.X - 1, InPosition.Y);
	}
	break;
	case EDirection::RIGHT:
	{
		return  FPosition(InPosition.X + 1, InPosition.Y);
	}
	break;
	}

	return InPosition;
}

// 실패
void Fail()
{
	cout << -1;
	exit(0);
}

// 성공
void Success(const uint8_t InDepth)
{
	cout << (int)InDepth;
	exit(0);
}

```
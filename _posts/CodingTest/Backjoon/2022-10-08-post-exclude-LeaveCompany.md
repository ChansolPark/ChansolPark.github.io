---
title: "Leave Company (14501)"
categories:
  - Backjoon
classes : wide
tags:
  - Dynamic Programing
  - C++
---

평소 DP에 대해 이론만 알고 사용해보진 않았었는데, DP의 개념을 잡기에 굉장히 좋은 문제 였던 것 같다. 날짜를 역순으로 돌며 각 날짜의 최적의 값을 기록해 둔 후, 전 날짜에서 다음 날짜의 최적의 값을 구할 때 바로 가져올 수 있도록 하였다. 

``` cpp

#include <iostream> 
#include <vector>

using namespace std;

struct FMeeting
{
	int SpendTime;
	int Point;
};

enum EErrorType
{
	OVER_TIME = -1,
	NOT_VALID = -2,
};

int Find_OptimalCase(const vector<FMeeting>& InMeetings, vector<int>& OutMemory_OptimalPoints, const int InDay, const int InLeaveDay);

int main()
{
	ios_base::sync_with_stdio(false);
	cin.tie(0);

	int N;
	cin >> N;

	int LeaveDay = N + 1;

	vector<int> Memory_Optimal_Points(N + 1, EErrorType::NOT_VALID);

	vector<FMeeting> Meetings;
	Meetings.reserve(N + 1);
	Meetings.push_back(FMeeting());

	for (int i = 0; i < N; ++i)
	{
		FMeeting Meeting;
		cin >> Meeting.SpendTime;
		cin >> Meeting.Point;
		Meetings.push_back(Meeting);
	}

	int OptimalPoint = 0;

	for (int Day = Meetings.size() - 1; Day > 0; --Day)
	{
		int ResultPoint = Find_OptimalCase(Meetings, Memory_Optimal_Points, Day, LeaveDay);
		if (ResultPoint > OptimalPoint)
		{
			OptimalPoint = ResultPoint;
		}
	}

	cout << OptimalPoint;

	return 0;
}


int Find_OptimalCase(const vector<FMeeting>& InMeetings, vector<int>& OutMemory_OptimalPoints, const int InDay, const int InLeaveDay)
{
	int Day_AfterMeeting = InDay + InMeetings[InDay].SpendTime;

	// 만약 현재 날짜의 미팅이 퇴사 날짜를 넘긴다면
	if (Day_AfterMeeting > InLeaveDay)
	{
		OutMemory_OptimalPoints[InDay] = EErrorType::OVER_TIME;
		return EErrorType::OVER_TIME;
	}

	int OptimalPoint = 0;
	for (int Candidate_Day = Day_AfterMeeting; Candidate_Day <= InLeaveDay - 1; ++Candidate_Day)
	{
		if (OutMemory_OptimalPoints[Candidate_Day] == EErrorType::NOT_VALID)
		{
			int Test = 0;
		}

		if (OutMemory_OptimalPoints[Candidate_Day] > OptimalPoint)
		{
			OptimalPoint = OutMemory_OptimalPoints[Candidate_Day];
		}
	}

	int ResultPoint = InMeetings[InDay].Point + OptimalPoint;

	OutMemory_OptimalPoints[InDay] = ResultPoint;

	return ResultPoint;

}
```
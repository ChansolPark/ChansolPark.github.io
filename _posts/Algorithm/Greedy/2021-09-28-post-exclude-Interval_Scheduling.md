---
title: "Interval_Scheduling"
categories:
  - Greedy
tags:
  - Greedy
---

<br>
<h1>
- 그리디 알고리즘을 이용한 인터벌 스케줄링
</h1>
<br>

수강 과목의 정보가 기록된 구조체 배열이 있고
solution 함수는 수강 과목의 정보를 받아
가장 많은 수강을 할 수 있는 경우의 수를 출력해주는 함수

```cpp
#include <iostream>
using namespace std;

// 대학교의 과목 스케줄표를 받아
// 가장 많이 과목을 듣는 최적을 값을 뽑아내는 그리디 알고리즘

// 판단 기준 : 들을 수 있는 과목중 종료시간이 가장 이른 것
struct StudyClass {
	// 수업 시작 시간
	int startTime;
	// 수업 종료 시간
	int endTime;
};

int solution(StudyClass* studyArr, int length);

// 입력 값은 수동으로 주었다.
int main()
{
	StudyClass classes[5];
	classes[0].startTime = 1;
	classes[0].endTime = 3;
	classes[1].startTime = 1;
	classes[1].endTime = 5;
	classes[2].startTime = 2;
	classes[2].endTime = 6;
	classes[3].startTime = 4;
	classes[3].endTime = 5;
	classes[4].startTime = 6;
	classes[4].endTime = 7;

	cout << "최종 수강 과목 수 : " << solution(classes, 5);

	// 출력 :
	// 수강시작 : 1 수강 완료 : 3
	// 수강시작: 4 수강 완료 : 5
	// 수강시작 : 6 수강 완료 : 7
	// 최종 수강 과목 수 : 3
}

// 최적의 수강 과목 수를 리턴

int solution(StudyClass* studyArr, int length)
{
	int answer = 0;

	
	// 종료 조건 여부 변수
	bool b_IsOver = true;

	// 최소 종료 변수의 시작 시간을 저장할 변수
	int minStartCount = 0;
	// 최소 종료 변수 값을 담을 변수
	int minEndCount = 999;

	// 1교시 부터 시작
	int timeCounter = 1;

	while (true)
	{
		// 반복문 돌때마다 초기화
		b_IsOver = true;
		minEndCount = 999;
		for (int i = 0; i < length; i++)
		{
			// 현재의 시간이 시작시간보다 같거나 커야 수강 가능
				// 수강 가능한것들중 종료시간이 가장 이른것을 찾아냄
			if (timeCounter <= studyArr[i].startTime && studyArr[i].endTime < minEndCount)
			{
				b_IsOver = false;
				minStartCount = studyArr[i].startTime;
				minEndCount = studyArr[i].endTime;
			}
		}

		// 종료 조건 : time이 모든 startTime보다 크다면
		// 종료 조건 체크 후 종료
		if (b_IsOver)
		{
			return answer;
		}

		// 수강 과목 출력
		cout << "수강시작 : " << minStartCount << " 수강 완료 : " << minEndCount << endl;
		// 시간 값에 선택한 과목의 과목 종료시간 대입
		timeCounter = minEndCount;
		// 과목 수강 수 + 1
		answer++;
	}
}
```


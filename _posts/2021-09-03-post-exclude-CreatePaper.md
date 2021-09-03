---
title: "Create Paper (2630)"
categories:
  - Backjoon Algorithm
tags:
  - Divide and conquer algorithm
  - C++
---

<h1>
2630 : 색종이 만들기
</h1>

Link : https://www.acmicpc.net/problem/2630

<br>
풀이 코드

```C++
#include <iostream>

using namespace std;

void CutPaper(int** paper, int paperSize, int y, int x);

int whiteCount;

int blueCount;


int main()
{
	int arrLength;

	cin >> arrLength;

	// 2차원 배열 동적 할당

	int** arr = new int*[arrLength];

	for (int i = 0; i < arrLength; i++)
		arr[i] = new int[arrLength];

	// 배열에 입력받은 값 대입

	for (int i = 0; i < arrLength; i++)
		for (int j = 0; j < arrLength; j++)
			cin >> arr[i][j];
	

	CutPaper(arr, arrLength, 0, 0);

	cout << whiteCount << endl;

	cout << blueCount << endl;

	// 2차원 배열 동적 할당 해제
	for (int i = 0; i < arrLength; i++)
		delete[] arr[i];

}

void CutPaper(int** paper, int paperSize, int y, int x)
{

	// 종료 여부
	bool isFinish = 1;

	// 첫번째 값 넣고
	// 배열을 돌면서 값이 하나라도 다르면 isFinish여부 0으로


	for (int i = y; i < y + paperSize; i++)
	{
		for (int j = x; j < x + paperSize; j++)
		{
			if (paper[y][x] != paper[i][j])
			{
				isFinish = 0;
			}
		}
	}


	// 종료 조건 
	// 크기가 1이거나 원소 모두가 색깔이 같거나
	if (isFinish == 1)
	{
		if (paper[y][x])
		{
			blueCount++;
		}

		else
		{
			whiteCount++;
		}
	}
	else
	{

		int devidePaperSize = paperSize / 2;

		CutPaper(paper, devidePaperSize, y, x);
		CutPaper(paper, devidePaperSize, y + devidePaperSize, x);
		CutPaper(paper, devidePaperSize, y, x + devidePaperSize);
		CutPaper(paper, devidePaperSize, y + devidePaperSize, x + devidePaperSize);
	}

}

```


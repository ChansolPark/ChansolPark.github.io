---
title: "Create Random Maze"
categories:
  - Algorithm (구현)
tags:
  - DFS Algorithm
  - C
  - Backtracking
---
<br>
랜덤 미로 생성 코드

- 변수 선언

```c
<br>
#define _CRT_SECURE_NO_WARNINGS
#define MAX_STACK_SIZE 500

#include <stdio.h>      
#include <stdlib.h>
#include <Windows.h>                               
#include <process.h>
#include <time.h>

int t_set = 0;

int _time = 0;   //시간을 나타내는 전역변수

char map[26][26];

void Gotoxy(int x, int y);

void Put_stone();    //돌 출력

int control_stone(); // 돌 컨트롤 함수

unsigned _stdcall timer(void* arg); //타이머


// 보드 랜덤 생성 함수

void SetRndBoard();


// stack관련 변수 및 함수

POINT stack[MAX_STACK_SIZE];

int top = -1;

int IsEmpty();

int IsFull();

void Push(POINT value);

POINT Pop();

```

- 함수 구현
```c

int main(void) {

	srand(time(NULL));

	system("mode con cols=100 lines=30 | title 미로");


	// 랜덤 보드 생성
	SetRndBoard();

	map[24][25] = 1;

	for (int i = 1; i <= 25; i++) {
		for (int j = 1; j <= 25; j++) {
			if (map[i][j] == 1) printf("■");
			if (map[i][j] == 0) printf("  ");
		}
		printf("\n");
	}
	Gotoxy(24, 25);
	printf("↓");
	map[25][24] = 0;

	// stone 조작
	control_stone();
}

//컨트롤 패널
int control_stone() {

	int x = 2, y = 1;
	char key;
	Gotoxy(x, y);
	Put_stone();
	_beginthreadex(NULL, 0, timer, 0, 0, NULL);

	while (1) {
		SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE), 11);  //앞y 뒤 x
		key = _getch();
		if (65 <= key && key <= 90) key = +32;
		if (key == 56) key = 119;
		else if (key == 48) key = 32;
		else if (key == 52) key = 97;
		else if (key == 54) key = 100;
		else if (key == 53) key = 115;

		switch (key) {     //a=97 d=100 w=119 s=115
		case 119:  //w
			if (1 <= y - 1 && map[y - 1][x] == 0) {
				Gotoxy(x, y);
				printf("  ");
				y--;
				Gotoxy(x, y);
				Put_stone();
			}
			break;

		case 115:  //s
			if (y + 1 <= 25 && map[y + 1][x] == 0) {
				Gotoxy(x, y);
				printf("  ");
				y++;
				Gotoxy(x, y);
				Put_stone();
			}
			break;

		case 100:  //d
			if (map[y][x + 1] == 0) {
				Gotoxy(x, y);
				printf("  ");
				x++;
				Gotoxy(x, y);
				Put_stone();
			}
			break;

		case 97:  //a
			if (map[y][x - 1] == 0) {
				Gotoxy(x, y);
				printf("  ");
				x--;
				Gotoxy(x, y);
				Put_stone();
			}
			break;

		case 27:
			exit(0);
		}

		Gotoxy(38, 15);
		printf("  %d %d  ", x, y);

		if (x == 24 && y == 25) {
			t_set = -1;
			Gotoxy(38, 15);
			printf("탈출 성공!");
			while (1);
			break;
		}
	}
}


// 보드값에 0로 초기화 후 

// 다녀간 곳은 1로 값 할당

void SetRndBoard()
{
	
	// 초기 위치
	POINT pos;
	pos.x = 2;
	pos.y = 2;

	// 난수 생성
	int random = 0;

	// 사방이 막혀있는지 여부 (1이면 사방이 막힘 0이면 한곳이라도 뚫려있음)
	boolean isBlocked = 0;

	// 보드판에 움직일수 있는 곳은 0로 초기화
	for (int i = pos.x; i <= 24; i++)
	{
		for (int j = pos.y; j <= 24; j++)
		{
			map[i][j] = 1;
		}
	}

	// 시작위치 초기화
	map[pos.y][pos.x] = 0;

	// 좌표 저장
	Push(pos);

	while (1)
	{
		// 1로 초기화 
		isBlocked = 1;


		// 상단확인
		if (pos.y >= 4 && map[pos.y - 2][pos.x] == 1)
		{
			isBlocked = 0;
		}
		// 하단확인
		else if (pos.y <= 22 && map[pos.y + 2][pos.x] == 1)
		{
			isBlocked = 0;
		}
		// 좌측확인
		else if (pos.x >= 4 && map[pos.y][pos.x - 2] == 1)
		{
			isBlocked = 0;
		}
		// 우측확인
		else if (pos.x <= 22 && map[pos.y][pos.x + 2] == 1)
		{
			isBlocked = 0;
		}

		// 사방에 뚫린 길이 없음
		if (isBlocked == 1)
		{
			// 전 위치로 돌아감
			pos = Pop();


			if (pos.x == 2 && pos.y == 2)
			{
				return;
			}
		}
		// 한곳이라도 뚫려있다면
		else
		{
			random = rand() % 4; // 난수 생성

			switch (random)
			{
				// 상
			case 0:
				if (pos.y - 2 >= 2 && map[pos.y - 2][pos.x] == 1)
				{

					// 좌표 이동
					map[--pos.y][pos.x] = 0;
					map[--pos.y][pos.x] = 0;

					// 이동한 좌표 저장
					Push(pos);

				}
				break;
				// 하
			case 1:
				if (pos.y + 2 <= 24 && map[pos.y + 2][pos.x] == 1)
				{
					map[++pos.y][pos.x] = 0;
					map[++pos.y][pos.x] = 0;

					Push(pos);
				}
				break;
				// 좌
			case 2:
				if (pos.x - 2 >= 2 && map[pos.y][pos.x - 2] == 1)
				{
					map[pos.y][--pos.x] = 0;
					map[pos.y][--pos.x] = 0;

					Push(pos);
				}
				break;
				// 우
			case 3:
				if (pos.x + 2 <= 24 && map[pos.y][pos.x + 2] == 1)
				{
					map[pos.y][++pos.x] = 0;
					map[pos.y][++pos.x] = 0;

					Push(pos);
				}
				break;
			}
		}
	}


}

void Gotoxy(int x, int y) {

	COORD Pos;
	Pos.X = 2 * x - 2;   // 첫줄에 x좌표를 1로 설정
	Pos.Y = y - 1;
	SetConsoleCursorPosition(GetStdHandle(STD_OUTPUT_HANDLE), Pos);
}



void Put_stone() {

	SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE), 11); //백
	printf("●");
}


unsigned _stdcall timer(void* arg) {

	while (1) {
		Gotoxy(30, 1);
		printf("[플레이시간 : %d sec]", _time);
		if (t_set == -1) return 1;
		Sleep(1040);
		_time++;
	}
}

int IsEmpty() {

	if (top < 0)
		return 1;
	else
		return 0;
}
int IsFull() {

	if (top >= MAX_STACK_SIZE - 1)
		return 1;
	else
		return 0;
}

void Push(POINT value)
{

	if (IsFull() == 1)
		printf("스택이 가득 찼습니다.");
	else
		stack[++top] = value;
}

POINT Pop()
{

	if (IsEmpty() == 1)
		printf("스택이 비었습니다.");
	else
		return stack[top--];
}

```


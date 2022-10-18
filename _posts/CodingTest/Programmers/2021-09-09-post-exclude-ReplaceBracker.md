---
title: "Replace Bracker"
categories:
  - Programmers
classes : wide
tags:
  - C++
---

<h1>
Replace Bracker
</h1>

Link : https://programmers.co.kr/learn/courses/30/lessons/60058

<br>
풀이 코드

```cpp

#include <iostream>
#include <string>
#include <stack>

using namespace std;

string* Devide(string w);
string solution(string w);

int main()
{
	string w = "(()())()";
	cout << solution(w);

	return 0;
}


string solution(string w)
{
	// 나눠진 문자열을 담을 문자열 배열
	string* devideStr;

	// 반환할 값을 담을 변수
	string result = "";

	string u = "";
	string v = "";

	// 입력 문자가 공백이라면 return
	if (w == "")
	{
		return "";
	}
	else
	{
		// 문자열 나눠서
		devideStr = Devide(w);

		// 각각 대입
		u = devideStr[0];
		v = devideStr[1];

		// u의 처음이 '("라면 올바른 괄호 문자열
		// 균형잡인 문자열의 시작이 '('인데 올바르지 않은 문자열이 나올 수 없음.

		// 올바른 괄호라면
		if (u[0] == '(')
		{
			// u 문자열 붙임
			result += u;
			// 나머지 문자열을 재귀를 통해 정렬 후 반환된 문자열을 붙임
			result += solution(v);
		}
		else
		{
			// u가 올바르지 않다면
			// 주어진 공식대로 진행

			result = "";
			result += '(';
			result += solution(v);
			result += ')';


			u.erase(u.begin());
			u.erase(u.end() - 1);

			// 배열 내 괄호 뒤집기
			for (int i = 0; i < u.size(); i++)
			{
				if (u[i] == '(')
				{
					u[i] = ')';
				}
				else if (u[i] == ')')
				{
					u[i] = '(';
				}
			}

			result += u[0];
		}
	}

	// 결과값 출력
	return result;
}

// 문자열 나눠주는 함수
string* Devide(string w)
{
	// 반환할 값을 저장할 변수 선언
	// 0번째 인덱스는 u값을 담음.
	// 1번째 인덱스는 v값을 담음.
	string* returnStr = new string[2];
	returnStr[0] = "";
	returnStr[1] = "";

	// 스택 변수 선언
	stack<char> chStack;

	// 첫번째 문자 스택에 삽입
	chStack.push(w[0]);

	// 첫문자니까 u에 바로 붙임
	returnStr[0] += w[0];

	// 0은 처리했으니 1부터 시작
	int i = 1;

	// size 값만큼 반복문 
	for (; i < w.size(); i++)
	{
		// u에 문자 추가해주고
		returnStr[0] += w[i];

		// 전에 넣은 문자와 현재 문자가 같은지
		if (chStack.top() == w[i])
		{
			//스택에 현재 문자 삽입
			chStack.push(w[i]);
		}
		// 다르다면 
		else
		{
			// 스택에서 값 뽑아냄
			chStack.pop();
			// 비어있다면 짝이 맞는 균형잡힌 문자열.
			if (chStack.empty())
			{
				// 반복문 중지하기전 인덱스값 +1 해줌
				i++;
				break;
			}
		}
	}
	// 나머지 문자열 v에 대입
	for (; i < w.size(); i++)
	{
		returnStr[1] += w[i];
	}


	return returnStr;
}

```


---
title: "N & M (1) (15649)"
categories:
  - Backjoon
tags:
  - DFS
  - C++
---

``` cpp

#include <iostream>
#include <vector>

using namespace std;

struct FComputer_LinkInfo
{
	int start;
	int end;
};

void SpreadVirus(const vector<FComputer_LinkInfo>& _computer_LinkInfos, vector<int>& _visited_Computers, const int _start);
bool IsAlreadyVisited_Computer(vector<int>& _visited_Computers, const int _checkNum);

int main()
{
	ios_base::sync_with_stdio(false);

	vector<FComputer_LinkInfo> computer_LinkInfos;

	int trash;
	cin >> trash;

	int computer_Num;
	cin >> computer_Num;

	for (int i = 0; i < computer_Num; ++i)
	{
		FComputer_LinkInfo LinkInfo;

		cin >> LinkInfo.start;
		cin >> LinkInfo.end;

		computer_LinkInfos.push_back(LinkInfo);

		int temp = LinkInfo.start;
		LinkInfo.start = LinkInfo.end;
		LinkInfo.end = temp;

		computer_LinkInfos.push_back(LinkInfo);
	}

	vector<int> visited_Computers;
	SpreadVirus(computer_LinkInfos, visited_Computers, 1);

	cout << visited_Computers.size() - 1;

	return 0;
}

// 바이러스 퍼뜨리기
void SpreadVirus(const vector<FComputer_LinkInfo>& _computer_LinkInfos, vector<int>& _visited_Computers, const int _start)
{
	// 이미 방문한 컴퓨터라면
	if (IsAlreadyVisited_Computer(_visited_Computers, _start) == true) { return; }
	
	_visited_Computers.push_back(_start);

	for (size_t i = 0; i < _computer_LinkInfos.size(); ++i)
	{
		// 전체 컴퓨터 목록에서 현재 컴퓨터를 찾았다면
		if (_computer_LinkInfos[i].start == _start)
		{
			// 해당 컴퓨터를 통해 다른 컴퓨터로 Virus 전파
			SpreadVirus(_computer_LinkInfos, _visited_Computers, _computer_LinkInfos[i].end);
		}
	}
}

bool IsAlreadyVisited_Computer(vector<int>& _visited_Computers, const int _checkNum)
{
	for (size_t j = 0; j < _visited_Computers.size(); j++)
	{
		if (_visited_Computers[j] == _checkNum)
		{
			return true;
		}
	}

	return false;
}
```
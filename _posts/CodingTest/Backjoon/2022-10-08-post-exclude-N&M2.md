---
title: "N & M 2 (15650)"
classes : wide 
categories:
  - Backjoon
tags:
  - Back Tracking
  - C++
---

``` cpp

#include <iostream>
#include <vector>
#include <string>

using namespace std;

bool IsNum_AlreadyVisited(vector<int>& InSearchedNum_Vector, const int InCheckNum);
void BackTrackingSearch(vector<int>& InSearchedNum_Vector, const int InNumArea, const int InSearchDepth, const int ParentNum);

string Result;

int main()
{
    int NumArea;
    cin >> NumArea;

    int SearchDepth;
    cin >> SearchDepth;

    vector<int> SearchedNum_Vectpr;
    SearchedNum_Vectpr.reserve(SearchDepth);

    BackTrackingSearch(SearchedNum_Vectpr, NumArea, SearchDepth, 1);

    cout << Result;
}

bool IsNum_AlreadyVisited(vector<int>& InSearchedNum_Vector, const int InCheckNum)
{
    for (int InSearchedNum : InSearchedNum_Vector)
    {
        if (InSearchedNum == InCheckNum)
        {
            return true;
        }
    }
    return false;
}

void BackTrackingSearch(vector<int>& InSearchedNum_Vector, const int InNumArea, const int InSearchDepth, const int ParentNum)
{
    if (InSearchedNum_Vector.size() == InSearchDepth)
    {
        for (int InSearchedNum : InSearchedNum_Vector)
        {
            Result += to_string(InSearchedNum) + " ";
        }
        Result += "\n";
        return;
    }

    for (int i = ParentNum; i <= InNumArea; ++i)
    {
        // 방문한 적이 없다면
        if (IsNum_AlreadyVisited(InSearchedNum_Vector, i) == false)
        {
            InSearchedNum_Vector.push_back(i);
            BackTrackingSearch(InSearchedNum_Vector, InNumArea, InSearchDepth, i);
            InSearchedNum_Vector.pop_back();
        }
    }
}


```
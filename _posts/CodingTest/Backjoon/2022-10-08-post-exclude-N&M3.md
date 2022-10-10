---
title: "N & M 3 (15651)"
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

    for (int i = 1; i <= InNumArea; ++i)
    {
        InSearchedNum_Vector.push_back(i);
        BackTrackingSearch(InSearchedNum_Vector, InNumArea, InSearchDepth, i);
        InSearchedNum_Vector.pop_back();
    }
}



```
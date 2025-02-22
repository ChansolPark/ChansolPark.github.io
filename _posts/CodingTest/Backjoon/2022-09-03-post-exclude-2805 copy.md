---
title: "Cut Trees (2805)"
categories:
  - Backjoon
classes : wide
tags:
  - Binary Search
  - C++
---

취업 시기 이후로 알고리즘을 내팽겨 두던 날 반성하며.. 이진 탐색부터 정진해보려 한다.
해당 문제를 풀면서, 제시된 예제와 내가 만든 예제들은 답이 제대로 나오는데, 정작 체점을 하면 오답으로 나와 끙끙 앓았다.. 논리적 결함을 도저히 못 찾겠어서 다른 분들의 답을 보니, 내 코드는 자료형의 범위에 대한 고려가 되어 있지 않다는 것이 였다.. 그래서 자료형을 수정 하니 정답을 받았다. 

``` cpp

#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

void Find_RightHeight(const vector<int>& InTrees, const int Min_Cut_Height, const int Max_Cut_Height, const int InTarget_ResultSize);

long long int GetResultTreeSize(const vector<int>& InTrees, const int InCut_Height);

static int MaxHeight = 0;

int main()
{
    vector<int> Trees;
    int Length = 0;
    int Target_ResultSize = 0;
    cin >> Length;

    Trees.reserve(Length);
    cin >> Target_ResultSize;
    for (int i = 0; i < Length; ++i)
    {
        int Value;
        cin >> Value;
        Trees.push_back(Value);
    }
    sort(Trees.begin(), Trees.end());

    Find_RightHeight(Trees, 0, Trees[Trees.size() - 1], Target_ResultSize);

    cout << MaxHeight;

    return 0;
}

void Find_RightHeight(const vector<int>& InTrees, const int Min_Cut_Height, const int Max_Cut_Height, const int InTarget_ResultSize)
{
    if (Min_Cut_Height > Max_Cut_Height)
    {
        return;
    }

    int Cut_Height = (Min_Cut_Height + Max_Cut_Height) / 2;

    long long int ResultTreeSize = GetResultTreeSize(InTrees, Cut_Height);

    if (ResultTreeSize >= InTarget_ResultSize)
    {
        if (Cut_Height > MaxHeight)
        {
            MaxHeight = Cut_Height;
        }
    }

    if (ResultTreeSize > InTarget_ResultSize)
    {
        Find_RightHeight(InTrees, Cut_Height + 1, Max_Cut_Height, InTarget_ResultSize);
        return;
    }

    if (ResultTreeSize < InTarget_ResultSize)
    {
        Find_RightHeight(InTrees, Min_Cut_Height, Cut_Height - 1, InTarget_ResultSize);
        return;
    }
}

long long int GetResultTreeSize(const vector<int>& InTrees, const int InCut_Height)
{
    long long int result = 0;
    for (size_t Index = 0; Index < InTrees.size(); ++Index)
    {
        int Cutten_TreeSize = InTrees[Index] - InCut_Height;
        if (Cutten_TreeSize < 0)
        {
            Cutten_TreeSize = 0;
        }
        result += Cutten_TreeSize;
    }

    return result;
}
```
---
title: "Coloring Book"
categories:
  - Kakao
classes : wide
tags:
  - DFS algorithm
  - C++
---

<h1>
Coloring Book
</h1>

Link : https://programmers.co.kr/learn/courses/30/lessons/1829

<br>
풀이 코드

```cpp

#include <iostream>
#include <vector>
#include <stack>
using namespace std;

class POINT {
public:
    int x;
    int y;
    POINT()
    {
        x = 0;
        y = 0;
    }
    POINT(int _x, int _y)
    {
        x = _x;
        y = _y;
    }
};

int size_of_one_area = 0;
vector<vector<int>> GetAreaSize(vector<vector<int>> picture, int y, int x, int areaNum);


// 전역 변수를 정의할 경우 함수 내에 초기화 코드를 꼭 작성해주세요.
vector<int> solution(int m, int n, vector<vector<int>> picture) {
    int number_of_area = 0;
    int max_size_of_one_area = 0;
    size_of_one_area = 0;
    // picture를 반복문 돌면서 0이 아닌값 찾기. 
    // 아닌 값 찾으면 find 함수 실행
    for (int i = 0; i < picture.size(); i++)
    {
        for (int j = 0; j < picture[0].size(); j++)
        {
            if (picture[i][j] != 0)
            {
                number_of_area++;
                picture = GetAreaSize(picture, i, j, picture[i][j]);

                if (size_of_one_area > max_size_of_one_area)
                    max_size_of_one_area = size_of_one_area;
            }
        }
    }


    vector<int> answer(2);
    answer[0] = number_of_area;
    answer[1] = max_size_of_one_area;
    return answer;
}

// 영역의 크기를 반환 해주는 함수.
// 확인 한 영역들은 0으로 초기화
vector<vector<int>> GetAreaSize(vector<vector<int>> picture, int y, int x, int areaNum)
{
    size_of_one_area = 0;
    int randNum = 0;
    int isBlock = 0;

    stack<POINT> posStack;
    POINT pos;

    // 시작 위치 저장
    pos.x = x;
    pos.y = y;
    posStack.push(pos);

    picture[pos.y][pos.x] = 0;


    // 영역 카운트 증가
    size_of_one_area++;

    while (1)
    {
        isBlock = 1;
        // 사방중 한곳이라도 갈수 있는 곳이 있는지
        if (pos.y > 0 && picture[pos.y - 1][pos.x] == areaNum)
        {
            isBlock = 0;

            // 위로 이동
            pos.y--;
            posStack.push(pos);

            picture[pos.y][pos.x] = 0;

            size_of_one_area++;
        }
        else if (pos.y < picture.size() - 1 && picture[pos.y + 1][pos.x] == areaNum)
        {
            isBlock = 0;
            pos.y++;
            posStack.push(pos);

            picture[pos.y][pos.x] = 0;

            size_of_one_area++;
        }
        else if (pos.x > 0 && picture[pos.y][pos.x - 1] == areaNum)
        {
            isBlock = 0;
            pos.x--;
            posStack.push(pos);

            picture[pos.y][pos.x] = 0;

            size_of_one_area++;
        }
        else if (pos.x < picture[0].size() - 1 && picture[pos.y][pos.x + 1] == areaNum)
        {
            isBlock = 0;
            pos.x++;
            posStack.push(pos);

            picture[pos.y][pos.x] = 0;

            size_of_one_area++;
        }
        // 사방이 막힘
        if (isBlock == 1)
        {
            // 시작위치와 같다면
            if (pos.x == x && pos.y == y)
            {
                break;
            }

            posStack.pop();
            pos = posStack.top();

        }


    }
    return picture;
}

int main()
{
    int m = 0;
    int n = 0;

    cin >> m;
    cin >> n;
    vector<vector<int>> picture(m, vector<int>(n, 0));
    int num = 0;
    for (int i = 0; i < m; i++)
    {
        for (int j = 0; j < n; j++)
        {
            cin >> picture[i][j];
        }
    }
    vector<int> answer;

    answer = solution(picture.size(), picture[0].size(), picture);

    cout << answer[0] << endl;
    cout << answer[1] << endl;
    return 0;
}
```


---
title: "InsertionSort"
categories:
  - Sort
tags:
  - Sort Algorithm
  - C++
---

직접 구현해본 삽입 정렬

```cpp

void InsertionSort(int nums[])

{

	for (int i = 0; i < 10; i++)
	{
		for (int j = i; j >= 0; j--)
		{
			// 비교할 대상이 있을때 조건 검사
			if (j > 0)
			{
				if (nums[j] < nums[j - 1])
				{
					int temp = nums[j - 1];
					nums[j - 1] = nums[j];
					nums[j] = temp;
				}
				else
					break;
			}
		}
	}
}
```
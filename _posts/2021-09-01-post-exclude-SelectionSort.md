---
title: "Implement_SelectionSort"
categories:
  - Implement (구현)
tags:
  - Sort Algorithm
  - C++
---

직접 구현해본 선택 정렬

```C++
<br>

void SelectionSort(int nums[])
{
	int minIndex = -1;

	for (int i = 0; i < 10; i++)
	{
		
		minIndex = -1;

		// 최소값 검사
		for (int j = i; j < 10; j++)
		{
			if (nums[minIndex] > nums[j])
			{
				minIndex = j;
			}
		}

		// 정렬되어야 하는 값이 있다면
		if (minIndex != -1)
		{
			// 자리 변경
			int temp = nums[i];
			nums[i] = nums[minIndex];
			nums[minIndex] = temp;
		}
	}
}
```
---
title: "SelectionSort"
classes : wide
categories:
  - Sort
tags:
  - C++
---
<br>
직접 구현해본 선택 정렬

```cpp
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
---
title: "QuickSort (Lomuto)"
categories:
  - Sort
tags:
  - C++
---
<br>
직접 구현해본 퀵(로무토) 정렬


```cpp


void QuickSort(int nums[], int start, int end)

{

	// 마지막 깊이의 함수라면
	if (start >= end)
	{
		return;
	}

	int pivot = partition(nums, start, end);

	// pivot의 좌측 재귀
	QuickSort(nums, start, pivot - 1);
	// pivot의 우측 재귀
	QuickSort(nums, pivot + 1, end);

}


int partition(int nums[], int left, int pivot)

{

	int temp = 0;

	for (int i = left; i < pivot; i++)
	{
		// 기준값 (피봇)보다 작다면
		if (nums[i] < nums[pivot])
		{
			temp = nums[left];
			nums[left] = nums[i];
			nums[i] = temp;

			left++;
		}
	}

	// pivot값과 left값 변경

	temp = nums[pivot];
	nums[pivot] = nums[left];
	nums[left] = temp;

	pivot = left;

	return pivot;
}
```
---
title: "QuickSort (Hoare)"
categories:
  - Sort
tags:
  - C++
---

<br>
직접 구현해본 퀵(호어) 정렬


```cpp


void QuickSort(int* nums, int left, int right)
{
	// 검사할 원소가 1개라면
	if (left > right)
	{
		return;
	}

	int pivot = left;

	int low = left + 1;
	int high = right;

	while (low <= high)
	{

		// 둘다 찾은상태라면 (증가가 멈춘상태)
		if (nums[low] > nums[pivot] && nums[high] <= nums[pivot])
		{
			int temp = nums[low];
			nums[low] = nums[high];
			nums[high] = temp;
		}

		// left는 오른쪽으로 가며 pivot보다 큰값을 찾을떄까지 증가
		if (nums[low] <= nums[pivot])
		{
			low++;
		}
		// right는 오른쪽으로 가며 pivot보다 작은값 찾을떄까지 증가
		if (nums[high] > nums[pivot])
		{
			high--;
		}
	}

	// pivot과 right를 변경
	int temp = nums[pivot];
	nums[pivot] = nums[high];
	nums[high] = temp;

	pivot = high;

	QuickSort(nums, left, pivot - 1);
	QuickSort(nums, pivot + 1, right);
}
```
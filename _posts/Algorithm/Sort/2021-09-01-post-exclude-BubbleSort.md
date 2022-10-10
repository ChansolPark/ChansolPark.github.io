---
title: "BubbleSort"
classes : wide
categories:
  - Sort
tags:
  - C++
---
<br>
직접 구현해본 버블 정렬

```cpp

void BubbleSort(int nums[])

{

	for (int i = 10; i > 0; i--)
	{
		for (int j = 0; j < i - 1; j++)
		{
			if (nums[j] > nums[j + 1])
			{
				int temp = nums[j];
				nums[j] = nums[j + 1];
				nums[j + 1] = temp;
			}
		}
	}
}
```
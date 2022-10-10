---
title: "MergeSort"
classes : wide
categories:
  - Sort
tags:
  - C++
---
<br>
직접 구현해본 병합 정렬

```cpp

int* MergeSort(int nums[], int numsSize)
{

	/*
	* 1. 배열의 크기가 1인지 검사후 1이라면 리턴
	* 2. 배열을 둘로 나눔
	* 3. 둘로 나눈 배열을 재귀함수에 넣음.
	* 4. 정렬 함수 호출
	* 5. 정렬된 배열 반환
	*/

	// 크기가 1이라면 반환
	if (numsSize == 1)
	{
		return nums;
	}

	// 크기값을 2로 나눔
	int devideSize = numsSize / 2;

	// 두 배열에 nums 배열을 나눠 대입
	// 
	// ex) devideSize가 5라면 
	//     devideArray1에는 2가 들어가고
	//     devideArray2에는 3이 들어감

	int* devideArray1 = new int[devideSize];
	int* devideArray2 = new int[numsSize - devideSize];

	// 나뉜 배열에 값 대입

	for (int i = 0; i < numsSize; i++)
	{
		if (i < devideSize)
		{
			devideArray1[i] = nums[i];
		}
		else
		{
			devideArray2[i - devideSize] = nums[i];
		}
	}

	// 나눈 두 배열을 재귀함수를 통해 크기가 1이될떄까지 나눔
	int* tempArray1 = MergeSort(devideArray1, devideSize);
	int* tempArray2 = MergeSort(devideArray2, numsSize - devideSize);

	// 나뉘어 반환된 배열들을 병합 및 정렬
	int* mergeArray = SortArrays(devideArray1, devideSize, devideArray2, numsSize - devideSize);

	// 병합 및 정렬된 배열을 반환
	return mergeArray;
}

// 두개의 배열을 받아 하나의 배열에 정렬해서 반환 

int* SortArrays(int* arr1, int arr1Size , int* arr2, int arr2Size)
{

	int i = 0, j = 0, count = 0;

	// 병합할 배열을 선언
	int* mergeArray = new int[arr1Size + arr2Size];
	int mergeArrayLength = arr1Size + arr2Size;

	// 두개의 배열을 정렬해서 하나의 배열에 대입하는 반복문
	for (int count = 0; count < mergeArrayLength; count++)
	{

		// 둘중 먼저 원소값의 대입이 끝나는 배열이 있다면 다른 배열을 순차적으로 대입해주는 조건문
		if (i >= arr1Size)
		{
			mergeArray[count] = arr2[j];
			++j;
		}

		else if (j >= arr2Size)
		{
			mergeArray[count] = arr1[i];
			++i;
		}
		
		// 특정한 배열의 대입이 끝나지 않았다면 크기비교후 값 대입
		else
		{
			if (arr1[i] < arr2[j])
			{
				mergeArray[count] = arr1[i];
				++i;
			}
			else
			{
				mergeArray[count] = arr2[j];
				++j;
			}
		}
	}

	// 배열 리턴
	return mergeArray;
}
```
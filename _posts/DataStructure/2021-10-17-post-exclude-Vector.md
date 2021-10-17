---
title: "Vector"
categories:
  - DataStructure
tags:
  - C++
---
  
<br>
<h1>
Vector
</h1>
<br>
  
  - 배열과 비슷한 역할을 하지만 큰 차이점은 크기가 변할수 있다는 점인 것 같다.
  
  - 간략화 하여 구현해본 Vector

```cpp
#include "MyVector.h"

using namespace std;

//Default Constructor.
MyVector::MyVector()
{
	_vectorIndex = -1;
	_vectorSize = 0;
	_vectorCapacity = 1;

	_myObject = nullptr;
}

// Constructor.
MyVector::MyVector(int capacity)
{
	_vectorIndex = -1;
	_vectorSize = capacity;
	_vectorCapacity = capacity * 2;

	if (_myObject)
		delete[]_myObject;

	_myObject = new MyObject[_vectorCapacity];
}

// Copy constructor.
MyVector::MyVector(const MyVector& other)
{
	_vectorIndex = -1;

	_vectorCapacity = other._vectorCapacity;
	_vectorSize = other._vectorSize;

	if (_myObject)
		delete[]_myObject;

	_myObject = new MyObject[_vectorCapacity];

	for (int count1 = 0; count1 < _vectorCapacity; count1++)
	{
		_myObject[count1]._id = other._myObject[count1]._id;
	}
}

// Assignment operator.
MyVector& MyVector::operator=(const MyVector& other)
{
	if (this != &other) {

		_vectorCapacity = other._vectorCapacity;
		_vectorSize = other._vectorSize;
		_vectorIndex = other._vectorIndex;

		if (_myObject)
			delete[]_myObject;

		_myObject = new MyObject[_vectorCapacity];

		for (int count1 = 0; count1 < _vectorCapacity; count1++)
		{
			_myObject[count1]._id = other._myObject[count1]._id;
		}
	}
	return *this;
}

// Destructor.
MyVector::~MyVector()
{
		delete[] _myObject;
}

// Returns current capacity of this vector.
int MyVector::GetCapacity() const
{
	return _vectorCapacity;
}

// Returns current size of this vector.
int MyVector::GetSize() const
{
	return _vectorSize;
}

// Returns End Index of this vector.
int MyVector::End() const
{
	return _vectorIndex + 1;
}

// Creates a new MyObject instance with the given ID, and appends it to the end of this vector.
void MyVector::Add(int id)
{
	// +1 해서 값을 대입 할 수 있도록
	++_vectorIndex;

	// size 값 증가 필요시
	if (_vectorIndex == _vectorSize)
	{
		// size 값 증가
		++_vectorSize;

		// size 값이 최대크기와 같아질 경우
		if (_vectorSize == _vectorCapacity)
		{
			// 크기 확장
			Grow();
		}
	}

	// 해당 인덱스에 값 대입
	_myObject[_vectorIndex]._id = id;
}

// expand the Size
void MyVector::Grow()
{
	_vectorCapacity *= 2;
	MyObject* answer = new MyObject[_vectorCapacity];

	// 값 복사
	for (int count1 = 0; count1 < _vectorSize; count1++)
	{
		answer[count1]._id = _myObject[count1]._id;
	}

	if (_myObject)
		delete[]_myObject;

	_myObject = answer;
}

// Returns the first occurrence of MyObject instance with the given ID.
// Returns nullptr if not found.
MyObject* MyVector::FindById(int MyObjectId) const
{
	for (int count1 = 0; count1 < End(); count1++)
	{
		if (_myObject[count1]._id == MyObjectId)
		{
			return &_myObject[count1];
		}
	}
	return nullptr;
}

// Trims the capacity of this vector to current size.
void MyVector::TrimToSize()
{
	// Size값 현재 벡터의 크기에 맞게 초기화
	_vectorCapacity = _vectorSize;

	// 사이즈 값대로 재 할당
	MyObject* answer = new MyObject[_vectorSize];

	for (int count1 = 0; count1 < _vectorSize; count1++)
	{
		answer[count1]._id = _myObject[count1]._id;
	}

	if (_myObject)
		delete[]_myObject;

	_myObject = answer;

}

// Returns the MyObject instance at the specified index.
MyObject& MyVector::operator[](size_t index)
{
	return _myObject[index];
}

// Returns string representation of the vector.
string MyVector::ToString() const
{
	string str = "";
	for (int count1 = 0; count1 < End(); count1++)
	{
		str += to_string(_myObject[count1]._id);

		// 마지막이 아닐때만 컴마 찍기
		if (count1 < End() - 1)
		{
			str += ", ";
		}
	}
	return str;
}

// Remove all MyObject instances with the given ID in this vector.
void MyVector::RemoveAll(int MyObjectId)
{
	MyObject* temp = new MyObject[_vectorCapacity]();
	int tempCount = 0;

	// 각 요소 검사
	for (int count1 = 0; count1 < _vectorCapacity; count1++)
	{
		// 해당되지 않는 요소들을 temp에 추가
		if (_myObject[count1]._id != MyObjectId)
		{
			temp[tempCount]._id = _myObject[count1]._id;
			++tempCount;
		}
	}

	if (_myObject)
		delete[]_myObject;

	_myObject = temp;

	// 변경된 벡터에 맞게 사이즈 값 및 인덱스 카운터 값 변경
	_vectorSize = tempCount;
	_vectorIndex = tempCount - 1;
}


// Returns a newly allocated array of MyVector objects,
// each of whose elements have the same "_id" value of the MyObject struct.
// The 'numGroups' is an out parameter, and its value should be set to
// the size of the MyVector array to be returned.
MyVector* MyVector::GroupById(int* numGroups)
{
	// 1. N * 2 의  2차원 배열에 그루핑 결과 값을 대입
	// ex ) Vector1 = {1, 3, 1, 2}
	//	{1, 2}
	//	{2. 1}
	// 	{3, 1}

	// 0번째 : 해당 값, 1번째 : 해당 값의 갯수

	// 동적 할당
	int** group_Arr = new int* [End()];
	for (int count1 = 0; count1 < End(); count1++)
		group_Arr[count1] = new int[2]();

	// Index 카운터
	int group_Index = 0;

	// 이미 그룹에 존재하는 값인지 여부
	bool b_isGroup = false;

	// MyObject 요소들 순회하며 그루핑
	for (int count1 = 0; count1 < End(); count1++)
	{
		b_isGroup = false;
		for (int count2 = 0; count2 < group_Index; count2++)
		{
			// 현재 검사중인 요소가 이미 그룹 배열에 있는 값인지 ?
			if (_myObject[count1]._id == group_Arr[count2][0])
			{
				// 그룹 존재 여부 True
				b_isGroup = true;
				// 갯수 증가
				group_Arr[count2][1]++;
			}
		}
		// 아니라면 배열에 새로 등록
		if (!b_isGroup)
		{
			group_Arr[group_Index][0] = _myObject[count1]._id;
			group_Arr[group_Index][1]++;

			// 카운터 증가
			group_Index++;
		}
	}
	

	// 2. 2차원 배열대로 MyVector* 생성 후 반환 
	

	// 클래스 배열 생성 해야함
	MyVector* temp = new MyVector[group_Index];

	int group_number = 0;
	int group_Size = 0;

	for (int count1 = 0; count1 < group_Index; count1++)
	{
		// 현재 대입할 값
		group_number = group_Arr[count1][0];

		// 대입 할 값의 갯수
		group_Size = group_Arr[count1][1];

		// 동적 할당
		temp[count1]._myObject = new MyObject[group_Size];

		for (int count2 = 0; count2 < group_Size; count2++)
		{
			temp[count1].Add(group_number);
		}
	}

	// 2차원 배열 동적 해제
	for (int count1 = 0; count1 < End(); count1++)
		delete[] group_Arr[count1];

	*numGroups = group_Index;

	return temp;
}
```
 
        





  
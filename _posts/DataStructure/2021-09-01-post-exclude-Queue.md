---
title: "Queue"
categories:
  - DataStructure
tags:
  - C++
---

직접 구현해본 Queue 클래스

```cpp

class QueueC 
{
  
private:

	// queue 포인터 변수 (동적 할당위한 변수)<br>
	int* queueArr;

	// queue의 크기 값을 저장할 변수
	int qLength;

	// Pop할 위치값을 저장하는 변수
	int front;

	// Push할 위치값을 저장하는 변수
	int back;

	// 값이 몇개 들어가 있는지 카운트 해줄 갯수
	int fullCount;

public:

	QueueC(int _qLength)
	{
		qLength = _qLength;

		queueArr = new int[qLength];
		front = -1;
		back = -1;

		fullCount = 0;
	}

	void Push(int _num)
	{
		// overflow
		if (fullCount == qLength)
		{
			cout << "overflow" << endl;
		}
		else
		{
			fullCount++;

			back++;
			if (back == qLength)
			{
				back = 0;
			}

			queueArr[back] = _num;
			cout << _num << "값 삽입 완료." << endl;
		}
	}

	int Pop()
	{
		if (fullCount == 0)
		{
			cout << "underflow" << endl;
		}
		else
		{
			fullCount--;


			front++;
			if (front == qLength)
			{
				front = 0;
			}

			int temp = queueArr[front];
			queueArr[front] = 0;

			cout << temp << "값 추출 완료." << endl;
			return temp;
		}
	}

	void Print()
	{
		for (int i = 0; i < qLength; i++)
		{
			cout << queueArr[i] << "   ";
		}
		cout << endl;
	}

};
```
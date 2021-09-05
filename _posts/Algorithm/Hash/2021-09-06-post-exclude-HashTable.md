---
title: "HashTable"
categories:
  - Hash
tags:
---

<br>
<h1>
- 해시 테이블
</h1><br>

- 매우 빠른속도를 가진 자료구조중 하나이다.
  <br><br>

- 검색, 삽입, 삭제의 평균시간이 O(1)로 매우 빠르다. 
  <br><br>

- 해시 테이블은 탐색 알고리즘, 반복문 없이 해당하는 인덱스 값을 찾을수 있다.
	- 하지만 값을 삽입하는 과정에서 충돌이 났을경우 해시코드에 해당하는 인덱스에 값이 여러개가 되므로, 시간복잡도는 O(N)이 된다.
	- 그래서 배열의 크기를 소수로, 충분하게 크게 잡으면 대부분의 경우에 O(1)의 속도를 가진다.

<br><br>
<h1>
- 구현 코드 
</h1>

```cpp

using namespace std;
#include <iostream>

static const unsigned int FNV_PRIME = 16777619u;
static const unsigned int OFFSET_BASIS = 2166136261u;

#define HASH_TABLE_LENGTH 11
```

- 해시값이 충돌할 경우 필요한 연결리스트 클래스 구현

```cpp
class NodeClass {
private:
	// 값을 저장할 변수
	string num;

	// 충돌한 값들을 연결할 연결리스트
	NodeClass* nextNode;
public:
	NodeClass()
	{
		num = "";
		nextNode = NULL;
	}
	NodeClass(string _num)
	{
		num = _num;
		nextNode = NULL;
	}

	// 연결된 노드의 마지막 노드에 새로운 노드를 연결해주는 함수
	void insertNewNode(string _inputStr)
	{
		// 현재 연결된 마지막 노드를 가리킬 변수
		NodeClass* lastNode = this;


		while (lastNode->nextNode != NULL)
		{
			lastNode = lastNode->nextNode;
		}

		lastNode->nextNode = new NodeClass(_inputStr);
	}

	// 연결된 노드들을 돌면서 값이 있는지 여부 검사 . (있으면 1, 없으면 0 리턴)
	int searchNode(string _findStr)
	{
		// 현재 연결된 마지막 노드를 가리킬 변수
		NodeClass* lastNode = this;

		do
		{
			if (_findStr == lastNode->num)
			{
				return 1;
			}
			lastNode = lastNode->nextNode;

		} while (lastNode != NULL);

		return 0;
	}

	void PrintNode()
	{
		// 현재 연결된 마지막 노드를 가리킬 변수
		NodeClass* lastNode = this;

		do
		{
			cout << lastNode->num << "  ";
			lastNode = lastNode->nextNode;

		} while (lastNode != NULL);

	}
};

```

- 해시 테이블의 각각의 인덱스를 구성할 클래스 구현

``` cpp

class HashTableC
{
private:

	// 값을 저장하고 다음 노드를 가르킬 노드 변수
	NodeClass node;
	// 값이 이미 저장되어 있는지 (충돌 발생) 여부를 담을 변수
	bool isCrash;


public:
	HashTableC()
	{
		isCrash = false;
	}

	void Insert(string _insertNum)
	{
		// 충돌 발생시
		if (isCrash)
		{
			node.insertNewNode(_insertNum);
		}
		// 해쉬 충돌이 일어나 중복인덱스에 저장되어야 할때
		else
		{
			isCrash = true;

			// 현재 노드에 값 저장
			node = NodeClass(_insertNum);
		}
	}

	// 값을 찾았을 경우 1리턴 못찾았으면 0리턴
	int Search(string _findNum)
	{
		// 값이 있는지 검사
		if (node.searchNode(_findNum) == 1)
			return 1;

		return 0;
	}

	void PrintNode()
	{
		// 한줄에 연결되어 있는 노드의 값들을 쭉 출력해줌
		node.PrintNode();
		cout << endl;
	}


};
```

- 메인 함수

```cpp
static unsigned int fnvHash(const char* str);

int main()
{
	HashTableC hashTable[HASH_TABLE_LENGTH];

	// 입력 문자열
	string inputStr1 = "ABC";
	string inputStr2 = "ABasdfasdf";

	// 해시값을 저장할 변수
	int hashCode;

	
	// 배열에 값 저장
	hashCode = fnvHash(inputStr1.c_str()) % HASH_TABLE_LENGTH;
	hashTable[hashCode].Insert(inputStr1);

	hashCode = fnvHash(inputStr2.c_str()) % HASH_TABLE_LENGTH;
	hashTable[hashCode].Insert(inputStr2);

	// 저장 확인
	for (int i = 0; i < HASH_TABLE_LENGTH; i++)
	{
		hashTable[i].PrintNode();
	}

	// 값이 있으면 1을 리턴 없으면 0을 리턴하는 함수
	hashCode = fnvHash(inputStr1.c_str()) % HASH_TABLE_LENGTH;
	cout << hashTable[hashCode].Search(inputStr1.c_str()) << endl;
	// 1 출력

	hashCode = fnvHash(inputStr2.c_str()) % HASH_TABLE_LENGTH;
	cout << hashTable[hashCode].Search(inputStr2.c_str()) << endl;
	// 1 출력

	inputStr2 = "afasdf";
	hashCode = fnvHash(inputStr2.c_str()) % HASH_TABLE_LENGTH;
	cout << hashTable[hashCode].Search(inputStr2.c_str()) << endl;
	// 0 출력

}

```

사용한 함수는 fnv 해시 함수

Link : https://gist.github.com/hwei/1950649d523afd03285c

```cpp
static unsigned int fnvHash(const char* str)
{
	const size_t length = strlen(str) + 1;
	unsigned int hash = OFFSET_BASIS;
	for (size_t i = 0; i < length; ++i)
	{
		hash ^= *str++;
		hash *= FNV_PRIME;
	}
	return hash;
}
```

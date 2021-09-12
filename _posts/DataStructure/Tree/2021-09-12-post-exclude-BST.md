---
title: "BST"
categories:
  - Tree
tags:
  - C++
---
<br>

<h1>
- BST
</h1>

<br>
- 이진 트리 (Binary Tree) : 
  
  - 자식노드의 최대 노드 수가 2인 트리
  
  - 왼쪽 자식, 오른쪽 자식
  
<br>
<br>

- 이진 탐색 트리 (Binary Search Tree, BST) :
  
  - 이진 트리에서 +a 를 한 트리
    - 이진트리에서 좌, 우 자식에 값을 넣는 조건을 추가한 트리.

  - 시간 복잡도 : 
    - 탐색 O(Log n)
    - 삽입 O(Log n)
  
  - BST는 가지를 뻗어나갈뿐 기존의 가지들은 변하지 않음
  
  - 직접 구현한 BST 코드

```cpp
#include <iostream>
using namespace std;

class Node
{
private:
	int data;
public:
	Node* leftChild;
	Node* rightChild;

	Node(int _data)
	{
		data = _data;
		leftChild = NULL;
		rightChild = NULL;
	}
	int GetData()
	{
		return data;
	}

	void Insert_New_Node(int _insertNum)
	{
		if (_insertNum < this->data)
		{
			if (leftChild == NULL)
				leftChild = new Node(_insertNum);
			else
				leftChild->Insert_New_Node(_insertNum);
		}
		else
		{
			if (rightChild == NULL)
				rightChild = new Node(_insertNum);
			else
				rightChild->Insert_New_Node(_insertNum);
		}
	}


	// 찾으면 1 못찾으면 0
	int Search_Node(int _findNum)
	{
		if (_findNum == this->data)
		{
			return 1;
		}

		if (_findNum < this->data)
		{
			if (this->leftChild == NULL)
				return 0;
			return this->leftChild->Search_Node(_findNum);
		}

		if (this->rightChild == NULL)
			return 0;

		return this->rightChild->Search_Node(_findNum);
	}

	void Delete_Node(int _deleteNum)
	{
		// 삭제할 노드에 도착
		if (this->data == _deleteNum)
		{
			Node* leftLeap = leftChild;

			if (leftLeap->rightChild = NULL)
			{
				this->leftChild = leftLeap->leftChild;
			}
			else
			{
				while (leftLeap->rightChild != NULL)
				{
					leftLeap = leftLeap->rightChild;
				}
			}
			this->data = leftLeap->data;

			delete leftLeap;
		}
		else if (_deleteNum < this->data)
		{
			// 찾는 값 없음
			if (this->leftChild == NULL)
				return;

			// 왼쪽 자식에서 삭제할 노드를 찾아봄
			this->leftChild->Delete_Node(_deleteNum);

		}
		else
		{
			// 찾는 값 없음
			if (this->rightChild == NULL)
				return;

			this->rightChild->Delete_Node(_deleteNum);
		}
	}
};

int main()
{
	Node* rootNode = new Node(10);
	rootNode->Insert_New_Node(2);
	rootNode->Insert_New_Node(1);
	rootNode->Insert_New_Node(12);
	rootNode->Insert_New_Node(15);

	cout << rootNode->Search_Node(2) << endl; // 1
	cout << rootNode->Search_Node(12) << endl; // 1

	rootNode->Delete_Node(2);

	cout << rootNode->Search_Node(2) << endl; // 0
	cout << rootNode->Search_Node(12) << endl; // 1
	return 0;
}




```

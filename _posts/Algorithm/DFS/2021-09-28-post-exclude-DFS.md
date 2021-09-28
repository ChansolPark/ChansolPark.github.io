---
title: "DFS"
categories:
  - Algorithm
tags:
  - Search Algorithm
---

<br>
<h1>
- 깊이 우선 탐색 (DFS)
</h1>
<br>

- 깊이 우선 탐색

  - 탐색의 경로가 정해지지 않았을때 일단 하나의 경로를 정해 탐색이 가능한 곳까지 탐색하는 기법
  
  - 예를 들어 트리구조에서 어떠한 노드를 찾는다고 가정하면, 하나의 자식을 선택해 리프노드까지 탐색
  
  - BFS가 트리구조의 그림 상에서 가로로 탐색을 진행하는 반면, DFS는 세로로 탐색함
  
  - 스택(Stack)으로 쉽게 구현 가능

<br><br>

- 소스코드
  - BFS의 코드에서 큐 -> 스택 만 해주면 DFS 방식으로 작동한다.
  
  ```cpp
  int Search_Node_DFS(Node* _node, int _findNum)
	{
		stack<Node*> nodeStack;

		nodeStack.push(_node);

		Node* node = NULL;
		// 노드가 비어있지 않다면 반복 (비었을 경우는 모든 노드를 탐색했을때 뿐)
		while (!nodeStack.empty())
		{
			// 스택에서 자료를 받아옴
			node = nodeStack.top();
			nodeStack.pop();

			// 노드의 데이터가 찾고 있는 값이라면
			if (node->data == _findNum)
			{
				// 함수 종료
				delete node;
				return 1;
			}

			// 그게 아니라면 스택에 오른쪽 자식부터 저장
			// 오른쪽 자식부터 저장해야 스택 자료구조의 특성 상 왼쪽이 먼저 탐색 됨
			if (node->rightChild != NULL)
				nodeStack.push(node->rightChild);
			if (node->leftChild != NULL)
				nodeStack.push(node->leftChild);
		}
		delete node;
		return 0;
	}
  ```
  


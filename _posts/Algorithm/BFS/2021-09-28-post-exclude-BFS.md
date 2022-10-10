---
title: "BFS"
classes : wide
categories:
  - Search
tags:
  - Search Algorithm
---

<br>
<h1>
- 넓이 우선 탐색 (BFS)
</h1>
<br>

- 넓이 우선 탐색

  - 탐색의 경로가 정해지지 않았을때 주변의 경로부터 하나씩 탐색하는 기법
  
  - 예를 들어 트리구조에서 어떠한 노드를 찾는다고 가정하면, 검사하는 노드의 자식을 모두 검사 후 자식의 자식을 검사해 나가는 방식
  
  - DFS가 트리구조의 그림 상에서 세로로 탐색을 진행하는 반면, BFS는 가로로 탐색함
  
  - 큐(Queue)로 쉽게 구현 가능
<br><br>

- 소스코드
    - DFS의 코드에서 스택 -> 큐 만 해주면 BFS 방식으로 작동한다.
  
  ```cpp
  int Search_Node_BFS(Node* _node, int _findNum)
	{
		queue<Node*> nodeStack;

		nodeStack.push(_node);

		Node* node = NULL;
		// 노드가 비어있지 않다면 반복 (비었을 경우는 모든 노드를 탐색했을때 뿐)
		while (!nodeStack.empty())
		{
			// 큐에서 자료를 받아옴
			node = nodeStack.front();
			nodeStack.pop();

			// 노드의 데이터가 찾고 있는 값이라면
			if (node->data == _findNum)
			{
				// 함수 종료
				delete node;
				return 1;
			}

			// 그게 아니라면 큐에 오른쪽 자식부터 저장
			if (node->leftChild != NULL)
				nodeStack.push(node->leftChild);
			if (node->rightChild != NULL)
				nodeStack.push(node->rightChild);
		}
		delete node;
		return 0;
	}
  ```
  


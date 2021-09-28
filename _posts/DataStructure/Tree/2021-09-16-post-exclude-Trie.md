---
title: "Trie"
categories:
  - Tree
tags:
  - C++
---
<br>

<h1>
- 트라이 (Trie)

  - (Degital Tree, Prefix Tree)
</h1>

<br>

- 노드 하나에 키값이 표현되는 트리와 달리 노드의 연결로 키값을 표현하는 트라이
  - ex) 
    - Tree = 1번노드('abc') 
    - Trie = 1번노드('a') -> 2번노드('b') -> 3번노드 ('c')
  
  <br>
- 트리와 구분하기위해 '트라이'라고 칭함

<br>
- 자동완성기능을 구현할때 유용하게 쓰임.
  - ex)
    - INPUT : a -> OUTPUT : abc, amazon, ... 
    - INPUT : ba -> OUTPUT : banana, base, ... 

- 직접 구현해본 트라이 구조를 이용한 자동완성 프로그램

- 1. 문자 삽입 
  - trie.Recursive_Insert_Word("ab");
  - trie.Recursive_Insert_Word("abc");
  - trie.Recursive_Insert_Word("amazon");
  - trie.Recursive_Insert_Word("alphabet");
  - trie.Recursive_Insert_Word("ba");
  - trie.Recursive_Insert_Word("b");

<br>

- 2. 검색어 입력 

  - ex) 
    - INPUT : a 
    - OUTPUT : ab, abc, amazon, alphabet
  
    - INPUT : b
    - OUTPUT : ba
    - INPUT : dada
    - OUTPUT : 


``` cpp
// Trie를 이용한 검색어 자동완성 프로그램
#include <iostream>
#include <string>
#include <vector>

using namespace std;


struct Node {
	char data;
	bool isLastWord;
};

class Trie {

	// 본인 데이터 값을 저장할 클래스 변수
	Node node;

	// 자식을 가르킬 클래스 포인터 배열 선언
	vector<Trie*> childs;
public:
	Trie()
	{
		node.data = NULL;
		node.isLastWord = false;
	}
	Trie(int _data)
	{
		node.data = _data;
		node.isLastWord = false;
	}
	~Trie()
	{
		for (int i = 0; i < childs.size(); i++)
			delete childs[i];
	}

	// 재귀적으로 문자를 트라이에 삽입하는 함수
	void Recursive_Insert_Word(string _word)
	{
		// 해당 노드와 연결된 자식 중 현재 찾는 문자열 중 앞글자가 같은 자식이 있다면

		for (int i = 0; i < childs.size(); i++)
		{
			// 찾았다면
			if (_word[0] == childs[i]->node.data)
			{
				// 현재 문자가 마지막이라면
				if (_word.length() == 1)
					childs[i]->node.isLastWord = true;
				// 검사할 문자가 2글자 이상이라면
				else
				{
					// 첫번째 문자 삭제
					_word.erase(_word.begin());


					// 남은 문자에 대해 재귀함수 호출
					childs[i]->Recursive_Insert_Word(_word);

				}

				return;
			}
		}

		// 자식 중에 없다면

		// 새로 추가해서 자식에 대입
		Trie* newChild = new Trie(_word[0]);

		// 문자열의 마지막 문자라면
		if (_word.length() == 1)
		{
			newChild->node.isLastWord = true;
		}
		// 검사할 문자가 2글자 이상이라면
		else
		{
			// 첫번쨰 문자 삭제
			_word.erase(_word.begin());

			// 남은 문자들을 자식에 넣을 new Next의 자식으로 대입
			newChild->Recursive_Insert_Word(_word);
		}
		// 자식들에 추가
		childs.push_back(newChild);
	}

	// 문자 인자값으로 넘겨주면 트라이에있는 연관 단어들을 벡터로 반환해주는 함수
	vector<string> Get_Auto_Word(string _word)
	{
		if (_word.length() > 0)
		{
			string _temp;
			vector<string> answer;
			Trie* startNode = this;

			// 관련 단어 검색을 시작할 노드 찾기.
			//	ex) 'ab' 입력시 마지막 문자인 'b' 값을 가진 노드가 StartNode
			for(int i = 0; ; i++)
			{
				// word가 트라이 내부에 없음
				if (i == startNode->childs.size())
				{
					return answer;
				}

				if (_word[0] == startNode->childs[i]->node.data)
				{
					// 같은 문자 찾음
					_temp += _word[0];
					_word.erase(_word.begin());

					startNode = startNode->childs[i];


					// 전달받은 문자열 모두가 트라이 내부에 있어야 자동완성 가능
					// ex) ab -> abc (O), ab -> a (X)
					if (_word.length() < 1)
						break;

					// 새로운 StartNode의 처음부터 다시
					i = -1;
				}

			}

			// 구한 StartNode로 자동완성 단어 찾아오기 (answer배열을 레퍼런스로 넘겨줘서 answer에 저장됨)
			Recursive_Find_Auto_Word(answer, startNode, _temp);

			// answer 리턴
			return answer;
		}
		return vector<string>();
	}
	// 재귀적으로 유사문자 찾아서 레퍼런스 배열에 저장
	void Recursive_Find_Auto_Word(vector<string>& _autoWords, Trie* _startNode, string _word)
	{
		string temp = _word;
		// 현재노드와 연결된 단어들을 모두 반환

		for (int i = 0; i < _startNode->childs.size(); i++, temp = _word)
		{
			// NULL이 아니면
			if (_startNode->childs[i] != NULL)
			{
				// 문자열에 현재 문자 더함
				temp += _startNode->childs[i]->node.data;
				// 마지막 문자라면
				if (_startNode->childs[i]->node.isLastWord)
				{
					// 레퍼런스 배열에 삽입
					_autoWords.push_back(temp);
				}

				// 연결된 단어있는지 검사
				Recursive_Find_Auto_Word(_autoWords, _startNode->childs[i], temp);
			}
		}
	}
};

int main()
{
	Trie trie;
	trie.Recursive_Insert_Word("ab");
	trie.Recursive_Insert_Word("abc");
	trie.Recursive_Insert_Word("amazon");
	trie.Recursive_Insert_Word("alphabet");
	trie.Recursive_Insert_Word("ba");
	trie.Recursive_Insert_Word("b");

	vector<string> outStr;
	string inputStr = "";
	while (1)
	{
		cin >> inputStr;
		outStr = trie.Get_Auto_Word(inputStr);
		for (int i = 0; i < outStr.size(); i++)
		{
			cout << "AutoWords : " << outStr[i] << endl;
		}
	}

	return 0;
}


```
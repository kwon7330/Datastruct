# Doubble LInked List
	- 더블링크드리스트는 싱글링크드리스트와 유사하지만 가장 큰 특징으로 Head와 Tail을 제외한 
	- 각 노드들이 다음주소와 이전주소를 알고 있다는것입니다.
	- 따라서 탐색을 할때 해드와 테일을 알고있으면 링크드 리스트보다 탐색을 하기 좋습니다.
	- 하지만 노드의 이전주소를 가리키는 포인터 변수도 선언을 해주기 때문에 메모리를 더잡아먹는 단점이 있습니다.
	
## Node.h
```
#pragma once

class Node
{
private:
	

public:
	int Data;
	Node* NextNode;
	Node* PrevNode;
	~Node();
	Node* CreateNode(int _NewData); // 새로운 노드를 만들어서 데이터를 추가한다.
	Node* DeleteNode(Node* _Node);
	void AppendNode(Node** _Head, Node* NewNode); // 새로운 노드가 노드의 뒤로오도록 하는 방식
	Node* GetNodeAt(Node* _Head, int _Location); // 노드를 탐색하여 Location에 대응하는 값을 리턴한다.
	void RemoveNode(Node** _Head, Node* _Remove); // 노드의 링크를 끊어 제거하는 함수이다.
	void InsertAfter(Node* _Current, Node* _NewNode); // 노드를 두개안에 새로운 함수를  끼우는 함수
	int GetNodeCount(Node* _Head); // 노드의 개수를 구하여 리스트의 길이를 구할수있다.
};

```
## Node.cpp
```
#include "Node.h"

Node::~Node()
{
}

Node* Node::CreateNode( int _NewData) 새로운 노드에 들어갈 데이터값을 받는다.
{
	Node* NewNode = new Node;   //  Heap 영역에 노드를 만들어 준다.
	NewNode->Data = _NewData; // 만든노드에 새로운데이터를 받아서 저장한다.
	NewNode->NextNode = nullptr; // 새롭게 만든 노드의 이전노드와 다음노드를 가리키는 포인터를 초기화한다.
	NewNode->PrevNode = nullptr;

	return NewNode;
}
Node* Node::DeleteNode(Node* _Node)
{
	delete _Node;
}

void Node::AppendNode(Node** _Head, Node* _NewNode)
{
	if (*_Head == nullptr) // head가 아무것도 가리키지 않는다면 받아온 새로운노드의 포인터가 해드 노드를 가리키게 한다.
	{
		*_Head = _NewNode;
	}
	else // head가 다음 노드를 가리킨다면
	{
		Node* Tail = (*_Head); // 노드타입 Tail 포인터 변수를 선언하고 Head의 주소를 가리키게한다.
		while (Tail->NextNode != nullptr) //그리고 다음 노드의 주소가 아무것도 안가리킬 때 까지 다음노드 포인터들을 따라가고 아무것도 안가리킨다면 Tail에 다음노드 주소를 가리키게하고
		{
			Tail = Tail->NextNode;
		}
		Tail->NextNode = _NewNode; // 테일의 다음 노드를 가리키는 포인터를 새로운노드를 가리키게한다.
		_NewNode->PrevNode = Tail; // 그리고 새로운노드는 더블링크드리스트기때문에 위의 Tail노드를 가리키도록 한다.

	}
}

Node* Node::GetNodeAt(Node* _Head, int Location)
{
	Node* Current = _Head; // 탐색할 노드를 선언해주고 노드의 처음이 되게 Head값을 넣어준다.
	while (Current != nullptr && (--Location) >= 0) // 탐색중인 현재 노드에 다음 노드가 있거나, 입력받은 몇번쨰가 0까지 계속해서
	{
		Current = Current->NextNode; // 현재 노드에 다음 노드를 가리키게 한다.
	}
	return Current; // 반복문을 빠져 나왔다는것은 Current가 입력받은 번째의 노드를 찾았기 때문에 리턴해준다.
}

void Node::RemoveNode(Node** _Head,Node* _Remove)
{
	
	if (*_Head == _Remove) // 제거하는것이 맨앞 노드이면
	{
		*_Head = _Remove->NextNode; // 제거한 노드의 다음 즉 맨앞 노드의 다음 노드를 가리키는 노드를 넘기고
			if ((*_Head) != nullptr) // 만약 아무것도 안가리키면 
			{
				(*_Head)->PrevNode = nullptr; // 앞함수의 이전 함수를 가리키는 함수를 초기화하고
				_Remove -> NextNode = nullptr; // 제거한 노드의 다음을 가리키는 함수를 초기화하고
				_Remove->PrevNode = nullptr; // 제거한 노드의 이전을 가리키는 함수를 초기화한다.
			}
	}
	else
	{
		Node* Temp = _Remove; // 노드타입에 템프라는 제거 노드를 만들어서
		if (_Remove->PrevNode != nullptr) // 제거하는 노드가 이전노드를 가리킨다면
			_Remove->NextNode->PrevNode = Temp->NextNode; // 제거하는 노드의 다음노드의 이전노드를 가리키는것에 제거할 노드의 다음노드 포인터를 가리키게하고
		if (_Remove->NextNode != nullptr) // 제거하는 노드가 다음노드를 가리킨다면
		{
			_Remove->NextNode->PrevNode = Temp->PrevNode; // 제거하는 노드의 다음노드의 이전노드를 가리키는 것을 템프를 가리키게한다.
		}
		_Remove->PrevNode = nullptr; // 제거한 노드의 앞노드 주소 는 아무것도 가리키지 않게
		_Remove->NextNode = nullptr; // 제거한 노드의 뒷노드 주소 도 아무것도 가리키지 않게
	}
	
}

void Node::InsertAfter(Node* _Current, Node* _NewNode) // 현재 노드의 주소와 새로운 노드의 주소를 입력받는다.
{
	_NewNode->NextNode = _Current->NextNode; // 들어올 노드의 다음노드를 가리키는 포인터가 현재 노드의 다음 노드를 가리키게하고
	_NewNode->PrevNode = _Current; // 새로운노드의 이전노드에서 현재 노드를 가리키게한다.

	if (_Current->NextNode != nullptr) // 현재노드가 다음노드를 가리키면
	{
		_Current-> NextNode -> PrevNode = _NewNode; // 현재 노드의 다음노드의 이전을 가리키는 포인터를  새로운 노드를 가리키게한다. 
		_Current->NextNode = _NewNode;  // 현재노드의 다음에 새로운 노드를 가리키게 한다.
	}
}

int Node::GetNodeCount(Node* _Head) // 리스트의 길이를 구하기위해 가장앞 노드의 주소를 받는다.
{
	unsigned int Count = 0; // 개수는 음수로 떨어지지 않으므로 언싸인인트로 선언하고 0으로 초기화한다.
	Node* Current = _Head; //  리스트의 현재를 가리키는 노드를 선언하고 가장앞인 해드노드로 초기화한다.

	while (Current != nullptr) // 노드가 1개 이상일떄
	{
		Current = Current->NextNode; // 현재노드가 다음노드를 가리키게하고
		++Count; // 개수를 하나씩 추가하여 
	}
	return Count;

}






```

## Main.cpp

```
#include <iostream>
#include "Node.h"


int main()
{

    int Count = 0; // 리스트 의 길이를 위한 노드의 개수를 샐 Count변수를 선언하여 0으로 초기화한다.
    Node* List = nullptr;  // 노드들을 연결할 리스트를 선언하였다.
    Node* NewNode = nullptr; // 새로운 노드를 생성하는 변수를 선언하여 아무것도 안가리키게 초기화
    Node* Current = nullptr; // 탐색할 현재 노드를 변수로 선언하여 아무것도 안가리키게 초기화.
    
    for (int i = 0; i < 5; ++i)  // 노드 5개를 만들어서 노드의 뒤에 다음노드가 오도록 리스트를 짠다.
    {
        NewNode->CreateNode(i);
        List->AppendNode(&List, NewNode);
       
    }
    Count = List->GetNodeCount(List); // 리스트길이를 개수함수를 이용해서 Count변수에 담아주고
    for (int i = 0; i < Count; ++i)
    {
        Current = List->GetNodeAt(List, i); // 리스트 하나하나를 Current 변수에담아서
        std::cout << i << " " << Current->Data; // 출력해준다.
    }
    

    for (int i = 0; i < Count; i++) // 더블링크드리스트 안에서
    {
        Current = List->GetNodeAt(List, 0); // 현재노드를 가장앞노드로 선택해서
        if (Current != nullptr) //  다음노드가 있을시 
        {
            List->RemoveNode(&List, Current); // 연결을 끊고
            List->DeleteNode(Current); // 연결이 끊긴 노드들을 모두 삭제해버린다.
        }
    }
	// ~Node();
    return 0;
}


```
```
#pragma once


struct Node
{
	int Paper;
	Node* pPreveNode;
	Node* pNextNode;
	Node()
		: Paper()
		, pNextNode(nullptr)
		, pPreveNode(nullptr)
	{}
};

class List
{
private:
	int Count;
	Node* pHead;
	Node* pTail;
	int Count;
public:
	List();
	~List();
	void PushBack(int _Data);
	void Remove(Node* _RemoveNode);
	int ListLength();
};
List::List()
	:pHead(nullptr)
	, pTail(nullptr)
	, Count(0)
{}
List::~List()
{
	Node* pDeleteNode = pHead;
	while (pDeleteNode)
	{
		Node* pNext = pDeleteNode->pNextNode;
		delete(pDeleteNode);
		pDeleteNode = pNext;
	}
}
void List :: PushBack(int _Data) // 노드를 만들어서 
{
	Node* pNewNode = new Node; 
	if (pHead == nullptr) //// 노드가 하나인 경우
	{
		pHead = pNewNode;
		pTail = pNewNode;
	}
	else // 데이터가 하나 이상일경우 , 현재 가장 마지막 데이터(Tail)을 저장하고 있는노드와 새로 생성된 노드가 서로 가리키게한다.
	{
		// 리스트가 마지막 노드의 주소값을 새로 입력된 노드로 갱신한다.
		pTail->pNextNode = pNewNode;
		pNewNode->pPreveNode = pTail;
		pTail = pNewNode;
	}
	++Count; //데이터 개수 증가
}
void List :: Remove(Node* _RemoveNode)
{
	if(pHead == nullptr)
	if (pHead == _RemoveNode)
	{
		pHead = _RemoveNode ->pNextNode;
		pHead->pPreveNode = nullptr;
		if (pHead == nullptr) pTail = nullptr;
	}
	else if (pTail == _RemoveNode)
	{
		pTail = pTail->pPreveNode;
		pTail->pNextNode = nullptr;
	}
	else
	{
		_RemoveNode->pPreveNode->pNextNode = _RemoveNode->pNextNode;
		_RemoveNode->pNextNode->pPreveNode = _RemoveNode->pPreveNode;
	}
}
int List::ListLength() // 풍선 갯수
{
	return Count;
}ㅍ
```

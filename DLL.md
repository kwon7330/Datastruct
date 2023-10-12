# Doubble LInked List
	- ����ũ�帮��Ʈ�� �̱۸�ũ�帮��Ʈ�� ���������� ���� ū Ư¡���� Head�� Tail�� ������ 
	- �� ������ �����ּҿ� �����ּҸ� �˰� �ִٴ°��Դϴ�.
	- ���� Ž���� �Ҷ� �ص�� ������ �˰������� ��ũ�� ����Ʈ���� Ž���� �ϱ� �����ϴ�.
	- ������ ����� �����ּҸ� ����Ű�� ������ ������ ������ ���ֱ� ������ �޸𸮸� ����ƸԴ� ������ �ֽ��ϴ�.
	
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
	Node* CreateNode(int _NewData); // ���ο� ��带 ���� �����͸� �߰��Ѵ�.
	Node* DeleteNode(Node* _Node);
	void AppendNode(Node** _Head, Node* NewNode); // ���ο� ��尡 ����� �ڷο����� �ϴ� ���
	Node* GetNodeAt(Node* _Head, int _Location); // ��带 Ž���Ͽ� Location�� �����ϴ� ���� �����Ѵ�.
	void RemoveNode(Node** _Head, Node* _Remove); // ����� ��ũ�� ���� �����ϴ� �Լ��̴�.
	void InsertAfter(Node* _Current, Node* _NewNode); // ��带 �ΰ��ȿ� ���ο� �Լ���  ����� �Լ�
	int GetNodeCount(Node* _Head); // ����� ������ ���Ͽ� ����Ʈ�� ���̸� ���Ҽ��ִ�.
};

```
## Node.cpp
```
#include "Node.h"

Node::~Node()
{
}

Node* Node::CreateNode( int _NewData) ���ο� ��忡 �� �����Ͱ��� �޴´�.
{
	Node* NewNode = new Node;   //  Heap ������ ��带 ����� �ش�.
	NewNode->Data = _NewData; // �����忡 ���ο���͸� �޾Ƽ� �����Ѵ�.
	NewNode->NextNode = nullptr; // ���Ӱ� ���� ����� �������� ������带 ����Ű�� �����͸� �ʱ�ȭ�Ѵ�.
	NewNode->PrevNode = nullptr;

	return NewNode;
}
Node* Node::DeleteNode(Node* _Node)
{
	delete _Node;
}

void Node::AppendNode(Node** _Head, Node* _NewNode)
{
	if (*_Head == nullptr) // head�� �ƹ��͵� ����Ű�� �ʴ´ٸ� �޾ƿ� ���ο����� �����Ͱ� �ص� ��带 ����Ű�� �Ѵ�.
	{
		*_Head = _NewNode;
	}
	else // head�� ���� ��带 ����Ų�ٸ�
	{
		Node* Tail = (*_Head); // ���Ÿ�� Tail ������ ������ �����ϰ� Head�� �ּҸ� ����Ű���Ѵ�.
		while (Tail->NextNode != nullptr) //�׸��� ���� ����� �ּҰ� �ƹ��͵� �Ȱ���ų �� ���� ������� �����͵��� ���󰡰� �ƹ��͵� �Ȱ���Ų�ٸ� Tail�� ������� �ּҸ� ����Ű���ϰ�
		{
			Tail = Tail->NextNode;
		}
		Tail->NextNode = _NewNode; // ������ ���� ��带 ����Ű�� �����͸� ���ο��带 ����Ű���Ѵ�.
		_NewNode->PrevNode = Tail; // �׸��� ���ο���� ����ũ�帮��Ʈ�⶧���� ���� Tail��带 ����Ű���� �Ѵ�.

	}
}

Node* Node::GetNodeAt(Node* _Head, int Location)
{
	Node* Current = _Head; // Ž���� ��带 �������ְ� ����� ó���� �ǰ� Head���� �־��ش�.
	while (Current != nullptr && (--Location) >= 0) // Ž������ ���� ��忡 ���� ��尡 �ְų�, �Է¹��� ������� 0���� ����ؼ�
	{
		Current = Current->NextNode; // ���� ��忡 ���� ��带 ����Ű�� �Ѵ�.
	}
	return Current; // �ݺ����� ���� ���Դٴ°��� Current�� �Է¹��� ��°�� ��带 ã�ұ� ������ �������ش�.
}

void Node::RemoveNode(Node** _Head,Node* _Remove)
{
	
	if (*_Head == _Remove) // �����ϴ°��� �Ǿ� ����̸�
	{
		*_Head = _Remove->NextNode; // ������ ����� ���� �� �Ǿ� ����� ���� ��带 ����Ű�� ��带 �ѱ��
			if ((*_Head) != nullptr) // ���� �ƹ��͵� �Ȱ���Ű�� 
			{
				(*_Head)->PrevNode = nullptr; // ���Լ��� ���� �Լ��� ����Ű�� �Լ��� �ʱ�ȭ�ϰ�
				_Remove -> NextNode = nullptr; // ������ ����� ������ ����Ű�� �Լ��� �ʱ�ȭ�ϰ�
				_Remove->PrevNode = nullptr; // ������ ����� ������ ����Ű�� �Լ��� �ʱ�ȭ�Ѵ�.
			}
	}
	else
	{
		Node* Temp = _Remove; // ���Ÿ�Կ� ������� ���� ��带 ����
		if (_Remove->PrevNode != nullptr) // �����ϴ� ��尡 ������带 ����Ų�ٸ�
			_Remove->NextNode->PrevNode = Temp->NextNode; // �����ϴ� ����� ��������� ������带 ����Ű�°Ϳ� ������ ����� ������� �����͸� ����Ű���ϰ�
		if (_Remove->NextNode != nullptr) // �����ϴ� ��尡 ������带 ����Ų�ٸ�
		{
			_Remove->NextNode->PrevNode = Temp->PrevNode; // �����ϴ� ����� ��������� ������带 ����Ű�� ���� ������ ����Ű���Ѵ�.
		}
		_Remove->PrevNode = nullptr; // ������ ����� �ճ�� �ּ� �� �ƹ��͵� ����Ű�� �ʰ�
		_Remove->NextNode = nullptr; // ������ ����� �޳�� �ּ� �� �ƹ��͵� ����Ű�� �ʰ�
	}
	
}

void Node::InsertAfter(Node* _Current, Node* _NewNode) // ���� ����� �ּҿ� ���ο� ����� �ּҸ� �Է¹޴´�.
{
	_NewNode->NextNode = _Current->NextNode; // ���� ����� ������带 ����Ű�� �����Ͱ� ���� ����� ���� ��带 ����Ű���ϰ�
	_NewNode->PrevNode = _Current; // ���ο����� ������忡�� ���� ��带 ����Ű���Ѵ�.

	if (_Current->NextNode != nullptr) // �����尡 ������带 ����Ű��
	{
		_Current-> NextNode -> PrevNode = _NewNode; // ���� ����� ��������� ������ ����Ű�� �����͸�  ���ο� ��带 ����Ű���Ѵ�. 
		_Current->NextNode = _NewNode;  // �������� ������ ���ο� ��带 ����Ű�� �Ѵ�.
	}
}

int Node::GetNodeCount(Node* _Head) // ����Ʈ�� ���̸� ���ϱ����� ����� ����� �ּҸ� �޴´�.
{
	unsigned int Count = 0; // ������ ������ �������� �����Ƿ� �������Ʈ�� �����ϰ� 0���� �ʱ�ȭ�Ѵ�.
	Node* Current = _Head; //  ����Ʈ�� ���縦 ����Ű�� ��带 �����ϰ� ������� �ص���� �ʱ�ȭ�Ѵ�.

	while (Current != nullptr) // ��尡 1�� �̻��ϋ�
	{
		Current = Current->NextNode; // �����尡 ������带 ����Ű���ϰ�
		++Count; // ������ �ϳ��� �߰��Ͽ� 
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

    int Count = 0; // ����Ʈ �� ���̸� ���� ����� ������ �� Count������ �����Ͽ� 0���� �ʱ�ȭ�Ѵ�.
    Node* List = nullptr;  // ������ ������ ����Ʈ�� �����Ͽ���.
    Node* NewNode = nullptr; // ���ο� ��带 �����ϴ� ������ �����Ͽ� �ƹ��͵� �Ȱ���Ű�� �ʱ�ȭ
    Node* Current = nullptr; // Ž���� ���� ��带 ������ �����Ͽ� �ƹ��͵� �Ȱ���Ű�� �ʱ�ȭ.
    
    for (int i = 0; i < 5; ++i)  // ��� 5���� ���� ����� �ڿ� ������尡 ������ ����Ʈ�� §��.
    {
        NewNode->CreateNode(i);
        List->AppendNode(&List, NewNode);
       
    }
    Count = List->GetNodeCount(List); // ����Ʈ���̸� �����Լ��� �̿��ؼ� Count������ ����ְ�
    for (int i = 0; i < Count; ++i)
    {
        Current = List->GetNodeAt(List, i); // ����Ʈ �ϳ��ϳ��� Current ��������Ƽ�
        std::cout << i << " " << Current->Data; // ������ش�.
    }
    

    for (int i = 0; i < Count; i++) // ����ũ�帮��Ʈ �ȿ���
    {
        Current = List->GetNodeAt(List, 0); // �����带 ����ճ��� �����ؼ�
        if (Current != nullptr) //  ������尡 ������ 
        {
            List->RemoveNode(&List, Current); // ������ ����
            List->DeleteNode(Current); // ������ ���� ������ ��� �����ع�����.
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
void List :: PushBack(int _Data) // ��带 ���� 
{
	Node* pNewNode = new Node; 
	if (pHead == nullptr) //// ��尡 �ϳ��� ���
	{
		pHead = pNewNode;
		pTail = pNewNode;
	}
	else // �����Ͱ� �ϳ� �̻��ϰ�� , ���� ���� ������ ������(Tail)�� �����ϰ� �ִ³��� ���� ������ ��尡 ���� ����Ű���Ѵ�.
	{
		// ����Ʈ�� ������ ����� �ּҰ��� ���� �Էµ� ���� �����Ѵ�.
		pTail->pNextNode = pNewNode;
		pNewNode->pPreveNode = pTail;
		pTail = pNewNode;
	}
	++Count; //������ ���� ����
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
int List::ListLength() // ǳ�� ����
{
	return Count;
}��
```

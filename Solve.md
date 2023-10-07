# 요세푸스 문제 풀이 (오답입니다.)

## Node.h
```
#pragma once
class Node
{

public:
	
	int Data;
	Node* NextNode;

	Node();
	~Node();
	Node* CreateNode(int _Data);
	Node* Find(Node* _Head, int _K);
	void Remove(Node** _Head, Node* _Remove);

};


```
## Node.cpp
```
#include "Node.h"

Node::Node()
{
}

Node::~Node()
{
}

Node* Node::CreateNode(int _Data)
{
	Node* NewNode = new Node;
	NewNode->NextNode = nullptr;
	NewNode->Data = _Data;
	return NewNode;
}

Node* Node::Find(Node* _Head, int _K)
{
	Node* Current = _Head;
	while (Current != nullptr && (--_K) >= 0)
	{
		Current = Current->NextNode;
	}

	return Current;
}

void Node::Remove(Node** _Head, Node* _Remove)
{
	if (*_Head == nullptr)
	{
		*_Head == _Remove->NextNode;
	}
	else
	{
		Node* Current = *_Head;
		while (Current != nullptr && Current->NextNode != _Remove)
		{
			Current = Current->NextNode;
		}
		if (Current != nullptr)
		{
			Current->NextNode = _Remove->NextNode;
		}
	}
}



```
## main
```
#include <iostream>
#include <string>
#include "Node.h"

using namespace std;

int main() 
{   
    int N, K;
    int FindNumber = 0;
    cin >> N >> K;
    Node List;
    Node* MyNode;
    
    for (int i = 1; i = K; ++i)
    {
        List.CreateNode(i);
    }
    
    MyNode = List.Find(&List, 1);
    for (K = N - 1; K >= 1; --K)
    {
       
      List.Remove(&MyNode, List.Find(&List, K));
        
    }
    
    List.~Node();
    
    
    
    return 0;
}
```


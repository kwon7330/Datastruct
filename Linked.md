# Linked Queue

```
#include "ioStream"
using namespace std;

class Node // Node 생성
{
public:
	int Data;
	Node* pNextNode;
	Node() : Data(0), pNextNode(nullptr) {}
};
class LQueue //Linked Queue 생성
{
	Node* Front; 
	Node* Rear;
	int Count;
public:
	LQueue() : Front(nullptr), Rear(nullptr), Count(0){} //초기화
	~LQueue(){}
	bool IsEmpty() // LinkedQueue가 비어있다면
	{
		return(Front == nullptr); // 앞을 가리키는 포인터 Front가 아무것도 가리키지 않으면 아무것도 없는것
	}
	void Enqueue(int _Data) // 
	{
		Node* pNewNode = new Node; // 새로운 노드를 추가해서
		pNewNode ->Data = _Data; // 새로운 노드의 Data에 매개변수로 받은 _Data를 집어 넣어준다.
		pNewNode ->pNextNode = nullptr; // 그리고 새로들어온 노드의 다음노든 nullptr로 초기화
	
		if (IsEmpty()) // 만약 Queue가 비어 있다면
		{
			Front = pNewNode;  // Front와 Rear를 새로운 노드를 가리키게한다.
			Rear = pNewNode;
		}
		else // 하나라도 있다면
		{
			Rear->pNextNode = pNewNode; // 원래 있던 Rear다음 노드를 가리키는 포인터를 새로운 노드로 변경
			Rear = pNewNode; // 그리고 Rear가 새로운 노드를 가리키게한다.
		}
		Count ++;
	}
	int Dequeue()
	{
		Node* pRemoveNode; // 제거할 노드 포인터 선언
		int Data; // 제거할 노드의 데이터를 보관할 변수 선언
		if (IsEmpty()) 
		{
			cout << "IsEmpty" << "\n";
		}
	
		else
		{
			pRemoveNode = Front; // 제거할 노드를 Front가 가리키는 노드로 설정하고
			Data = pRemoveNode -> Data; // 그 노드의 데이터를 보관해논다음
			Front = pRemoveNode -> pNextNode; // Front가 제거한노드가 가리키던 곳을 가리키게한다.
			
			if(Front == nullptr) 
			{
				Rear == nullptr;
			}
			delete pRemoveNode; // 제거한 노드를 Heap에서 지워준다.
			Count --;
			return Data;
		}
	}
	void PrintLQueue()
	{
		Node* i;
		for (i = Front; i != nullptr; i = i->pNextNode)
		{
			cout << i->Data << " " << "\n";
		}
	}
	int Size()
	{
		return Count;
	}

};

int main()
{
	LQueue Queue;
	Queue.Enqueue(1);
	Queue.Enqueue(2);
	Queue.Enqueue(3);
	Queue.Enqueue(4);
	Queue.Enqueue(5);
	Queue.Dequeue();
	Queue.Dequeue();
	
	
	Queue.PrintLQueue();
	cout << Queue.Size() << "\n";

}
```
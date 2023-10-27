# Linked Queue

```
#include "ioStream"
using namespace std;

class Node // Node ����
{
public:
	int Data;
	Node* pNextNode;
	Node() : Data(0), pNextNode(nullptr) {}
};
class LQueue //Linked Queue ����
{
	Node* Front; 
	Node* Rear;
	int Count;
public:
	LQueue() : Front(nullptr), Rear(nullptr), Count(0){} //�ʱ�ȭ
	~LQueue(){}
	bool IsEmpty() // LinkedQueue�� ����ִٸ�
	{
		return(Front == nullptr); // ���� ����Ű�� ������ Front�� �ƹ��͵� ����Ű�� ������ �ƹ��͵� ���°�
	}
	void Enqueue(int _Data) // 
	{
		Node* pNewNode = new Node; // ���ο� ��带 �߰��ؼ�
		pNewNode ->Data = _Data; // ���ο� ����� Data�� �Ű������� ���� _Data�� ���� �־��ش�.
		pNewNode ->pNextNode = nullptr; // �׸��� ���ε��� ����� ������� nullptr�� �ʱ�ȭ
	
		if (IsEmpty()) // ���� Queue�� ��� �ִٸ�
		{
			Front = pNewNode;  // Front�� Rear�� ���ο� ��带 ����Ű���Ѵ�.
			Rear = pNewNode;
		}
		else // �ϳ��� �ִٸ�
		{
			Rear->pNextNode = pNewNode; // ���� �ִ� Rear���� ��带 ����Ű�� �����͸� ���ο� ���� ����
			Rear = pNewNode; // �׸��� Rear�� ���ο� ��带 ����Ű���Ѵ�.
		}
		Count ++;
	}
	int Dequeue()
	{
		Node* pRemoveNode; // ������ ��� ������ ����
		int Data; // ������ ����� �����͸� ������ ���� ����
		if (IsEmpty()) 
		{
			cout << "IsEmpty" << "\n";
		}
	
		else
		{
			pRemoveNode = Front; // ������ ��带 Front�� ����Ű�� ���� �����ϰ�
			Data = pRemoveNode -> Data; // �� ����� �����͸� �����س����
			Front = pRemoveNode -> pNextNode; // Front�� �����ѳ�尡 ����Ű�� ���� ����Ű���Ѵ�.
			
			if(Front == nullptr) 
			{
				Rear == nullptr;
			}
			delete pRemoveNode; // ������ ��带 Heap���� �����ش�.
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
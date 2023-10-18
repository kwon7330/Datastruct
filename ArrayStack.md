# ���� ���� Ǯ��
```
#include <iostream>
#include <assert.h>
using namespace std;

class ArrayStack
{
private :
	int Capacity;
	int Top;
	int* Arr;
public:
	ArrayStack(int _Capascity) // ������
	{
		Top = -1; // �迭�� ���� ���κ� -1�������� �ε��� ��ȣ-1�� ���̱� ����
		Capacity = _Capascity; // �迭�� ũ��
		Arr = new int[Capacity]; // �迭����
	}
	~ArrayStack() // �Ҹ���
	{
		delete[] Arr; // �迭�� �����.
	}
	int IsEmpty() // �迭�� ��� �ִ°�?
	{
		return (Top == -1); // Top�� -1�ΰ�� �ƹ��͵� ���� ���̱� ������ �����Ѵ�.
	}
	int IsFull() // �迭�� ���� �� �ִ°�?
	{
		return(Top + 1 == Capacity); //
	}
	int Push(int _Value) // ���ù迭�ȿ� ���� �߰��Ѵ�.
	{
		if (IsFull()) // ���� ���� ���ִٸ� 
		{
			exit(EXIT_FAILURE); // ���� ����
		}
		Arr[Top++] = _Value; // Top�� �ϳ��÷��ְ� ������ ���� �ִ´�.
	}
	int Peek() // �迭������ ������ ���� ��ȯ�Ѵ�. 
	{
		if (IsEmpty()) // ���� �迭�� ���������
		{
			exit(EXIT_FAILURE); // ���� �����Ų��.
		}
		else return Arr[Top];
	}
	int Pop() // ������ ������ ���� ��ȯ�ϰ� ����
	{
		if (IsEmpty())
		{
			exit(EXIT_FAILURE);

		}
		Peek();
		return Arr[Top--]; // ���� �Ǿ����Ƿ� �ϳ����δ�.
	}
	int Capacityy()
	{
		return Top;
	}
};


int main()
{
	int K, Number, ToTal=0;
	cin >> K;
	ArrayStack Stk(K);
	for (int i = 0; i < K; i++)
	{
		cin >> Number;
		
		if (Number == 0)
		{
			Stk.Pop();
		}
		else Stk.Push(Number);
	}
	for (int i = 0; i < Stk.Capacityy();  i++)
	{
		ToTal += Stk.Peek();
	}
	cout << ToTal << "\n";

	
	return 0;




   
}


```

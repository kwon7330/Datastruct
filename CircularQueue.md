# Circular Queue
```
#include <iostream>
using namespace std;


class CircularQueue
{
public:
	int* Arr;s
	int Front;
	int Rear;
	int Capacity;
public:
	CircularQueue(int _Capacity)
	{
		int Front = 0;
		int Rear = 0;
		Capacity = _Capacity + 1;
		Arr = new int[Capacity];
	}
	~CircularQueue()
	{
		delete[] Arr;
	}
	bool IsEmpty()
	{
		if (Front == Rear) return true;
		
		else
		return false;
	}
	bool IsFull()
	{
		if (Front == (Rear + 1) % Capacity)
			return true;
		else
		return false;
	}
	void EnQueue(int _Data)
	{
		if (IsFull())
		{
			cout << "ISFULL" << "\n";
		}

		Rear = ++Rear % Capacity;
		Arr[Rear] = _Data;

	}
	int DeQueue()
	{
		if (!IsEmpty())
			return Arr[++Front % Capacity];
		
		return -1;
	}
};

int main()
{

	/*CircularQueue Queue(100);
	
	Queue.EnQueue(1);
	Queue.EnQueue(2);
	Queue.EnQueue(3);
	cout << Queue.DeQueue();
	cout << Queue.DeQueue();*/

	int N, Temp = 0;
	cin >> N;
	CircularQueue Queue(N);
	for (int i = 0; i < N; i++)
	{
		Queue.EnQueue(N);
		
		// ÀÎµ¦½º ¹øÈ£°¡ È¦¼ö ÀÏ¶§
		if(i%2 == 1)
		Queue.DeQueue();

		// ÀÎµ¦½º ¹øÈ£°¡ Â¦¼ö ÀÏ¶§
		if(i%2 == 0)
		Temp = Queue.DeQueue();
		Queue.EnQueue(Temp);
	}
	

}
```
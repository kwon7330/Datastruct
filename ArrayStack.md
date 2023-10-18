# 제로 문제 풀이
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
	ArrayStack(int _Capascity) // 생성자
	{
		Top = -1; // 배열의 가장 윗부분 -1일이유는 인덱스 번호-1의 값이기 때문
		Capacity = _Capascity; // 배열의 크기
		Arr = new int[Capacity]; // 배열생성
	}
	~ArrayStack() // 소멸자
	{
		delete[] Arr; // 배열을 지운다.
	}
	int IsEmpty() // 배열이 비어 있는가?
	{
		return (Top == -1); // Top이 -1인경우 아무것도 없는 것이기 때문에 리턴한다.
	}
	int IsFull() // 배열이 가득 차 있는가?
	{
		return(Top + 1 == Capacity); //
	}
	int Push(int _Value) // 스택배열안에 값을 추가한다.
	{
		if (IsFull()) // 만약 가득 차있다면 
		{
			exit(EXIT_FAILURE); // 강제 종료
		}
		Arr[Top++] = _Value; // Top을 하나올려주고 해준후 값을 넣는다.
	}
	int Peek() // 배열스택의 마지막 값을 반환한다. 
	{
		if (IsEmpty()) // 만약 배열이 비어있으면
		{
			exit(EXIT_FAILURE); // 강제 종료시킨다.
		}
		else return Arr[Top];
	}
	int Pop() // 스택의 마지막 값을 반환하고 삭제
	{
		if (IsEmpty())
		{
			exit(EXIT_FAILURE);

		}
		Peek();
		return Arr[Top--]; // 삭제 되었으므로 하나줄인다.
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

## 虚函数实现原理

C++中的虚函数的作用主要是实现了多态的机制。带有virtual关键字的类其中会有个vbpr指针，指向真正的函数体。

```c++
#include <iostream>

class CBase
{
public:
	virtual void funcV() 
	{
		std::cout << "CBase::funcV" << std::endl;
	}
};

typedef void(*Func)(void);

int main()
{
	CBase BaseTest;

	std::cout << "Virtural table address: " << (int*)(&BaseTest)<< std::endl;//int* 转换为16进制整数地址
	std::cout << "Virtural table - 1st virtural func: " <<  (int*)*(int*)(&BaseTest) << std::endl; //虚表地址解引用然后转为地址
	Func pFunc =  (Func)*((int*)*(int*)(&BaseTest)); //虚函数地址解引用然后强制抓换为Func指针
	pFunc();
	return 0;
}
```

## 代码
```c++
#include <iostream>
using namespace std;

class TEST
{
public:
	TEST(int _r, int& _ref):range(_r), refer(_ref){}

	void printVar() const;
	void printVar();
	void printVar2() const ;
	void printVar3();
private:
	const int range;
	int &refer;
};

void TEST::printVar() const
{
	cout << "const printVar range:" << range << " refer:" << refer << endl; 
}

void TEST::printVar()
{
	cout << " printVar range:" << range << " refer:" << refer << endl; 
}

void TEST::printVar2() const 
{
	cout << " printVar2"<< endl;
}

void TEST::printVar3()
{
	cout << " printVar3"<< endl;
}

int main()
{
	int a = 5, b = 6;
	const TEST A(a, b);
	TEST B(a, b);
	
	A.printVar(); 
	B.printVar();
	
	A.printVar2();
	B.printVar2();
	
//	A.printVar3(); // error
	B.printVar3();
}
```
## 输出：
```C++
const printVar range:5 refer:6
printVar range:5 refer:6
printVar2
printVar2
printVar3
```
## 总结：
const 实例***只能***调用***const成员函数***
非const实例***既能***调用const成员函数，***也能***调用非const成员函数
***const成员变量***和***引用成员变量***都***只能***通过构造函数参数列表初始化
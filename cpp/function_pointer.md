## 背景：

在类A里有一个函数A::doSomething，需要选择使用A::Encrypt或者A::Decrypt两者中的一个，所以想使用函数指针来实现

```C++
Class A
{
	void doSomething(int a, BOOL (*CRYPT)(int a, char* p));
	void Encrypt(int a, char *p);
	void Decrypt(int a, char *p);
};


void A::doSomething(int a, BOOL (*CRYPT)(int a, char *p))
{
	char *pc;
	....
    CRYPT(3, pc);
}

```
如果使用上面的方式不能调用Decrypt或者Encrypt函数因为对于C++类使用thiscall的方式调用函数，也就是说，实际上对于Encrypt来说，实际参数列表如下
```
void Encrypt(A& this, int a, char *p);
```
所以Encrypt的参数列表和doSomething的函数指针的参数列表显然不一样。

## 解决方法：
```C++
Class A
{
	void doSomething(int a, BOOL (A::*CRYPT)(int a, char* p));
	void Encrypt(int a, char *p);
	void Decrypt(int a, char *p);
};


void A::doSomething(int a, BOOL (A::*CRYPT)(int a, char *p))
{
	char *pc;
	....
    //不能直接调用  
    //CRYPT(3,pc);
    (this->CRYPT)(3, pc);
}

调用doSomething时需要用如下的方式
doSomething(3， &A::Encrypt);//引用符号和所属类不能丢
```
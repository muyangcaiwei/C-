```c++
class base
{
public:
	virtual void f(){}
	virtual void g(){}
};

class derived1 : virtual public base
{
public:
	virtual void f(){}
	virtual void h(){}
};

class derived2 : virtual public base
{
public:
	virtual void f(){}
	virtual void i(){}
};

```
已知上述三个类base ， derived1，derived2，问：
```c++
class Derived   size(28):
        +---
 0      | {vfptr}
 4      | {vbptr}
        +---
        +--- (virtual base base)
 8      | {vfptr}
        +---
        +--- (virtual base derived1)
12      | {vfptr}
16      | {vbptr}
        +---
        +--- (virtual base derived2)
20      | {vfptr}
24      | {vbptr}
        +---
```

### 1.该内存布局对应的Derived类
```c++
  class Derived:virtual public derived1, virtual public derived2
  {
  public:
  		virtual void f(){}    
  }
```
```c++
class Derived   size(20):
        +---
        | +--- (base class derived2)
 0      | | {vfptr}
 4      | | {vbptr}
        | +---
        +---
        +--- (virtual base base)
 8      | {vfptr}
        +---
        +--- (virtual base derived1)
12      | {vfptr}
16      | {vbptr}
        +---
```
### 2.该内存布局对应的Derived类
```c++
  class Derived:virtual public derived1, public derived2
  {
  public:
  		virtual void f(){}    
  }
```

```c++
class Derived   size(20):
        +---
        | +--- (base class derived1)
 0      | | {vfptr}
 4      | | {vbptr}
        | +---
        | +--- (base class derived2)
 8      | | {vfptr}
12      | | {vbptr}
        | +---
        +---
        +--- (virtual base base)
16      | {vfptr}
        +---
```
### 3.该内存布局对应的Derived类
```c++
  class Derived: public derived1, public derived2
  {
  public:
  		virtual void f(){}    
  }
```

### 4总结
C++继承过程中，非虚继承的类在所占的内存在低地址位置，虚继承的类在内存的高地址地方；当全部为虚拟继承时，类才有虚基指针。***虚基类总是先于非虚基类构造***，

### 5.虚函数指针
例如3中Derived类的结构所示，类Derived有**两**个虚函数指针，分别指向derived1，derived2的虚函数表，Derived的虚函数追加到derived1虚表的最后。

如果基类的虚函数是private或者protected的，但是这些非public的虚函数仍然存在于虚函数表中，所以可以通过指针访问虚函数表的方式访问这些non-public的虚函数。
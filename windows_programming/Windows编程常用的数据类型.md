# Windows编程常用的数据类型

```C++
引入头文件 Windows.h

WORD：16位无符号整形数据 
SHORT：无符号短整型（16位） 
DWORD：32位无符号整型数据（DWORD32）  	unsigned int
DWORD64：64位无符号整型数据 
INT：32位有符号整型数据类型 		   int
INT32：32位符号整型 
int64：64位符号整型 
LONG：32位符号整型（LONG32） 
ULONG：无符号LONG 
LONGLONG：64位符号整型（LONG64） 
UINT：无符号INT

INT_PTR：指向INT数据类型的指针类型     int *
PVOID:普通指针
VOID：无类型，相当于标准C语言中的void 

FLOAT：浮点数据类型 

LPSTR：字符指针，也就是字符串变量    
LPCSTR：字符串常量 
LPCTSTR：根据环境配置，如果定义了UNICODE宏，则是LPCWSTR类型，否则则为LPCSTR类型 
LPCWSTR：UNICODE字符串常量 
LPDWORD：指向DWORD类型数据的指针 

BYTE：字节类型（8位） 
CHAR：8比特字节 
TCHAR：如果定义了UNICODE，则为WCHAR，否则为CHAR 
UCHAR：无符号CHAR 
WCHAR：16位Unicode字符 

BOOL：布尔型变量 
CONST：常量 
SIZE_T：表示内存大小，以字节为单位，其最大值是CPU最大寻址范围 

LPARAM：消息的L参数 
WPARAM：消息的W参数 
HANDLE：对象的句柄，最基本的句柄类型，其实就是 void*
HICON：图标的句柄 
HINSTANCE：程序实例的句柄 
HKEY：注册表键的句柄 
HMODULE：模块的句柄 
HWND：窗口的句柄 


```


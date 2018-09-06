## Windows多线程
### 线程函数格式
**DWORD WINAPI ThreadFunction (LPVOD pParam);**

### 传递参数
将参数封装到一个结构体里

### 启动多线程
```C++
 HANDLE WINAPI CreateThread(
      _In_opt_  LPSECURITY_ATTRIBUTES  lpThreadAttributes,   
      _In_      SIZE_T                 dwStackSize,
      _In_      LPTHREAD_START_ROUTINE lpStartAddress,
      _In_opt_  LPVOID                 lpParameter,
      _In_      DWORD                  dwCreationFlags,
      _Out_opt_ LPDWORD                lpThreadId
    );
```
```C++
第一个参数 lpThreadAttributes 表示线程内核对象的安全属性，一般传入NULL表示使用默认设置。
第二个参数 dwStackSize 表示线程栈空间大小。传入0表示使用默认大小（1MB）。
第三个参数 lpStartAddress 表示新线程所执行的线程函数地址，多个线程可以使用同一个函数地址。
第四个参数 lpParameter 是传给线程函数的参数。
第五个参数 dwCreationFlags 指定额外的标志来控制线程的创建，为0表示线程创建之后立即就可以进行调度，如果为CREATE_SUSPENDED则表示线程创建后暂停运行，这样它就无法调度，直到调用ResumeThread()。
第六个参数 lpThreadId 将返回线程的ID号，传入NULL表示不需要返回该线程ID号。
```

## 实例

```c++
//参数结构体
struct INFO
{
	INFO(CString _s, CString _f, int _d){secret = _s; fpath = _f; direc = _d;}
	CString secret;
	CString fpath;
	int direc;
};
//多线程函数
DWORD WINAPI startDEncrypt(LPVOID lParam);

//启动多线程并传参
INFO *info = new INFO(secret, filePath, 0);
CreateThread(NULL,NULL,startDEncrypt,info,NULL,NULL);
```
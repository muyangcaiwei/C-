## hook
```C++
获取窗口
CWnd* cwnd = Findwindow(NULL,_T("title"));

获取句柄handle
HWND handle = cwnd->GetSafeHwnd();

CWnd->HWnd
CWnd cwnd;
cwnd.Attach(handle);

关闭窗口 
SendMessageA((HWND)handle,WM_CLOSE,NULL,NULL);

获取中文窗口标题
#include<locale>

WCHAR title[255];
setlocale(LC_ALL, "");
::GetWindowTextW(handle,title, 100 ); // 注意前面的两个冒号必须有，否则会提示没有重载该函数
MessageBoxW((LPWSTR)title);

判断WCHAR是否相等
if(!wcscmp(title, _T("你指的是要切换应用吗?")))
{
	MessageBoxW(_T("找到弹窗了"));
}

隐藏窗体
ShowWindow(hwnd,false);

CString 转换成 char *
CString.GetBuffer(0)
    
获取窗体的位置
typedef struct _RECT {
  LONG left; //upper-left x
  LONG top;  //upper-left y
  LONG right;//lower-right x
  LONG bottom;//lower-right y
} RECT, *PRECT;
RECT rect;
GetWindowRect(hwndOwner, &rect); 


问题：
error LNK2019: 无法解析的外部符号
头文件里引入相应的lib文件
#pragma comment (lib, "User32.lib")

```
reference：

在windows10应用中去掉提示窗口

<https://www.cnblogs.com/zhxilin/p/4849341.html>
## ukey项目总结
### MFC使用动态链接库方法
```C++
1.加载动态链接库
HINSTANCE hInstance = LoadLibrary("cncbForUser.dll");

2.获取函数
typedef int (*FUNC)(char* , int* );

FUNC getMediaID;//声明一个函数指针getMediaID

//GetMediaID是dll里的一个方法的名称，参数列表为(char*,int *)
getMediaID = (FUNC)GetProcAddress(hInstance, "GetMediaID");

3.使用函数
char *str;
int a = 0;
....
int ret = getMediaID(str, &a);
```

### 多字节转换为宽字节
```C++
CString str;
//...str赋值操作
int len = str.GetLength() * 2 + 2;//宽字节将2个字节是为一个单位，最后的2个字节是padding存放\0
wchar_t *arr = new wchar_t[len];
memset(arr, '\0', len);
//CP_ACP:ANSI
int ret = MultiByteToWideChar(CP_ACP, 0, str.GetBuffer(), str.GetLength() , arr, str.GetLength() );
//最终的arr存放的就是宽字节，可以转换为BYTE*使用
```


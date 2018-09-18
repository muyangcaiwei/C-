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


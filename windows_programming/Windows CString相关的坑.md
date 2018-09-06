Windows CString相关的坑
```C++

CString lpsz;

....

const char * p =(const char *)lpsz;  //Unicode编码的话，得到的只是lpsz的第一个字符

正确的姿势
#include <atlbase.h>
USES_CONVERSION;
const char *p = T2A(lpsz);
```
## a++ �� ++a������
```c++
Author:   ��ϡ��
Tool:	  Visual Studio 2012
Compiler: cl
```

```c++
	int a = 4;
00A113EE  mov         dword ptr [a],4  
    a = (a++) + (++a);
00A113F5  mov         eax,dword ptr [a]  //eax = 4
00A113F8  add         eax,1  		 //eax += 1 (eax = 5)
00A113FB  mov         dword ptr [a],eax  //a = eax(5)
00A113FE  mov         ecx,dword ptr [a]  //ecx = a(5)
00A11401  add         ecx,dword ptr [a]  //exc = ecx + a (5 + 5 = 10)
00A11404  mov         dword ptr [a],ecx  //a = ecx (10)
00A11407  mov         edx,dword ptr [a]  //edx = a (10)
00A1140A  add         edx,1  		 //edx += 1 (11)
00A1140D  mov         dword ptr [a],edx  //a = edx (11)



    a = 4;
00A1142B  mov         dword ptr [a],4  	 // a = 4
    a = (++a) + (++a);
00A11432  mov         eax,dword ptr [a]  // eax = a(4)
00A11435  add         eax,1  		 // eax += 1(5)
00A11438  mov         dword ptr [a],eax  // a = eax (5)
00A1143B  mov         ecx,dword ptr [a]  // ecx = a(5)
00A1143E  add         ecx,1  		 // ecx += 1 (6)
00A11441  mov         dword ptr [a],ecx  // a = ecx (6)
00A11444  mov         edx,dword ptr [a]  // edx = a(6)
00A11447  add         edx,dword ptr [a]  // edx += a (12)
00A1144A  mov         dword ptr [a],edx  // a = edx (12)




    a = 4;
00A11468  mov         dword ptr [a],4    // a = 4
    a = (a++) + (a++);
00A1146F  mov         eax,dword ptr [a]  // eax = a (4)
00A11472  add         eax,dword ptr [a]  // eax += a (8)
    a = (a++) + (a++);
00A11475  mov         dword ptr [a],eax  // a = eax (8)
00A11478  mov         ecx,dword ptr [a]  // ecx = a(8)
00A1147B  add         ecx,1  		 // ecx += 1 (9)
00A1147E  mov         dword ptr [a],ecx  // a = ecx (9)
00A11481  mov         edx,dword ptr [a]  // edx = a (9)
00A11484  add         edx,1  		 // edx += 1 (10)
00A11487  mov         dword ptr [a],edx  // a = edx (10)




    a = 4;
00A114A5  mov         dword ptr [a],4    // a = 4
    a = (++a) + (a++);//10
00A114AC  mov         eax,dword ptr [a]  // eax = a(4)
00A114AF  add         eax,1  		 // eax += 1 (5)
00A114B2  mov         dword ptr [a],eax  // a = eax (5)
00A114B5  mov         ecx,dword ptr [a]  // ecx = a(5)
00A114B8  add         ecx,dword ptr [a]  // ecx += a (10)
00A114BB  mov         dword ptr [a],ecx  // a = ecx(10)
00A114BE  mov         edx,dword ptr [a]  // edx = a (10)
00A114C1  add         edx,1  		 // edx += 1(11)
00A114C4  mov         dword ptr [a],edx  // a = edx (11)
```

## �ܽ�
```c++
1.��vs�У��ǰ������ȼ�����������ģ����Ҵӻ���������++a�����ȼ�Ҫ����a++
2.����a++����++�����ȼ�ҪС�ڼӺţ�+��
	���� a = 4
		a = (a++) + (++a)
		a = (++a) + (a++)
	����������++a,��ʱa = 5��Ȼ��a = a + a,����ִ�� a++���++���� ��a += 1��
3.��GCC����ͬ����++a�Ĵ��������Ƚ�a += 1����������ʱ���a�ĵ�ַ��ȡ���µĽ��
```
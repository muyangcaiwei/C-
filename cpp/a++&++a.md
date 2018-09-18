## ����a++��++a���������
```assembly
Author��	 ��ϡ��
Tool:	  Code blocks
Compiler: GNU GCC Compiler
```

```assembly
a = 4
a = (a++) + (++a)
0x40134e	movl   $0x4,0x1c(%esp)  // esp+0x1c <- 4
0x401356	mov    0x1c(%esp),%eax  // a -> eax				;eax = 4
0x40135a	lea    0x1(%eax),%edx   // eax + 1 -> dex 		;edx = 5, eax = 4
0x40135d	mov    %edx,0x1c(%esp)  // edx -> esp + 0x1c
0x401361	addl   $0x1,0x1c(%esp)  // (esp + 0x1c) + 1 	;esp + 0x1c = 6
0x401366	add    %eax,0x1c(%esp)  // (eax) + (esp + 0x1c) ;10

a = 4
a = (++a) + (++a)
0x40137e	movl   $0x4,0x1c(%esp)  // esp + 0x1c <- 4
0x401386	addl   $0x1,0x1c(%esp)  // (esp + 0x1c) + 1		;5
0x40138b	addl   $0x1,0x1c(%esp)  // (esp + 0x1c) + 1 	;6
0x401390	mov    0x1c(%esp),%eax  // (esp + 0x1c) -> eax 	;6
0x401394	add    %eax,%eax 	    // eax * 2  			;12
0x401396	mov    %eax,0x1c(%esp)  // eax -> esp + 0x1c 	;12

a = 4
a = (a++) + (a++)
0x4013ae	movl   $0x4,0x1c(%esp) 	// esp + 0x1c <- 4
0x4013b6	mov    0x1c(%esp),%edx  // esp + 0x1c -> edx	;edx = 4
0x4013ba	lea    0x1(%edx),%eax   // edx + 1 -> eax		;5
0x4013bd	mov    %eax,0x1c(%esp)  // eax-> esp + 0x1c		;5
0x4013c1	mov    0x1c(%esp),%eax  // esp+0x1c -> eax		;eax = 5
0x4013c5	lea    0x1(%eax),%ecx 	// eax + 1 -> ecx		;6
0x4013c8	mov    %ecx,0x1c(%esp)  // ecx -> esp + 0x1c	;6
0x4013cc	add    %edx,%eax		// edx + eax -> eax		;9

a = 4
a = (++a) + (a++)
0x4013e6	movl   $0x4,0x1c(%esp)	// 4 -> esp + 0x1c
0x4013ee	addl   $0x1,0x1c(%esp)  // esp + 0x1c + 1		;5
0x4013f3	mov    0x1c(%esp),%eax  // esp + 0x1c -> eax	;eax = 5
0x4013f7	lea    0x1(%eax),%edx   // eax + 1 -> edx		;edx = 6
0x4013fa	mov    %edx,0x1c(%esp)	// edx -> esp + 0x1c	;6
0x4013fe	add    %eax,0x1c(%esp) 	// eax + esp + 0x1c		;5 + 6 = 11
```

```C++
Result:
10
12
9
11
```
## �ܽ᣺
��GCC�������У�����a++�����Ƚ�a -> eax �ݴ棬Ȼ��a��ֵ��1
```C++
*(&a) -> eax;
*(&a) += 1;
```
����++a����ͨ���Ĵ�����ֱ�ӽ�a += 1
```C++
*(&a) += 1;
```
### ����
```C++
(1)
a = 4
a = (a++) + (++a)
1.��a��ֵ����eax[eax = 4]�У�Ȼ��a��ֵ+1 [a = 5] ��a++��
2.��a��ֵ�ټ�1 [a = 6] ��++a��
3.���ս�eax��ֵ��a��ֵ��Ӽ��� [4 + 6 = 10]

(2)
a = 4
a = (++a) + (++a)
1.��a��ֱֵ�� +1 [a = 5]��++a��
2.��a��ֵ�� +1 [a = 6] (++a)
3.ֱ�Ӵ�a�ĵ�ַ��ȡֵ *(&a) ��Ȼ����� [6 + 6 = 12]

(3)
a = 4
a = (a++) + (a++)
1.a��ֵ�ŵ�eax�� [eax = 4]��Ȼ��a��ֵ+1 [a += 1]��a++��
2.��a��ֵ�ŵ�edx��[edx = 5],Ȼ��a��ֵ+1 [a += 1] (a++)
3.��eax��edx���[eax + edx = 4 + 5 = 9]

(4)
a = 4
a = (++a) + (a++)
1.��a��ֱֵ��+1 [a += 1; a = 5] (++a)
2.��a��ֵ�ŵ�eax�� [eax = 5],a��ֵ+1 [a = 6] ��a++��
3.��a�ĵ�ַ��ȡ�����µ�ֵ [a = 6]��Ȼ����eax��� [a + eax = 11]
```
**���ϣ�++a��a++���ȼ�һ������������ҽ��С����ʹ��a++�Ļ����ӼĴ���ȡֵ������ֵΪ++֮ǰ�ľ�ֵ�����ʹ��++a�Ļ�������������Ľ�ֱ�Ӵ�a�ĵ�ַ��ȡ���µ�ֵ**


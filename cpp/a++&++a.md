## 关于a++与++a的相关运算
```assembly
Author：	 咸稀饭
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
## 总结：
在GCC编译器中，对于a++，首先将a -> eax 暂存，然后将a的值加1
```C++
*(&a) -> eax;
*(&a) += 1;
```
对于++a，不通过寄存器，直接将a += 1
```C++
*(&a) += 1;
```
### 剖析
```C++
(1)
a = 4
a = (a++) + (++a)
1.将a的值放入eax[eax = 4]中，然后将a的值+1 [a = 5] （a++）
2.将a的值再加1 [a = 6] （++a）
3.最终将eax的值与a的值相加即可 [4 + 6 = 10]

(2)
a = 4
a = (++a) + (++a)
1.将a的值直接 +1 [a = 5]（++a）
2.将a的值再 +1 [a = 6] (++a)
3.直接从a的地址里取值 *(&a) ，然后相加 [6 + 6 = 12]

(3)
a = 4
a = (a++) + (a++)
1.a的值放到eax中 [eax = 4]，然后将a的值+1 [a += 1]（a++）
2.将a的值放到edx中[edx = 5],然后a的值+1 [a += 1] (a++)
3.将eax与edx相加[eax + edx = 4 + 5 = 9]

(4)
a = 4
a = (++a) + (a++)
1.将a的值直接+1 [a += 1; a = 5] (++a)
2.将a的值放到eax中 [eax = 5],a的值+1 [a = 6] （a++）
3.从a的地址里取出最新的值 [a = 6]，然后与eax相加 [a + eax = 11]
```
**综上，++a与a++优先级一样，运算从左到右进行。如果使用a++的话将从寄存器取值，并且值为++之前的旧值，如果使用++a的话，最后参与运算的将直接从a的地址处取最新的值**


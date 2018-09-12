STL六大组件
```C++

容器 序列容器：   vector 动态数组

			    list 双向链表

                 queue 使用deque实现，加了适配器

                 deque 控制单元，通过链表指向多个连续的内存控件

                 stack 默认使用deque实现，加了适配器

	关联容器 ：	set	红黑树，只有key，没有value，插入后自动排序

                 map  红黑树 插入，查找，删除都log(n)

                 multiset 红黑树，允许有重复键

                 multimap 不能使用[]	

算法

迭代器 ： input iterator: 只能读

		 output iterator：只能写

		 forward iterator：在一个方向上移动(begin->end，不支持iter--)，可读可写

		 bidirectional iterator ：可在两个方向上移动，支持iter++/iter--，可读可写

		 random access iterator：提供了算术运算能力，iter + n / iter - iter1 / iter < iter1,可随机访问元素

配置器

仿函数 实际上就是一个class，重载了operator()
       refer:https://www.cnblogs.com/decade-dnbc66/p/5347088.html

配接器 stack和queue，通过对deque的封装
```





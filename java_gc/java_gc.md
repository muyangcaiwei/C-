## JAVA GC机制

### 1. 识别垃圾的算法
#### 1.1 引用计数法
给对象中添加一个引用计数器，每当有一个地方引用它时，计数器值就加1；当引用失效时，计数器值就减1；任何时刻计数器为0的对象就是不可能再被使用的。
![引用计数](E:\中信实习\Github_C++_virtual_inherit\java_gc\img\引用计数.png)
缺点:对循环引用的对象无法进行回收
![循环引用](E:\中信实习\Github_C++_virtual_inherit\java_gc\img\循环引用.png)

```C++
public class Object {
    Object field = null;
    public static void main(String[] args) {
        Thread thread = new Thread(new Runnable() {
            public void run() {
                Object objectA = new Object();
                Object objectB = new Object();//位置1
                objectA.field = objectB;
                objectB.field = objectA;//位置2
                //to do something
                objectA = null;
                objectB = null;//位置3
            }
        });
        thread.start();
        while (true);
    }  
}
```
```C++
代码中标注了1、2、3三个数字，当位置1的语句执行完以后，两个对象的引用计数全部为1。当位置2的语句执行完以后，两个对象的引用计数就全部变成了2。当位置3的语句执行完以后，也就是将二者全部归为空值以后，二者的引用计数仍然为1。根据引用计数算法的回收规则，引用计数没有归0的时候是不会被回收的。
```
#### 1.2 根搜索法 
从GC root出发，探索每个引用节点是否可达，并将可达节点进行标记，搜索过程中走过的路径成为引用链，当从GC root出发无法抵达某个引用节点时，证明此对象不可用。
![根搜索](E:\中信实习\Github_C++_virtual_inherit\java_gc\img\根搜索.png)
### 2. GC算法
#### 2.1 标记清除算法
![标记清除](E:\中信实习\Github_C++_virtual_inherit\java_gc\img\标记清除.png)
直接清除未被引用的垃圾对象
缺点：会产生内存碎片
​     	   GC过程中，会暂停程序执行

​	    效率比较低（全堆对象遍历）

#### 2.2 标记整理算法

![标记整理](E:\中信实习\Github_C++_virtual_inherit\java_gc\img\标记整理.png)
清理时，将所有的存活对象压缩到内存的一端，并清理边界外的其他空间。
缺点：效率也不高
​	   GC暂停时间可能会增长，因为需要进行内存拷贝，并更新他们的引用地址。
#### 2.3 复制算法

该算法主要用于新生代GC（Minor GC）
![复制算法](E:\中信实习\Github_C++_virtual_inherit\java_gc\img\复制算法.png)
两块空间1:1，使用其中一块空间，当发生GC时，将存活对象复制到另外一块空间中，并排列整齐，然后互换两块空间的角色。

在新生代GC机制中
新生代内存分为Eden，survivor1，survivor2（比例为8：1：1）三个区。开始时使用Eden区，当第一次发生Minor GC时，先将Eden区存活对象复制到survivor1区中，然后清空Eden区，当suvivor1区满时，将Eden和survivor1区的存活对象复制到survivor2区，然后清空Eden和survivor1并将survivor2与survivor1角色互换，保证survivor2是空的。每当存活对象在survivor存活一次，则年龄+1，默认达到15岁则进入老年代。

### 3. 垃圾回收器 GC
#### 3.1 串行收集器
![串行](E:\中信实习\Github_C++_virtual_inherit\java_gc\img\串行.PNG)
为单线程环境设计，只使用一个单独的线程进行垃圾回收，通过冻结所有应用线程进行工作。
#### 3.2 并行收集器
![并行](E:\中信实习\Github_C++_virtual_inherit\java_gc\img\并行.PNG)
JVM默认垃圾回收器，它使用多线程进行垃圾回收。同样的当执行垃圾回收时也会冻结所有应用程序线程。
#### 3.3 CMS
### 4. 堆内存

### Refer
<https://www.cnblogs.com/smyhvae/p/4744233.html>

<https://www.jianshu.com/p/5261a62e4d29>
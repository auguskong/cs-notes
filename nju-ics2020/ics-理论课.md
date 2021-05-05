B站视频链接: 

https://www.bilibili.com/video/BV1kE411X7S5



### C 语言程序举例



知识点

* 编译器如何处理自变量
* 高级语言中的运算规则
* 高级语言与指令之间的对应关系
* 机器指令的执行过程
* 机器级数据的表示和运算



```c
-2147483648 < 2147483647
表达式结果 false 
  
int i = -2147483648
i < 2147483647
表达式结果 true  why ?

-2147483647-1 < 2147483647 
  

```



知识点

* 高级语言中的运算规则
* 机器指令的含义和执行
* 计算机内部的运算电路
* 异常检测和处理
* 虚拟地址空间

```c
sum(int a[], unsigned len) {
  int i, sum = 0;
  for (i = 0; i <= len - 1; i++)
    sum += a[i];
  return sum;
}  

当参数len为0时，返回值应该是0，但是却发生访问异常 0xC0000005: Access Violation 这里为什么是地址0xC0000005 ?
当参数len的类型为int时，正常执行, 为什么? 

```





知识点: 

* 机器级数据的表示
* 变量的存储空间分配
* 数据的大端/小端存储方式
* 链接器的符号解析规则



```c
// main.c
int d=100;
int x=200;
int main()
{
	p1();
	printf ("d=%d,x=%d\n", d, x);
	return 0;
}

// p1.c
double d;

void p1()
{
  d=1.0;
}

打印结果
d = 0, x=1072693248 为什么? 
```



知识点

* 乘法运算及溢出
* 虚拟地址空间
* 存储空间映射

```
int copy_array(int *array, int count) {
  int i;
  // 在Heap申请内存
  int *myarray = (int *) malloc(count * sizeof(int));
  if (myarray == NULL)
  	return -1;
  for (i = 0; i < count; i++)
    myarray[i] = array[i];
  return count;
}

count = 2^30 + 1时 会发生什么? 参数很大时, count*sizeof(int)会发生溢出 , heap中的数据会被破坏
```





知识点

* IEEE 754的表示
* X87 FPU的体系结构
* IA-32和x86-64过程调用的参数传递

```c
#include <stdio.h>
main()
{
	double a = 10;
	printf("a = %d\n", a);
}

在IA-32上运行时，打印结果是a=0
在x86-64上运行时，打印的a是一个不确定的值  为什么?
```





知识点

* 数组的存放方式
* Cache的机制
* 访问局部性

```

实现1
void copyij(int src[2048][2048], int dst[2048][2048]) {
  int i,j;
  for (i = 0; i < 2048; i++)
    for (j = 0; j < 2048; j++)
      dst[i][j] = src[i][j];
}

实现2
void copyij(int src[2048][2048], int dst[2048][2048]) {
  int i,j;
  for (j = 0; j < 2048; j++)
    for (i = 0; i < 2048; i++)
      dst[i][j] = src[i][j];
}

实现1 比 实现2 执行速度快21倍 为什么?
```







### 计算机系统基本组成与基本功能



计算机系统 抽象层的转换



应用

算法

编程

操作系统/虚拟机

指令集体系结构(ISA)

为体系结构

功能部件

电路

器件



指令是 01序列? 如何理解 

mov 可能就是01序列 类似于十六进制和二进制的转换 不同的message 其实都是表示同样的meaning? 本质上都是01  计算机中的information 本质就是01序列





课程目标: 使学生清楚理解计算机是如何生成和运行可执行文件的

重点在高级语言及以下的各个抽象层

* C语言程序设计
  * 数据的机器级表示、运算
  * 语句和过程调用的机器级表示
* 操作系统、编译和链接
* 指令集体系结构(ISA) 和汇编
  * 指令系统、机器代码、汇编语言
* 微体系结构及硬件层
  * CPU通用结构
  * 层次结构存储系统





von Neumann architecture



![Von Neumann Architecture - Computer Science GCSE GURU](http://computerscience.gcse.guru/wp-content/uploads/2016/04/Von-Neumann-Architecture-Diagram.jpg)



有Memory 来存储程序, 然后通过一个取指令的部件, 执行, 指令描述如何对数据处理， 将程序和原始数据输入计算机的部件，将运算结果输出计算机的部件。

![image-20210428102002112](/Users/xiangyu/Library/Application Support/typora-user-images/image-20210428102002112.png)



ENIAC: Electronic Numerical Integrator And Computer 

第一台通用电子计算机 

电子真空管

十进制表示信息并运算 

手动编程: 通过设置开关和插拔电缆来实现



和图灵机的区别是什么? 





### 程序开发和执行过程





* 最早的程序开发过程

最早的程序是用打孔纸带或打孔卡片来记录0/1 



语言能够操作的空间范围只是 Register Memory Adder



存在的问题是 如果要在特定指令之前加入新指令的话 需要从新计算地址 不够灵活 同时阅读和书写困难



```
0101 0110
0010 0100
....
```





* 汇编语言程序开发过程

用**符号**来表示跳转位置和变量位置 来简化 

```
add B
jc L0
...
```

汇编程序来完成 汇编语言和机器语言之间的转换



高级语言开发程序



与具体的机器结构无关

面向算法来进行描述 描述能力强 一条语句可能对应几条、几十条、几百条指令

有 面向过程 和 面向对象的语言区别

主要包括三种逻辑处理结构:

* 顺序结构
* 选择结构
* 循环结构

有两种将高级语言转为机器语言的方式

* 编译程序: 先将高级语言的source code编译为对应的可执行文件 然后来运行可执行文件  e.g. C / Java  先要用gcc编译为`.o` 文件 然后通过 `/a.out` 来执行
* 解释程序: 将高级语言逐条翻译为机器指令并立即执行 不需要生成目标文件

e.g. Python 直接运行的就是`.py` 文件



Hello 程序的启动和执行

不同层次语言之间的等价关系



![image-20210428105138744](/Users/xiangyu/Library/Application Support/typora-user-images/image-20210428105138744.png)



### 1.4 编程语言和计算机系统层次



* 早期计算机系统的层次
  * 第一代程序设计语言  直接用指令 0 / 1 序列来表示程序 可以直接在硬件上执行
  * 第二代程序设计语言: 汇编语言 不是0/1序列 需要用操作系统来作为中间
* 现代计算机系统: 需要使用语言处理程序
  * 第三代: 过程式语言，编码描述实现过程 -> 表示如何做
  * 第四代: 非过程语言， 编码只需要说明"做什么"，不需要描述具体的算法实现细节



* 指令集体系结构(ISA)
  * 规定了如何使用硬件 包括指令格式、操作种类以及每种操作对应的操作数 可以参考 80386指令集手册 https://nju-projectn.github.io/i386-manual/toc.htm
  * 



### 1.5 课程内容概要

![image-20210504225313586](/Users/xiangyu/Library/Application Support/typora-user-images/image-20210504225313586.png)



* 三个主题
  * 表示(Representation)
    * 不同的数据类型在寄存器或存储器中如何表示和存储?
    * 指令如何表示和编码? 
    * 存储地址(指针) 如何表示? 如何生成复杂数据结构中数据元素的地址? 
  * 转换(Translation)
    * 高级语言程序对应的机器级代码是怎样的? 如何转换并连接生成可执行文件
  * 执行控制流(Control flow)
    * 计算机能理解的“程序”是如何组织和控制的？
    * 如何在计算机中组织过个程序的并发执行? 
    * 逻辑控制流中的异常事件及其处理
    * I/O 操作的执行控制流
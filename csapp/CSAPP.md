## Reference

Labs: http://csapp.cs.cmu.edu/3e/labs.html

Data Lab：bit 运算与float的相关操作

Bomb Lab：阅读汇编破解密码

Attack Lab：Buffer Overflow 攻击

Cache Lab：实现一个cache simulator已经一个cache efficient的矩阵转置。

Shell Lab：用多进程实现一个简单的linux shell。主要是熟悉进程控制与同步。

Malloc Lab：自己写一个C语言的malloc函数。

Proxy Lab：写一个支持HTML的多线程Server。熟悉Unix网络编程与多线程的控制与同步。

作者：李远

链接：[https://www](https://www/).[zhihu.com/question/20402534/answer/223555103](http://zhihu.com/question/20402534/answer/223555103)

来源：知乎

著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

19-Slides: http://www.cs.cmu.edu/afs/cs/academic/class/15213-f19/www/schedule.html

15-Slides: http://www.cs.cmu.edu/afs/cs/academic/class/15213-f15/www/schedule.html

Video: https://www.bilibili.com/video/BV1iW411d7hd?from=search&seid=6227351850995130111

Recitation Video: https://www.youtube.com/channel/UC9Kz-FH4pRiwYukGhquf-Ug

Lab - Solutions: https://github.com/Zhenye-Na/CSAPP-Labs

https://github.com/anniewu1214/CSAPP

https://github.com/Exely/CSAPP-Labs

CSAPP Lab 2讲解 https://www.youtube.com/watch?v=xvgfuMsFCho&list=PLr7wLi8bQyM1wgKEgclR2AccUhuPql6CO&index=9

知乎专栏: https://zhuanlan.zhihu.com/p/82529114 

课后题答案: https://dreamanddead.gitbooks.io/csapp-3e-solutions/chapter2/2.55.html

Attack Lab: 



## Chapter 1 A Tour of Computer Systems



### 核心概念

* Information is Bits + Context

  * Bits: 计算机中所有的信息(包括disk files, programs stored in memory, user data stored in memory) 都是通过0和1来表示. 但是如何区分和解读这些完全相同的0/1 bit 是通过context来做到的. 

  * Context: 帮助解读0/1 bit的其他的0/1  相互之间产生语义?? 这些context又怎么解读呢? 认为规定的指令集是在这里用到的?

    > The only thing that distinguishes different data objects is the context in which we view them. For example, in different contexts, the same sequence of bytes might represent an integer, floating-point number, character string, or machine instruction.

* 一个简单的`hello.c` 编译全流程

  * Preprocessing 预编译 .c -> .i  处理`#` include语句 纯文本替换 生成新的.i文件 还是**c代码(c program)**

  * Compilation 编译 .i -> .s 将c代码翻译成**assembly-language**

    * ```
      main:
      	subq   $8, %rsp
      	movl   $.LCO, %edi
      	call   puts
      	movl   $0, %eas
      	addq   $8, %rsp
      	ret
      ```

  * Assembly 汇编 .s -> .o 将**assembly-language** 编译成 **machine-language** instructions, packages them in a form known as a **relocatable object program**

  * Linking 链接 .o -> a.out 将已经提前编译好的库函数(e.g. `printf`) merge到``hello.o` 中生成完整的 **executable file**

  ![image-20210425211249040](/Users/xiangyu/Library/Application Support/typora-user-images/image-20210425211249040.png)

* OS提供的 三大抽象
  * Processes: Processor + Main memory + I/O devices
  * Virtual memory: Main memory + I/O devices
  * Files: I/O devices

![image-20210425211159047](/Users/xiangyu/Library/Application Support/typora-user-images/image-20210425211159047.png)

* Hardware Organization of a System
  * Buses: carry bytes of information back and forth between the components
  * I/O Devices: systems's connection to the external world
  * Main Memory: temporary storage device that holds both a program and the data. Logically, memory is organized as a linear array of bytes, each with its own unique address (array index).
  * Processor(CPU): the engine that interprets(executes) instructions stored in main memory
* Concurrency and Parallelism
  * Concurrency: general concept of a system with multiple, simultaneous activities
  * Parallelism: the use of concurrency to make a system run faster





## Chapter 2 Representing and Manipulating Information





### Information Storage

`!` 是逻辑运算, 将True变为False

`~` 是取非位运算 将每一个bit上的1变为0, 0变为1 True取非还是True  只要不是0x0 都是True

### Integer Representation

### Integer Arithmetic

### Floating Point





## Chapter 3 Machine-Level Representation of Program



### 3.1 A Historical Perspective

### 3.2 Program Encodings

### 3.3 Data Formats

### 3.4 Accessing Information



`*`: dereference -> 取出某一个地址包含的值



```c++
// xp是指针类型 read the value stored in xp 并且赋值到long类型的变量x 
long x = *xp;

// xp 是指针, 将xp所指向的地址中的值更新为y所表示的值 xp的地址仍然不变? 
*xp = y;
```



`&`: reference -> 得到某一个地址

### 3.5 Arithmetic and Logical Operations

### 3.6 Control



Processor State

* Temporary data (%rax)
* Location of runtime stack (%rsp)
* Location of current code control point
* Status of recent tests e.g.CF ZF SF OF 

### 3.7 Procedures

* Control 
* Data 
* Memory
* 

### 3.8 Array Allocation and Access



## Chapter 4 Processor Architecture



### The Y86-64 Instruction Set Architecture



virtual address vs. physical address



### Logic Design and the Hardware Control Language HCL

### Sequential Y86-64 Implementations

### General Principles of Pipelining

### Pipelined Y86-64 Implementations




## 资源列表

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

  

* OS提供的 三大抽象
  * Processes: Processor + Main memory + I/O devices
  * Virtual memory: Main memory + I/O devices
  * Files: I/O devices

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



## Chapter 8 Exceptional Control Flow

### 8.1 Exceptions

**基本概念**

* *Exception*: an abrupt change in the control flow in response to some change in the processor's state. e.g. system call, signal, 
* Control Flow: $a_0,a_1, ... a_n$​ 指令执行
* exception table / page table / process table / file table ... 本质都是map structure 将一个整数/字符串 map到一个地址上

**8.1 小结**

本小节重点要理解异常控制流概念，相比于“正常控制流” 完全按照程序本来的逻辑顺序执行，当然程序中也会存在跳转jumps, calls, 但是这些跳转和flow的改变依然是在程序范围内，可以看做是没有任何外部中断。而Exception Flow 是一个外来的影响可能是系统本身或者是其他正在运行的程序。需要想到 这个Exceptional 为什么会存在? 因为我们需要和外界进行交互和反应，有I/O Network, Error。对程序有何影响？可能导致提前终止。 如何处理 单独写处理逻辑来处理

异常的分类 

* 从下到上  从Hardware到Software 不同层级来进行分类
  * Hardware: 
  * OS: system call (trap)
  * Application: 

* 从Exception本身的特点来分类

![8.4-Classes-of-exceptions](..\screenshot\csapp\8.4-Classes-of-exceptions.png)

关于异常的处理，需要认识到异常一定涉及到两个主体，发送方和接收方，在后面章节中可以看到这两个主体可以是 Process/ Process Group / Job / Kernel 

![8.1-Anatomy-of-an-exception](..\screenshot\csapp\8.1-Anatomy-of-an-exception.PNG)



### 8.2 Processes

**基本概念**

* *Context Switch*: Context: that state that the program  needs to run correctly. This state includes the program's code and data stored in memorym, its stack, the contents of its general-purpose registers, its program counter, environment variables, and the set of open file descriptors , Switch ->
*  *Process*: an instance of a program in execution. 
* *Concurrent Flow* vs. *Parallel Flow* 
  * concurrent flow: if two flows overlap in time, even if they are running on the same processor
  * parallel flow: 是concurrent flow的子集, 平行的 -> 存在两条不相交的线 -> 在两个cores/computers同时运行,也被称为running in parallel / parallel execution 
* *User Mode* vs. *Kernel Mode*

**8.2 小结** 

进程提供的最重要的两个抽象: 

* 独立的逻辑控制流
* 私有的地址空间

进程是人为创造出来的概念 方便我们更好的管理CPU 和 Memory, 整体划分 time slicing



### 8.3 System Call Error Handling

```c
pid_t Fork(void) 
{
    pid_t pid;
    
    if ((pid = fork()) < 0)
        unix_error("Fork error");
    return pid;
}
```



**8.3 小结**

使用一个error-handling wrappers `Fork` 来进行错误处理，错误处理的常规操作是Unix system-level function会返回一个error变量，-1表示出错，0表示正常退出，同时使用一个`errno` 来标识出错原因



### 8.4 Process Control

**基本概念**

进程状态(state)

* Running: executing on the CPU or waiting to be executed and will eventually be scheduled by the kernel
* Stopped: the execution of the process is **suspended** and will not be scheduled. `SIGSTOP` `SIGTSTP` `SIGTTIN` `SIGTTOU` 信号可以让进程stop. `SIGCONT`可以让进程恢复运行
* Terminated: The process is stopped permanently. 可能有三种原因导致: 1. receive a signal whose default action is to terminate the process 2. returning from the main routine 3. calling the `exit` function

8.4 小结: 

本小节的知识点是对于进程的操作，结合进程的生命周期的角度来看掌握内置的系统调用方法 Create -> Run -> Pause / Sleep / Interrupt / -> Terminate -> Reap 

关于进程操作的方法

```c

pid_t getpid(void) 
// returns: PID of the caller
    
pid_t getppid(void)
// returns: PID of the parent

void exit(int status)

pid_t fork(void)
// returns: 0 to child, PID of child o parent, -1 on error
    
pid_t waitpid(pid_t pid, int *statusp, int options)
// returns: PID of child if OK, 0(WNOHANG), or -1 on error
    
pid wait(int *statusp)
// wait是waitpid的简易版本 默认pid是当前process 和 options变量   
    
unsigned int sleep(unsigned int secs)    
    
int pause(void)

int execve(const char *filename, const char *argv[], const char *envp[]) 
// Does not return if OK; returns -1 on error  
    
char *getenv(const char *name) 
// returns: pointer to name if it exists, NULL if no match

int setenv(const char *name, const char *newvalue, int overwrite)
// returns: 0 on success, -1 on error
    
void unsetenv(const char *name)
// returns: nothing
    

```



### 8.5 Signal

**基本概念**

* Sending Signal
  * `/bin/kill` Program  `linux > /bin/kill -9 15213`
  * Keyboard / Terminal Command
  * `kill` function  `int kill(pid_t pid, int sig)`
    * pid > 0 send signal sig to process pid
    * if pid = 0 send signal sig to every process in the process group of the calling process, including the calling process itself.
    * if pid < 0 send signal sig to every process in process group |pid|
* Receiving Signals
  * each signal type has a default action
    * process terminates
    * process terminates and dumps core
    * process stops until restarted by a SIGCONT signal
    * process ignores the signal
* Blocking / Unblocking Signal
  * implicit blcoking: kernel blocks any pending signals of the type currently being processed by a handler
  * explicit blocking: use `sigprocmask` function
* Writing Signal Handlers

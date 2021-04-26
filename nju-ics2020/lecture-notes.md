

Markdown Cheat Sheet: https://wordpress.com/support/markdown-quick-reference/



## P1 C语言拾遗(1): 机制

### 本讲概述

两个重点内容

​	**1. 编译 链接 加载都做了什么**

​	**2. RTFSC时需要关注的C语言特性**



`echo $?  # 查看程序的返回值`



#### 从`hello.c`源代码文件 翻译到 `hello`可执行文件的四个阶段 

* 预编译	`gcc -E a.c`

  ```
  ➜  ~ gcc -E a.c
  # 1 "a.c"
  # 1 "<built-in>" 1
  # 1 "<built-in>" 3
  # 366 "<built-in>" 3
  # 1 "<command line>" 1
  # 1 "<built-in>" 2
  # 1 "a.c" 2
  int main{}
  ```

* 编译  `gcc -S a.c` =>  `a.s`  

  ```
  1           .section        __TEXT,__text,regular,pure_instructions
    1         .build_version macos, 11, 0     sdk_version 11, 1
    2         .globl  _main                   ## -- Begin function main
    3         .p2align        4, 0x90
    4 _main:                                  ## @main
    5         .cfi_startproc
    6 ## %bb.0:
    7         pushq   %rbp
    8         .cfi_def_cfa_offset 16
    9         .cfi_offset %rbp, -16
   10         movq    %rsp, %rbp
   11         .cfi_def_cfa_register %rbp
   12         xorl    %eax, %eax
   13         popq    %rbp
   14         retq
   15         .cfi_endproc
   16                                         ## -- End function
   17 .subsections_via_symbols
  ```

  

* 汇编

   `gcc -c a.c` =>  `a.o`  如果直接打卡`a.o` 只会看到各种乱码

  ```
  Ïúíþ^G^@^@^A^C^@^@^@^A^@^@^@^D^@^@^@¸^A^@^@^@ ^@^@^@^@^@^@^Y^@^@^@8^A^@^@^@^@^@^@^@^@^    @^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@h^@^@^@^@^@^@^@Ø^A^@^@^@^@^@^@h^@^@^@^@^@^@^@^G^@^@    ^@^G^@^@^@^C^@^@^@^@^@^@^@__text^@^@^@^@^@^@^@^@^@^@__TEXT^@^@^@^@^@^@^@^@^@^@^@^@^@^@    ^@^@^@^@^H^@^@^@^@^@^@^@Ø^A^@^@^D^@^@^@^@^@^@^@^@^@^@^@^@^D^@<80>^@^@^@^@^@^@^@^@^@^@^    @^@__compact_unwind__LD^@^@^@^@^@^@^@^@^@^@^@^@^H^@^@^@^@^@^@^@ ^@^@^@^@^@^@^@à^A^@^@^    C^@^@^@@^B^@^@^A^@^@^@^@^@^@^B^@^@^@^@^@^@^@^@^@^@^@^@__eh_frame^@^@^@^@^@^@__TEXT^@^@    ^@^@^@^@^@^@^@^@(^@^@^@^@^@^@^@@^@^@^@^@^@^@^@^@^B^@^@^C^@^@^@^@^@^@^@^@^@^@^@^K^@^@h^    @^@^@^@^@^@^@^@^@^@^@^@2^@^@^@^X^@^@^@^A^@^@^@^@^@^K^@^@^A^K^@^@^@^@^@^B^@^@^@^X^@^@^@    H^B^@^@^A^@^@^@X^B^@^@^H^@^@^@^K^@^@^@P^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^A^@^@^@^A^@^@^@^    @^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^    @^@^@^@^@^@^@^@^@UH<89>å1À]Ã^@^@^@^@^@^@^@^@^H^@^@^@^@^@^@^A^@^@^@^@^@^@^@^@^@^@^@^@^@    ^@^@^@^T^@^@^@^@^@^@^@^AzR^@^Ax^P^A^P^L^G^H<90>^A^@^@$^@^@^@^\^@^@^@¸ÿÿÿÿÿÿÿ^H^@^@^@^@    ^@^@^@^@A^N^P<86>^BC^M^F^@^@^@^@^@^@^@^@^@^@^@^A^@^@^F^A^@^@^@^O^A^@^@^@^@^@^@^@^@^@^@    ^@_main^@^@
  ```

  

  `objdump -d a.o`: 将`a.o`文件反汇编 `a.o`是没有进行链接前的二进制文件，会得到下面的输出

  ```
  a.o:	file format Mach-O 64-bit x86-64
  
  
  Disassembly of section __TEXT,__text:
  
  0000000000000000 _main:
         0: 55                           	pushq	%rbp
         1: 48 89 e5                     	movq	%rsp, %rbp
         4: 31 c0                        	xorl	%eax, %eax
         6: 5d                           	popq	%rbp
         7: c3                           	retq
  ```

* 链接



* 加载执行

  `./a.out`

  背后都是通过调用命令行工具完成的，控制行为的三个选项: `-E, -S, -c` 分别都做了什么?  `-E` 预编译 `-S` 编译 `-c`链接

  `gcc --help man gcc` 查看具体细节

  

  使用`vi a.out`直接打开可执行文件会出现乱码，可以在vim中使用`:%!xxd` 来翻译

  [Stackoverflow-Use Vim as a hex editor](https://vi.stackexchange.com/a/2234)

  >You can use the `xxd` command to transform a file in Vim to hex representation, doing
  >
  >```
  >:%!xxd
  >```
  >
  >`:` enters command-line mode, `%` matches whole file as a range, `!` filters that range through an external command, `xxd` is that external shell command

  

  可以使用 `file a.out` 来查看`a.out`文件具体内容

  

`.c ->(预编译 Precompile) .l ->(编译 Compile) .s ->(汇编 Assembly) .o ->(链接 Link) a.out`



Q: 背后到底都发生了什么? 如何验证我们的判断/猜想? 

A: 使用命令行工具来查看

如何来学习`gcc` command 先从读gcc的手册开始 

`tldr gcc` 需要安装`tldr`二进制工具来查看gcc中最常用的一些命令



#### 进入C语言之前: 预编译 



判断哪些部分是由预编译负责的依据: `#` 开头

```
#include
#define
#
##
```



> `#` 究竟在干什么? 什么是引用?

```c
#include <stdio.h> //是一条预编译指令 做的事情就是把include的内容直接复制粘贴进来
```



示例: 层层include的结果

```c
//a.c
  #include <stdio.h>
  1 int main() {
  2   printf(
  3 #include "a.inc" // 必须要错开写 否则会有expected expression error 
  4 );
  5 }

// a.inc
#include "b"

// b
"hello, world!\n"
  
// 如果运行 ./a.out
hello world
```



> 在#include 当中的 < > 和 " " 区别是什么? 

```c
#include <stdio.h> // 在系统的内部进行search
#include "stdio.h"
```



更好的方法是**阅读命令的日志**



`gcc a.c --verbose`

使用`verbose`来发现命令运行之后发生了什么

在gcc 内部的config设置成了默认的`-x86`



`gcc a.c -I.` 如果存在可以搜索当前的目录中的 



```
gcc a.out --verbose
```



示例: 

```c
// 会输出什么? 
// 答案: Yes 因为aa 和 bb 都是null
#include <stdio.h>

int main() {
  #if aa == bb
  	printf("Yes\n");
  #else
    printf("No\n");
  #endif
}
```



宏是文件的替换

宏定义与展开

**宏展开**: 通过复制/粘贴改变代码的形态 

* `#include` -> 粘贴文件
* `aa bb ` -> 粘贴符号



`##`: 连接两个关键字

`#define true (__LINE__ % 10 != 0)` 改变代码中的true的定义 `__LINE__` 是在c中定义的宏

X-Macros

```c
#define NAMES(X) \ 
  X(Tom) X(Jerry) X(Tyke) X(Spike)
    
int main() {
    #define PRINT(x) puts("Hello, " #x "!");
    NAMES(PRINT)
}
```



宏展开: 通过复制/粘贴改变代码的形态

反复粘贴: 直到没有宏可以展开为止



**有趣的预编译**

* Pros
  * 提供灵活的用法 (X-macros)
  * 接近自然语言的用法

```c
#define L (
int main L) { puts L "Hello, World");}
```

* Cons
  * 破坏可读性 程序分析(补全)



#### 编译与链接



*编译*: C代码的连续一段内容总能找到对应的一段连续的机器指令

示例: 

```c
int foo(int n) {
  int sum = 0;
  for (int i = 1; i <= n; i++) {
    sum += i;
  }
  return sum;
}
```







编译出来的结果是什么? 



*链接*: 将多个二进制目标代码拼凑在一起

* C中称为编译单元 compilation unit
* 甚至可以链接C++, Rust, ...代码

链接是在做什么? 链接是将所有的a.o b.o 都链接到一起





#### 加载: 进入C语言的世界





**C程序执行的两个视角**

*静态*: C代码的连续一段总能对应到一段连续的机器指令

*动态*: C代码执行的状态总能对应到机器的状态

* 源代码视角: 
  * 函数、变量、指针

* 机器指令视角
  * 寄存器、内存、地址

两个视角的**共同之处**: 内存 (一段足够大的以字节为单位的连续数组)

代码、变量(源代码视角) = 地址 + 长度(机器指令视角)



本质上所有的东西都是指针





内存模型

动态的内存模型?

C语言中的所有内容都是指针

一切都可以取地址(包括)



示例: 

```c
void printptr(void *p) {
  printf("*p = %p; *p = %0161x\n", p, *(long *)p);
}
int x;
int main(int argc, char *argv[]) {
  printptr(main);  // 代码
  printptr(&main); 
  printptr(&x);    // 数据
  printptr(&argc); // 堆栈
  printptr(&argc); // 堆栈
  printptr(argv); 
  printptr(&argv); // 堆栈
  printptr(argv[0]); // 堆栈
}
```





计算机系统就是状态机 整体一门课最重要的概念 程序是在执行一段指令

C语言中的所有内容都是地址

类型是对于地址的解读

C Type System

```c
int main(int argc, char *argv[]) {

int (*f)(int, char *[]) = main; // f是指向main()的指针

if (argc != 0) {

char ***a = &argv, *first = argv[0], ch = argv[0][0];

\printf("arg = \"%s\"; ch = '%c'\n", first, ch);

assert(***a == ch);

f(argc - 1, argv + 1); // 调用f()

}

}
```



指针运算 == 地址运算



## P2 C语言拾遗(2): 编程实践

### 本讲概述



怎样写代码才能从一个大型项目里存活下来

* 核心准则: 编写可读代码
* 两个例子



### 核心准则: 编写可读代码



不可读 = 不可维护



编写代码的准则: 降低维护成本

* 宏观
  * 做好分解和解耦 (参考现实世界中的复杂系统 学校、高铁系统)

* 微观

  * 不言自明: 只通过阅读代码就能理解一段程序是**做什么的**

  * 不严自证: 只通过阅读代码就能验证一段程序**与specification的一致性**



### 例子1: 实现数字逻辑电路模拟器



### 例子2: 实现YEMU全系统模拟器





程序之间的内在关系可能是你不知道的

```c
// 使用预编译 宏的版本

#define FORALL_REGS(X) _(X) _(Y)
#define LOGIC X1 = !X && Y; 
Y1 = !X && !Y;

#define DEFINE(X) static int X, X##1;

#define UPDATE(X) X = X##1;

#define PRINT(X) printf(#X " = %d; ", X);

int main() {

FORALL_REGS(DEFINE);

// DEFINE(X) DEFINE(Y)

// static int X, X1; static int Y, Y1;

while (1) { // clock

FORALL_REGS(PRINT); putchar('\n'); sleep(1);

LOGIC; //更新所有逻辑门

FORALL_REGS(UPDATE);

}
```





## P3 框架代码选讲(1) 编译运行



### 本讲概述

* Git, GitHub与代码仓库
* 项目的构建
  * Lab
  * NEMU
  * AbstractMachine 【这是什么玩意?】



### 工具/文档

* `tldr`: 简化命令行工具help page 的程序 [Git Repo](https://github.com/tldr-pages/tldr)

* [Visual Git Reference](https://marklodato.github.io/visual-git-guide/index-en.html)
* [Visualizing Git Concepts with D3](http://onlywei.github.io/explain-git-with-d3/#)



白名单 .gitignore 文件

只在Git repo里管理 `.c` `.h` 和 `Makefile`

```
*       # 忽略一切文件
!*/     # 除了目录
!*.c    # .c 文件
!*.h    # .h 文件
!Makefile
!.gitignore 
```



### 项目构建



#### Make 工具



Makefile是一段 "declarative"的代码

描述了构建目标之间的依赖关系和更新方法

同时也是和Shell结合紧密的编程语言

* 能够生成各种字符串
* 支持"元编程"(`#include`, `#define` ...) 【什么意思? 支持表示能够复制粘贴?】	





有向无环图  可以只编译需要编译的文件 + 依赖



多核处理器 -> 进行多核操作

`make -B`

`make -B -j8`



可以使用 `time` 来计时



想要运行很多东西的时候 可以尝试并行



C 和 Unix 和 Shell Make 工具是分不开的 理解C是进入Linux世界的基础



为什么读Makefile 感觉有点困难



一个Makefile 描述了一个有向无环图



Make工具会按照一个拓扑排序的顺序来构建这个图



忽略不需要构建的内容/文件



表面复杂 本质就是个有向无环图 



通过`man make` 来阅读make的手册 来找一些附加的选项 



`-n`: --just-print  只打印 不编译

Print the commands that would be executed, but do not execute them



`:set nowrap`



gcc

`-I`: 定义include的路径

`-D`: define  定义脚本中的宏



其实就是一堆 `gcc -c `



Docs as code 直接通过代码来生成注释 



使用工具是编程的一部分 



依赖的管理 



### 总结



计算机的正确打开方式

* 编程 不等于 闷头写代码
* 使用工具也是编程的一部分
  * git
  * build systems
  * shell



基本原则: 任何感到不爽的事情都一定有工具能帮你 

* 如果真的没有，自己造一个的机会来了







## P4 框架代码选讲2-代码导读



### 本讲概述

* 浏览源代码

* 启动代码选讲

* 编辑器配置

拿到项目源代码之后 先大概浏览整个项目

* 项目总体组织
  * `tree .`
  * `tree . | less`
  * `find . -name "*.c"` 查看当前目录下的文件
  * `find . -name "*.c" -o "*.h"`  找到当前目录下所有的.c 和 .h 文件
    * `-name` 表示命名
    *  `-o` 表示"或"一个操作

* 项目规模
  * `find ... | xargs cat | wc -l` 项目规模





尝试阅读代码





vi . 直接打开一个目录来进行文件的浏览?

fzf: 命令行工具

vi $(fzf)

parse(argc - 1, argv + 1)

argv 可以直接舍弃命令行传入的第一个参数 从第二个参数开始读

static inline 只在一行

assert() 如果判断条件不成立 程序会立刻终止

调试segment fault的方法 使用gdb

`layout asm`: assembly layout $xxx 代表一个常数

PA2 的时候遇到了预编译的函数不确定内部实现的时候 需要使用gcc进行调整

vimrc的set up应该是 `set tags=./tags,tags;`

 is used to overwrite

 is used to append to a file

tokens 数组从0开始读?





static inline() 



## P8 Abstract Machine 选讲



### 本讲概述

* 复杂系统的构造与解释
* 理解计算机系统
* 理解AbstractMachine
* 代码导读



### 复杂系统的构造与解释



《计算机系统基础》到底在学什么? 

计算机系统是一个状态机



* 状态机的状态是什么?
  * 内存 + 寄存器 + (外部设备状态)

* 状态机的行为是什么? 
  * 取指令 + 译码 + 执行
  * 输入/输出设备访问
  * 中断 + 异常控制流
  * 地址转换



## P10 调试: 理论与实践



### 本讲概述

* 调试理论
* 调试理论的应用
  * 调试"不是代码" 【也就是和编程无关的问题】
  * 调试 PA/Lab/任何代码 



#### 摆正心态: 编程哲学



* 机器永远是对的

* 未测试代码永远是错的

  * 你认为最不可能出bug的地方,往往bug就在那躺着

  * 复制粘贴过来的代码 在之前的地方是对的不等于在新的地方也是对的



#### 调试理论

程序的两个功能

* 人类世界需求的载体: 理解错了需求 -> bug 需要收钱码  而不是付钱码
* 计算过程的精确描述: 实现错误 -> bug  转账10块 变成了5块



代码的本质: 物理世界的需求在计算机世界的一种表示

为什么写代码困难? 程序设计语言的规律和 物理世界中的不精确世界 

需求 -> 设计/算法 -> 代码

人类世界中的需求 不严谨 不完善 自己也说不清楚



手册 + NEMU讲义 变成 代码



本科毕业生的合格要求: 从假想代码 -> 最后代码 应该无压力完成 



#### 为什么debug那么困难? 

因为bug的出发经历了漫长的过程

需求 -> 设计 -> 代码 -> Fault(bug) -> Error(程序状态出错) -> Failure

头脑中有一个假想的执行过程

* 我们只能观测到Failure
* 我们可以检查状态的正确性
* 无法预期bug究竟在哪一行



error: 是程序运行起来之后的某一个中间状态不符合预期 

fault: 程序bug

failure: 可观测到的最后结果错误了



中间的程序执行状态很重要，能够给我们信息来帮助我们进行调试

想清楚每一个时刻每一个变量的值/状态 就很容易debug了



调试理论: 如果我们能判定任意程序状态的正确性，那么给定一个failure, 我们可以通过二分查找定位到**第一个**error的状态，此时的代码就是fault(bug)

用`printf` 打印就是在确认中间状态

可以观测: 

TLE Time Limit Error 运行太久

Wrong Answer 





单步调试 

从一个假定正确的状态出发

每个状态的行为有限，所以容易判断是否是error



为什么调试理论看起来没用? 

A: 因为判定程序状态的正确性非常困难



单步调试的威力



实际中的调试: 通过观察程序执行的轨迹(trace)

* 缩小错误状态可能差生的位置
* 做出适当的假设
* 进行细粒度的定位和诊断



打印printf的时候需要想 哪些量是关键信息 能够帮助判定我们的程序究竟对不对

printf(大概锁定范围 + 做二分) + debugger(精细)



#### 调试理论: 应用(1) 

解决和编程无关的问题: 问题诊断其实也是调试

```
bash: curl: command not found

fatal error: No such file or directory
```



总有一天要进入 **无人区**  解决问题的通用方法



`curl` 背后的原理 `PATH` 有路径

```
a.sh

curl baidu.com

使用外部工具让curl 打印出更多的信息
strace -f bash a.sh 2>&1 | less 
```



从PATH中逐个尝试来找到我们的命令



UNIX世界里做任何事情都是在编程，配置出错 单元测试出错，都是程序或输入/配置有bug 



把所有问题都当做程序来调试



程序出了源代码 还应该考虑 输入 配置



绝大部分工具的Failure都会有"原因报告" 能够帮助快速定位fault



为什么抓瞎?

因为出错原因报告不准确或不够详细

程序执行的过程不详细



#### 调试理论: 应用(2) 调试代码



1. NEMU没有debug信息  
   * 执行着 执行着 纠错了 直接在某个地方死循环了

2. NEMU有两个层次的状态机



NEMU的大部分bug原因是 需求理解错了







Fault -> Error

* 充分的测试

Error -> Failure

* 充足的日志

* 及时的检查



## P11 系统编程与基础设施

### 本讲概述

* 开发/调试的基础设施
* 系统编程: 基础设施
* Differential testing 代码导读





训练 + 基础设施 





例子: 

在vim中直接使用 `map` 命令来讲编译 + 读标准输入 + 输出 来绑定到一个按键上做一定程度的自动化



并行执行编译来缩短编译时间



手册也是开发者写的 每一个命令背后都一定是有一个motivation 



基础设施是应对 重复的



本质上，这些都不是难事，STFW 

对手册、编程语言、搜索技巧比较熟悉的

克服惰性可以使你快速成长 

get out your comfort zone 挑战自己 


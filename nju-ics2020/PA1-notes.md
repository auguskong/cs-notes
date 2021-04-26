# PA1-Notes





## 讲义笔记 

### [在开始愉快的PA之旅之前](https://nju-projectn.github.io/ics-pa-gitbook/ics2020/1.1.html)



做PA的终极目标是通过构建一个**简单完整的计算机系统**，来深入理解程序如何在计算机上运行。只有去尝试理解并掌握计算机系统的每一处细节，才能一步步完成PA



PA的正确做法

* 多思考为什么
* 独立解决问题
* 尝试尽可能理解每一处细节
* 用正确的工具做事情: 节省时间的科学方法 比如fzf, cscope
* 多读讲义
* 按时完成，拒绝拖延



[提问的智慧](https://github.com/ryanhanwu/How-To-Ask-Questions-The-Smart-Way/blob/main/README-zh_CN.md)

* 在提出问题之前,先做到
  * 在准备提问的论坛旧文章中搜索
  * 上网Google
  * 手册
  * FAQ
  * 自己检查或试验
  * 向强者朋友打听
  * 尝试阅读源码





实现红白机模拟器 



模拟硬件的世界，在这个硬件世界中执行程序，将要在PA中编写一个用来执行其他程序的程序 ? 

执行其他程序的程序是什么意思?



NEMU 是什么?  例子是ATM与支付宝APP的关系

ATM有物理运行实体

支付宝没有物理运行实体, 都是通过程序来进行记录和交易的 转账 存款 取款不是和真正的纸钱 而是在支付宝APP内部来进行的



NEMU就是模拟计算机系统的程序

* 可以用数组模拟内存，那么对于这个数组进行读写就相当于对内存进行读写

* 结构体模拟cpu

* ...



Hello World

Simulated hardware

NEMU

GNU/Linux

Real hardware





### [开天辟地的篇章](https://nju-projectn.github.io/ics-pa-gitbook/ics2020/1.2.html)



处理数据(信息)

最简单的计算机



处理 = 运算 加减乘除 用加法器举例 处理1+2+....+100 

存储 + 计算

存储 -> 内存

计算 -> 

* 指令 需要用`PC(Program Counter)` 在x86中特定的名字是 `EIP(Extended Instruction Pointer)` 来确定CPU现在执行到了哪一条指令

* CPU 

  ```
  while (1) {
  	从PC指示的存储器位置取出指令;
  	执行指令;
  	更新PC;
  }
  ```

  ```
  // PC: instruction           | // label: statement
  0: mov r1, 0								 | pc0: r1 = 0
  1: mov r2, 0								 | pc1: r2 = 0
  2: addi r2, r2, 1						 | pc2: r2 = r2 + 1
  3: add r1, r1, r2						 | pc3: r1 = r1 + r2
  4: blt r2, 100, 2            | pc4: if (r2 < 100) goto pc2
  5: jmp 5										 | pc5: goto pc5
  ```

  





时序逻辑部件(存储器，计数器，寄存器) + 组合逻辑部件(加法器) 

根据当前时序逻辑部件的状态，在组合逻辑部件的作用下，计算并转移到下一个时钟周期的新状态





### RTFSC



`tree -P '*.c'` : 只显示当前文件夹下的`.c` 文件, `-P` 展示符合pattern的文件

Debian 中 `sudo apt-get install tree`

Mac中 `brew install tree`

```
.
├── device
│   ├── alarm.c
│   ├── audio.c
│   ├── device.c
│   ├── intr.c
│   ├── io
│   │   ├── map.c
│   │   ├── mmio.c
│   │   └── port-io.c
│   ├── keyboard.c
│   ├── serial.c
│   ├── timer.c
│   └── vga.c
├── engine
│   └── interpreter
│       └── init.c
├── isa
│   ├── mips32
│   │   ├── difftest
│   │   │   └── dut.c
│   │   ├── exec
│   │   │   ├── exec.c
│   │   │   └── special.c
│   │   ├── init.c
│   │   ├── intr.c
│   │   ├── local-include
│   │   ├── logo.c
│   │   ├── mmu.c
│   │   └── reg.c
│   ├── riscv32
│   │   ├── difftest
│   │   │   └── dut.c
│   │   ├── exec
│   │   │   ├── exec.c
│   │   │   └── special.c
│   │   ├── init.c
│   │   ├── intr.c
│   │   ├── local-include
│   │   ├── logo.c
│   │   ├── mmu.c
│   │   └── reg.c
│   └── x86
│       ├── decode.c
│       ├── difftest
│       │   └── dut.c
│       ├── exec
│       │   ├── exec.c
│       │   └── special.c
│       ├── init.c
│       ├── intr.c
│       ├── local-include
│       ├── logo.c
│       ├── mmu.c
│       └── reg.c
├── main.c
├── memory
│   └── paddr.c
└── monitor
    ├── cpu-exec.c
    ├── debug
    │   ├── expr.c
    │   ├── log.c
    │   ├── ui.c
    │   └── watchpoint.c
    ├── difftest
    │   └── dut.c
    └── monitor.c
```



为什么monitor.c 是自带调试器功能? 



不是自带的 而是需要自己来实现`/monitor/debug` 中的相关函数来完成debug 

* `expr.c `: 生成表达式 + 对字符串表达式进行拆分? 25800022222 
* `log.c`
* `ui.c`
* `watchpoint.c`



(Turing Machine, TRM) 图灵机



客户计算机: 在NEMU中模拟的计算机

客户程序: 在NEMU中运行的"客户程序"





NEMU的四个模块:

* monitor: 目的是为了方便监控客户计算机的运行状态
* CPU: 执行指令?
* memory: 数组
* 设备: 在PA2中介绍



框架代码包括两个主要部分

* ISA无关的基本框架 
* ISA相关的具体实现 在`src/isa/x86` 文件夹中



```c
//main.c

void init_monitor(int, char *[]); // 在monitor.c 中实现
// 继续调用
	parse_args(argc, argv);

  init_log(log_file);

  init_mem();

  init_isa();

  long img_size = load_img();

  init_regex();

  init_wp_pool(); // watchpoint pool

  init_difftest(diff_so_file, img_size, difftest_port);

  welcome();


void engine_start();
int is_exit_status_bad();
```





monitor.h 和 monitor.c 有什么区别?

init_isa() 加载img是什么意思? img 是[disk image](https://en.wikipedia.org/wiki/Disk_image)

每一次`init_isa` 都需要copy image 并且restart pc指针的指向



differential testing是什么? 





程序当前状态(serialized copy of the entire state)可以用img来表示 放在了`/nemu/src/isa/x86/init.c` 当中

https://en.wikipedia.org/wiki/System_image 



将一个内置的客户程序读入到内存中





`sudo dmesg`: 输出操作系统启动日志 



C - union: 

a special data type available in c that allows to store different data types in the same memory location.





如何判断哪些命令只是syntactic sugar? 区分的标准是什么? 



### 基础设施



实例: 

* Makefile 来简化项目的build 和 compile
* Google对于 **Multiplier**类型的项目定义: 做好一个项目能够让多个项目得益
* 在NEMU中实现Monitor作为简易调试器(PA1需要做的)



为什么说简易调试器是一项非常重要的基础设施呢? 



NEMU是用来执行其它客户程序的程序，程序的中间状态信息对外面的调试器是不容易获取的 所以必须要在NEMU中实现一个调试器来进行状态个跟踪和监控?



### 表达式求值





## 需求



* 实现表达式求值

* 通过Random Testing 来检测我的表达式求值的实现
* 实现监视点





## C 语法 Q&A



Q: How to read the `input.txt` file in *main.c* ?

`FILE *fp = fopen("toosl/gen-expr/test/input.txt", "r");`



Q: How to read a new line in c?

```c
while (fscanf(fp, "%u %s"), &expected_rt, input_expr) != EOF) {
  ... // 对于expected_rt 和 input_expr做处理即可
}
```

Q: 



`strtol()` : 将str 转换为一个 long

`strcmp()` return 0 => equal 



出现了Divide by zero error

这个error 没有被strtol() 中的 assert() catch到的话 说明是在某一个中间的计算过程产生的 有没有必要对于所有的中间计算结果都用double 来表示 只在最后一步的时候使用int 来截取返回结果呢? 





按照PA的要求需要使用无符号运算 

PA的表达式求值中两个蓝框思考题

1. 为什么要使用无符号类型?
2. 除0的确切行为



如果再表达式求值过程中出现了除0的行为 编译器会报错 warning: 

`warning: division by zero [-Wdiv-by-zero]`

可以考虑根据编译器的报错来进行过滤?



https://stackoverflow.com/questions/818255/in-the-shell-what-does-21-mean

`2 > &1`

`&` indicates that what follows and precedes is a file descriptor and not a file name

File descriptor 1 is the standard output(`stdout`)

File descriptor 2 is the standard error(`stderr`)



用什么command来run整个项目?

`make ISA=x86 run`



如何来run整个的项目? 





3.7 现在报错的内容是什么? 

Evaluation



需要保证生成的测试表达式本身就是合法的 如何进行catch呢? 

测试的时候 生成随机表达式的规则 生成代码的规则







现在修改的文件都是干什么用的? 



对于表达式的evaluation是在哪个文件里发生的?



*main.c* : 

*src/monitor/debug/expr.c* : 

*tools/gen-expr/gen-expr.c* : 生成表达式的 如何生成 需要注意什么

*test.c* : 测试c文件语法的



Failed to evaluate the expression, 将不同的test case的表达值



有没有可以参考的解决方案? 



## Debug



报错: Segmentation Fault

算法:



进行随机表达式测试

如何生成一些随机的表达式

测试通过判断的依据



解析流程: 



* 处理括号 ( )
  * 括号会改变优先级
  * 括号可能不匹配

* 处理运算符 + - * /
  * 运算符有不同的优先级
  * 除法运算需要check 除0操作	

* 处理数字 
  * 整数溢出怎么办? 什么时候会有整数溢出
  * 全部默认的是无符号数字，和有符号数的区别是什么? 如何处理有符号数字
  * 如何处理负数? 如何区分减号和负号?
  * 
* 处理空格





如何确定我的代码是对的，尽可能多的做单元测试?

有一个while 死循环 指针一直没有往后移动

中间过程出现了0之后没有进行处理

token解析过程中地址覆盖的问题 会共享同样的地址吗? 如何来进行清除? 



## Command

### PA1 - GDB Command



如何进入Command Line 

如何在调试过程中 展示源码

打断点



单步调试

跳到下一个断点 

monitor 监视点功能



### Linux Command

`lscpu` 查看本机的CPU内核数





install `.deb` file

`sudo apt install ./name.deb`  必须要加./来从

`google-chrome --version` google chrome浏览器是有命令行command

### Vim Command



ctrl + B: 向上一页

ctrl + F: 向下一页

ctrl + D: 向下半页



### Chrome Command

* 切换到下一个标签页 
  * Windows: 同时按下`Ctrl+Tab`
  * Mac: `Command + Option + ←`

* 切换到之前一个标签页
  * Windows: 同时按下 `Ctrl+Shift+Tab`
  * Mac: `Command + Option + ←`



## 心路历程

3.7 pick up 之前的内容 需要重新梳理目前的进展 有点麻烦



## 参考资料

[CMU SEI C Standard Page](https://wiki.sei.cmu.edu/confluence/display/c/SEI+CERT+C+Coding+Standard)



C++
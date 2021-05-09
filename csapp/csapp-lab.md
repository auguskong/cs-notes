## **Bomb Lab**



配套学习材料: 



+ Docker + 配套答案: https://zhuanlan.zhihu.com/p/104130161
+ Recitation(16 Spring): https://www.cs.cmu.edu/afs/cs/academic/class/15213-s16/www/recitations/recitation04-bomblab-s16.pdf
+ Jump 指令集: http://unixwiz.net/techtips/x86-jumps.html 
+ X86汇编指令集: https://zhuanlan.zhihu.com/p/53394807
+ GDB调试:
  + GDB中应该知道的几个调试方法-酷壳 https://coolshell.cn/articles/3643.html
  + https://www.cnblogs.com/laizhenghong2012/p/10126096.html
  + 100个gdb 小技巧: https://wizardforcel.gitbooks.io/100-gdb-tips/content/info-frame.html





### **Phase 1**

破解答案: Border relations with Canada have never been better.

直接判断两个字符串是否相等 读0x402400地址上面存的字符串即可 用gdb 命令





### **Phase 2**



破解答案: 3 256 (不唯一 是一组数字)

push的话表示重新开一个栈空间 不共享rsp, 如果不push清理的话就直接共享当前的rsp



read_six_numbers 里面调用了炸弹 也需要分析



cmp DWORD PTR[rsp], 0x1  -> rsp = 1 表示从rsp 向后开始读取一个double word(一个word表示一个字长 == 2byte)

cmp DWORD PTR[rbx], eax -> 



64位机器指的是: CPU的通用寄存器(General Purpose Registers) 的位数是64bit



传进去的都是char 





si 执行下一行代码 ni下一个函数 c: 直接跳转到下一个断点  

加断点  b *0x[address]

查看全部断电信息 info break
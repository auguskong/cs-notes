



https://www.bilibili.com/video/BV1iW411d7hd?p=5



Machine Lebel Program - 1

![image-20210505215622395](/Users/xiangyu/Library/Application Support/typora-user-images/image-20210505215622395.png)



```
movq $0x4, %rax    temp = 0x4  // 本地变量指向的是register, 临时存储
movq $-147, (%rax)  *p = -147  // 指针指向的是memory, 非临时存储

```


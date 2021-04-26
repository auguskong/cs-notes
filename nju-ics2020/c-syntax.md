**循环**

生成无限循环?

**指针**

定义指针 指针是有类型的 根据所指向的对象来确定

```c
char *Ptr
```

\```c

\```

打印指针的地址 `%p`

打印指针所指向的对象的值

指针存的是所指向对象的地址

指针的指针存的是指针的地址

指针与数组

当数组作为一个值传给一个函数function的时候，其实传的是指针

\```c

\#include <stdio.h>

void min(int a[]) {

printf("min sizeof(a)=%lu\n", sizeof(a));

}

int main() {

int a[] = {1,2,3};

printf("main sizeof(a)=%lu\n", sizeof(a));

min(a);

return 0;

}

//result:

\> main sizeof(a)=12 数组的长度3个int 每个int占4个字节 3*4 = 12个字节

\> min sizeof(a)=8 指针的长度8个字节

\```

**字符串**

如何在c中表示一个字符串?

如何表示一个字符串数组?

字符串常用函数

**GCC编译器**
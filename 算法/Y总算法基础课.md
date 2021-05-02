

主要思想

背下来: 能够快速写出来然后调试通过



提高熟练度的方法: 写完一遍调试了之后 删除 在重新写一遍 重复3-5遍



## 基础算法(一)



### 排序



* 快排

  * 确定分界点 l (l + r) / 2  r

  * 调整区间: 小于等于 x 的在左半边 大于等于x的在右半边

  * 递归处理左右两个区间

    ```c++
    #include <iostream>
    
    using namespace std;
    
    const int N = 1e6 + 10;
    
    int n;
    int q[N];
    
    void quick_sort(int q[], int l, int r)
    {
        // when l == r 只有一个数字 不需要排序 直接return
        if (l >= r) return;
        
        int x = q[(l + r) >> 1], i = l - 1, j = r + 1;
        while (i < j)
        {
          	// 如果i都是小于x的话 符合条件 向右移动 
            // 指针移动的条件是 < x 不能是 <=x 会死循环
            do i ++; while (q[i] < x);
          	// 如果j指向的数字都是大于x的话 符合条件 向左移动
            do j --; while (q[j] > x);
            // 坑: swap 是有前提条件 i < j 如果i > j 表示走到了最后一个元素 当前i指向的数字可能比j指向的数字大 不应该交换
            if (i < j) swap(q[i], q[j]);
        }
        
        quick_sort(q, l, j);
        quick_sort(q, j + 1, r);
    }
    
    int main()
    {
      	// 直接用scanf 来读数据 不需要进行n = 赋值操作
        scanf("%d", &n);
        for (int i = 0; i < n; i++) scanf("%d", &q[i]);
        
        quick_sort(q, 0, n - 1);
        
        for (int i = 0; i < n; i++) printf("%d ", q[i]);
        
        return 0;
    }
    
    ```
    
    

* 归并

  * 确定分界点 固定index mid = (l + r) / 2

  * 递归排序 左半边区间 和 右半边区间

  * 归并 将两个小区间合并为一个区间

    ```c++
    #include <iostream>
    
    using namespace std;
    
    const int N = 1000010;
    
    int n;
    int q[N], tmp[N];
    
    // 数组定义是 q[] 
    void merge_sort(int q[], int l, int r)
    {
        if (l >= r) return;
        
        int mid = l + r >> 1;
        
        merge_sort(q, l, mid), merge_sort(q, mid + 1, r);
        
      	// 注意这里的i 是从l开始的 只是数组区间上的某一段起点 不能从0开始
        int k = 0, i = l, j = mid + 1;
      	// 当两个指针都没有走到小区间的终点
        while (i <= mid && j <= r) {
            if (q[i] <= q[j]) {
                // 这里需要对i进行++操作 赋值之后右移
                tmp[k++] = q[i++];
            } else {
              	// j赋值之后右移
                tmp[k++] = q[j++];
            }
        }
      	// 当i和j中某一个走到重点之后，直接将小区间中的剩余的数字依次加入到大区间中
        while (i <= mid) tmp[k++] = q[i++];
        while (j <= r) tmp[k++] = q[j++];
        
      	// 将数字从tmp中放回到原来的数组中
      
      	// 为什么这里i是从l开始 而j是从0开始的?  因为tmp在每一次递归都是从0开始进行赋值,而我们的q数组在不同的递归方法之间是共享的
        for (i = l, j = 0; i <= r; i++, j++) q[i] = tmp[j];
    }
    
    int main() {
        // 先读入输入的数据个数
        scanf("%d", &n);
        for (int i = 0; i < n; i++) {
            scanf("%d", &q[i]);
        }
        merge_sort(q, 0, n - 1);
        
        for (int i = 0; i < n; i++) {
            printf("%d ", q[i]);
        }
        return 0;
    }
    ```
    



### 二分



```c++

// 二分模板
bool check(int x) {
  
}

用来找右边区间的最左边的端点 mid不需要使用 + 1
区间被划分成[l, mid] 和 [mid + 1, r]
int bsearch_1(int l, int r) {
  while (l < r) {
    int mid = l + r >> 1;
    if (check(mid)) r = mid;
    else l = mid + 1;
  }
  return l;
}

用来找到左边区间的最右边的端点 mid需要 + 1
区间被划分成[l, mid - 1] 和 [mid, r]
int bsearch_2(int l, int r) {
  while (l < r) {
    int mid = l + r + 1 >> 1;
    if (check(mid)) l = mid;
    else r = mid - 1;
  }
  return l;
}
```





* 例题: 数的范围 https://www.acwing.com/problem/content/791/

```c++
#include <iostream>

using namespace std;

const int N = 100010;
int n, m, x;
int q[N];

int main() {
    scanf("%d%d", &n, &m);
    for (int i = 0; i < n; i++) {
        scanf("%d", &q[i]);
    }
    
    while (m-- > 0) {
        int l = 0, r = n - 1;
        scanf("%d", &x);
        while (l < r) {
            int mid = l + r >> 1;
            if (q[mid] >= x) {
                r = mid;
            } else {
                l = mid + 1;
            }
        }
        
      // 如果没有找到当前元素 直接返回 -1 -1即可
        if (q[l] != x) {
            cout << "-1 -1" << endl;
        }
        else {
          
          // 这里打印的是第一个位置 先不换行
            cout << l << ' ';
    
            int l = 0, r = n - 1;
            while (l < r) {
              // 找右端点的时候需要进行+1操作
                int mid = l + r + 1 >>1;
                if (q[mid] <= x) {
                    l = mid;
                } else {
                    r = mid - 1;
                }
            }
            
          // 这里打印的是第二个位置 l已经被更新过了
            cout << l << endl;
        }
    }
    
    return 0;
}
```





## 基础算法(二) - [Video](https://www.acwing.com/video/11/)



### 前缀和和差分 



举例子:

\```

a = {1, 3, 7}

b = {1, 2, 4}

1 = 1

3 = 1 + 2

7 = 1 + 2 + 4

\```

b数组是a数组的差分

a数组是b数组的前缀和

\```math

a_{i} = b_{1} + b_{2} + \dots + b_{i}

\```



差分的作用: 通过修改b数组来快速处理操作对于a数组中的给定区间[l, r]的所有数字都要加上c的操作。

如果有很多的操作的话，暴力做是O(n)的，用差分做的话是O(1)

\```math

b_{l} + c \to a_{l} + c, a_{l + 1} + c \dots a_{n} + c

\```

需要在`$b_{l} + c$`的同时进行`$b_{r + 1} - c` 来终止加c的效果,注意检查越界

例题:

[Corporate Flight Bookings](https://leetcode.com/problems/corporate-flight-bookings)

数学知识

1.素数的判定-试除法

2.分解质因数-试除法(跳过)

3.筛法判定质数

质数(素数): 在大于1的整数中，如果只包含1和本身这两个约数

O(sqrt(n)) 试除法判断素数的方法

原理: 如果d能够被n整除，那么n/d 也一定能被n整除，因为除法的结果都是成对出现的

\```c++

bool is_prime(int n) {

if (n < 2) {

return false;

}

for (int i = 2; i <= n / i; i++) {

if (n % i == 0) {

return false;

}

}

return true;

}

\```

从数开始 删掉每个数的所有倍数

如果p仍然存在的话，[2, p-1] 中不存在任何一个数是p的

\```c++

int primes[N], count;

bool st[N];

void get_primes(int n) {

for (int i = 2; i <= n; i++) {

if (!st[i]) {

primes[cnt++] = n;

}

for (int j = 0; primes[j] <= n / i; j++) {

st[primes[j] * i] = true;

if (i % primes[j] == 0) {

break;

}

}

}

}

\```

调和级数 和为 `$\ln{n}$`

\```math

1 + \frac{1}{2} + \frac{1}{3} + \dots + \frac{1}{n}

\```

\```java

class Solution {

public int countPrimes(int n) {

boolean[] notPrime = new boolean[n + 1];

if (n <= 1) {

return 0;

}

int count = 0;

for (int i = 2; i < n; i++) {

if (!notPrime[i]) {

count++;

}

for (int j = i; j <= n / i; j++) {

notPrime[j * i] = true;

}

}

return count;

}

}

\```



Week7 基本数据结构
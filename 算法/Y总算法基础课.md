

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



### 前缀和



* 一维数组前缀和

  计算数组区间[l, r]: $S_r - S_{l-1}$

  

  ```c++
  #include <iostream>
  
  const int N = 100010;
  
  int n, m;
  int a[N], s[N];
  
  int main() {
  
      scanf("%d %d", &n, &m);
    
      // 下标直接从 1 开始取值 这样后面用到i - 1的时候不会越界
      for (int i = 1; i <= n; i++) scanf("%d", &a[i]);
      
      for (int i = 1; i <= n; i++) s[i] = s[i - 1] + a[i];
      
      while (m--) {
          int l, r;
          scanf("%d %d", &l, &r);
          printf("%d\n", s[r] - s[l - 1]);
      }
  }
  ```

* 二维矩阵前缀和

  

  x1, y1 是矩阵左上角的坐标
  
  x2, y2 是矩阵右上角的坐标
  
  构造矩阵前缀和: $S_{i, j-1} + S_{i-1,j} - S_{i-1, j-1} + a_{i, j}$
  
  
  
  计算矩阵区间: $S_{x_2y_2} - S_{x_2,y_1-1} - S_{x_1-1,y_2} + S_{x_1-1,y_1-1}$
  
  
  
  注意这里是x2 y1 和 x1 y2混用来找到小矩阵的位置 
  
  ```c++
  #include <iostream>
  
  using namespace std;
  
  const int N = 1010;
  int n, m, q;
  int a[N][N], s[N][N];
  
  int main() {
      scanf("%d%d%d", &n, &m, &q);
      
      // 数组下标是从1开始的, 可以处理边界
      for (int i = 1; i <= n; i++) {
          for (int j = 1; j <= m; j++) {
              scanf("%d", &a[i][j]);
          }
      }
      
    	// 用两个小矩阵相加 减去重叠
      for (int i = 1; i <= n; i++) {
          for (int j = 1; j <= m; j++) {
              s[i][j] = s[i - 1][j] + s[i][j - 1] - s[i - 1][j - 1] + a[i][j];
          }
      }
      
      while (q--) {
          int x1, x2, y1, y2;
          scanf("%d%d%d%d", &x1, &y1, &x2, &y2);
        	// 大矩阵的前缀和减去两个小矩阵 加回重叠的部分
          printf("%d\n", s[x2][y2] - s[x2][y1 - 1] - s[x1 - 1][y2] + s[x1 - 1][y1 - 1]);
      }
  }
  ```
  
  







### 差分 



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





### 双指针算法



#### 基本模板

```c++
for (int i = 0, j = 0; i < n; i++) {
  while (j < i && check(i, j)) {
    j++;
  }
  
  // 题目的具体逻辑
}
```



#### 最长连续不重复子序列

```c++

// 我的实现
#include <iostream>

using namespace std;

const int N = 100010;

int n;

int q[N], s[N];

int main() {
    scanf("%d", &n);
    for (int i = 0; i < n; i++) {
        scanf("%d", &q[i]);
    }
    
    int r = 0;
    // 输入的是有序的吗? 不一定
    // 开一个数组 因为这里有前提条件是所有的输入数字都在[0, 10000]的区间内 存一下当前已经走过的元素 出现次数加1
    for (int i = 0, j = 0; i < n; i++) {
        while (j < n && s[q[j]] == 0) {
            // 这里注意操作顺序是先计数 出现次数+1 然后进行比较 再将指针右移
            s[q[j]]++;
            r = max(j - i + 1, r);
            j++;
        }
        s[q[i]]--;
    }
    
    printf("%d", r);
}
```





#### 数组元素的目标和

```c++
#include<iostream>

using namespace std;

const int N = 100010;

int n, m, x;

int a[N], b[N];

int main () {
    scanf("%d%d%d", &n, &m, &x);
    for (int i = 0; i < n; i++) {
        scanf("%d", &a[i]);
    }
    
    for (int i = 0; i < m; i++) {
        scanf("%d", &b[i]);
    }
    
    for (int i = 0, j = m - 1; i < n; i++) {
        while (j > 0 && a[i] + b[j] > x) {
            j--;
        }
        if (a[i] + b[j] == x) {
            printf("%d %d", i, j);
            break;
        }
    }
    
    return 0;
}
```



### 位运算



最常用的两个基本操作





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



```
```



1 + \frac{1}{2} + \frac{1}{3} + \dots + \frac{1}{n}



```java
```



class Solution {

​	https://www.bilibili.com/video/BV1iW411d7hd?p=5

}



\```



Week7 基本数据结构



## 动态规划(一)



### 背包问题



#### 0/1 背包



i不是第i件  而是前i件



```c++
// 朴素版 二维
#include <iostream>
#include <algorithm>

using namespace std;

const int N = 1010;

int n, m;
int v[N], w[N];
int f[N][N];

int main() {
    cin >> n >> m;
    
    for (int i = 1; i <= n; i++) cin >> v[i] >> w[i];
    
    for (int i = 1; i <= n; i++) {
        for (int j = 1; j <= m; j++) {
            f[i][j] = f[i - 1][j];
            if (j >= v[i]) {
                f[i][j] = max(f[i - 1][j], f[i - 1][j - v[i]] + w[i]);
            }
        }
    }
    
    cout << f[n][m] << endl;
    
    return 0;
}

// 一维数组只存体积就可以
#include <iostream>
#include <algorithm>

using namespace std;

const int N = 1010;

int n, m;
int v[N], w[N];
int f[N];

int main() {
    cin >> n >> m;
    
    for (int i = 1; i <= n; i++) cin >> v[i] >> w[i];
    
    for (int i = 1; i <= n; i++) {
        for (int j = m; j >= v[i]; j--) {
            f[j] = max(f[j], f[j - v[i]] + w[i]);
        }
    }
    
    cout << f[m] << endl;
    
    return 0;
}

a.cpp:18:48: error: no matching function for call to 'max(int [1010], int*)'
   18 |             f[j] = max(f[j], f[j - v[i]] + w[i]);

记得要把二维数组的定义改成一维的 不然会有报错
```





### 线性DP



按照一种线性关系来进行递推


最长上升子序列
=======


#### 数字三角形

题目: https://www.acwing.com/problem/content/900/



```c++
// 我的实现

基本思路: 
1. 从最下层的数字向上走 (这样最后只需要返回f[1][1]即可)
  1. 最下层的元素直接复制原数组最下层
  2. 非最下层的其他元素f[i][j]只能有两个选项 f[i + 1][j] 同列 f[i + 1][j] 靠右的一列
2. f[i][j] 表示的是从最底层走到当前位置的
  
#include <iostream>
using namespace std;

const int N = 510;
int n;
int f[N][N], q[N][N];

int main() {
    scanf("%d", &n);
    for (int i = 1; i <= n; i++) {
        for (int j = 1; j <= i; j++) {
            scanf("%d", &q[i][j]);
        }
    }
    
    for (int i = 1; i <= n; i++) {
        f[n][i] = q[n][i];
    }
    for (int i = n - 1; i >= 1; i--) {
        for (int j = 1; j <= i; j++) {
            f[i][j] = max(f[i + 1][j], f[i + 1][j + 1]) + q[i][j];
        }
    }
    printf("%d", f[1][1]);
    return 0;
}

```



#### 最长上升子序列

题目: https://www.acwing.com/problem/content/897/



```c++
// 我的实现

基本思路: 
1. f[i] 表示以第i个数字结尾的最长递增子序列
2. 从前向后依次遍历每个数字 重新检查当前位置之前的所有元素 如果有更长的上升序列就比较并更新 f[i] 和 max, 没有就保留原来的最长序列 
3. 

#include <iostream>
using namespace std;

const int N = 1010;
int n;
int q[N], f[N];

int main() {
    int res = 0;
    scanf("%d", &n);
    for (int i = 1; i <= n; i++) {
        scanf("%d", &q[i]);
    }
    
    for (int i = 1; i <= n; i++) {
        f[i] = 1;
    }
    for (int i = 1; i <= n; i++) {
        for (int j = 1; j <= i; j++) {
            if (q[i] > q[j]) {
                f[i] = max(f[i], f[j] + 1);
                res = max(f[i], res);
            }
        }
    }
    
    printf("%d", res);
}
```



最长公共子序列





动态规划(二)视频: https://www.acwing.com/video/35/



### 区间DP



#### 合并石子 

#### 石子合并

题目: https://www.acwing.com/problem/content/284/

视频讲解: https://www.acwing.com/video/943/

```c++
基本思路: 

1. 用数组来表示dp 将数组分隔成不同的区间 
  按照区间划分的临界点 来作为遍历对象 
  集合表示的是所有将[L, R]这个区间中的石子合并成一堆的方案的集合
  
  f[L, k] 本身是左边集合的最小值 而f[k + 1, R]是右边集合的最小值 相互之间没有重叠是独立的，所以可以直接进行求和操作。合并操作的代价是S[R] - S[L - 1]
  转移方程是 f[L, k] + f[k + 1, R] + S[R] - S[L - 1]
```



活动打卡: https://www.acwing.com/activity/content/11/

要求的是只能合并相邻集合




=======
区间DP的固定遍历模式,先枚举区间长度

```c++
for (int len = 2; len <= n; len++) 
  // 遍历区间端点
  for (int l = 1; l + len - 1 <= n; l++)
    
```



```c++
// 我的实现

#include <iostream>
using namespace std;

const int N = 310, INF = 1e9;

int n;
int q[N], s[N], f[N][N];

int main() {
    cin >> n;
    for (int i = 1; i <= n; i++) cin >> q[i];
    for (int i = 1; i <= n; i++) s[i] = s[i - 1] + q[i];
    
    for (int len = 2; len <= n; len++) {
        for (int l = 1; l + len - 1 <= n; l++) {
            int r = l + len - 1;
            f[l][r] = INF;
            
            for (int k = l; k <= r; k++) {
                // 前缀和是谁的前缀? 合并区间(一个部分区间) 堆的和
                f[l][r] = min(f[l][r], f[l][k] + f[k + 1][r] + s[r] - s[l - 1]);
            }
        }
    }
    
    printf("%d", f[1][n]);
    
    return 0;
}
```




### 计数类DP



### 数位统计DP



### 状态压缩DP



### 树形DP



### 记忆化搜索



#### 滑雪



表示所有从点(i, j) 开始滑的路径 属性是Max 

`f[i][j]` :



状态计算:  

前提条件: 

当前点还没有被计算过

四个方向中高度更小的情况下



```c++
// 我的实现

#include <iostream>
#include <cstring>
#include <algorithm>

using namespace std;

const int N = 310;

int n, m;
int f[N][N], h[N][N];

int dx[4] = {0, 0, -1, 1}, dy[4] = {1, -1, 0, 0};



int dfs(int x, int y) {

    if (f[x][y] != -1) {
        return f[x][y];
    }
    
    f[x][y] = 1;
    for (int i = 0; i < 4; i++) {
        int nx = x + dx[i];
        int ny = y + dy[i];
        if (nx > 0 && nx <= n && ny > 0 && ny <= m && h[nx][ny] < h[x][y]) {
            f[x][y] = max(f[x][y], dfs(nx, ny) + 1); // 这个地方应该继续搜下去 而不是直接用f[nx][ny]中存的值
        }
    }
    
    return f[x][y];
}

int main() {
    scanf("%d %d", &n, &m);
    
    for (int i = 1; i <= n; i++) {
        for (int j = 1; j <= m; j++) {
            scanf("%d", &h[i][j]);
        }
    }
    
    memset(f, -1, sizeof f);
    
    int res = 1;
    for (int i = 1; i <= n; i++) {
        for (int j = 1; j <= m; j++) {
            res = max(res, dfs(i, j));
        }
    }
    printf("%d", res);
    
    return 0;
}
```


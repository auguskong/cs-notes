





```c++
// c++ stdin/stdout
#include <iostream>

using namespace std;

int main () {
    int a, b;
    cin >> a >> b;
    cout << a + b << endl;
    return 0;
}


// c stdin/stdout
#include <stdio.h>

int main()
{
    int a, b;
    scanf("%d%d", &a, &b);
    printf("%d\n", a + b);
    return 0;
}



```



```python
# Python3 stdin/stdout
import sys

for line in sys.stdin:
    print(sum(map(int, line.split())))
```



```java
// Java stdin/stdout
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String args[]) throws Exception {
        Scanner cin = new Scanner(System.in);
        var a = cin.nextInt();
        var b = cin.nextInt();
        System.out.println(a + b);
    }
}
```



c++ namespace: 



类型转换? 

```c++
// 打卡1 A+B
#include <iostream>

int main() {
    int a, b;
    scanf("%d %d", &a, &b);
    printf("%d", a + b);
}

// 打卡2 差
#include <iostream>

using namespace std;

int main() {
    int a, b, c, d;
    cin >> a >> b >> c >> d;
    cout << "DIFERENCA = " << a*b - c*d << endl;
    return 0;
}

// 打卡3 圆的面积 
// 整数乘法/浮点数乘法会有区别 需要用到double 类型
// 如何使用cout 来保留四位小数？

#include <iostream>

using namespace std;
#define PI 3.14159 // 定义一个宏 取常数

int main() {
    double r;
    cin >> r;
    printf("A=%.4lf",PI*r*r); // 保留四位小数的long float %.4lf
    return 0;
}

// 打卡4 平均数
#include <iostream>

using namespace std;

int main() {
    double a, b;
    cin >> a >> b;
    printf("MEDIA = %.5lf", (3.5/11*a+7.5/11*b)); // 这里面注意权重的取值
    return 0;
}

// 打卡5 工资
#include <iostream>

using namespace std;

int main() {
    int n, h;
    double s;
    cin >> n >> h >> s;
    printf("NUMBER = %d\n", n);
    printf("SALARY = U$ %.2lf", h*s);
    return 0;
}

// 打卡6 油耗
#include <iostream>

using namespace std;

int main() {

    double dis, gas;
    cin >> dis >> gas;

    printf("%.3lf km/l", dis/gas);
    return 0;
}

// 打卡7 两点间的距离
#include <iostream>
#include <math.h>

using namespace std;

int main() {
    double x1, y1, x2, y2;
    cin >> x1 >> y1 >> x2 >> y2;

    printf("%.4lf", sqrt(pow((x2 - x1), 2) + pow((y2 - y1), 2)));
    return 0;
}
```




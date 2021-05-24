## 21.5.17



https://leetcode.com/problems/flatten-binary-tree-to-linked-list/



```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def flatten(self, root: TreeNode) -> None:
        """
        Do not return anything, modify root in-place instead.
        """
        if root == None:
            return
        self.flatten(root.left)
        if root.left:
            curr = root.left
            while curr.right:
                curr = curr.right
            curr.right = root.right
            root.right = root.left
            root.left = None
        self.flatten(root.right)
        
```



```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    void flatten(TreeNode* root) {
        if (!root) {
            return;
        }
        TreeNode* curr = NULL;
        TreeNode* next = root->right;
        flatten(root->left);
        if (root -> left) {
            curr = root->left;
            while (curr->right) {
                curr = curr->right;
            }
            curr->right = next;
            root->right = root->left;
            root->left = NULL;
        }
        flatten(root->right);
    }
};
```



```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public void flatten(TreeNode root) {
        TreeNode curr = null;
        if (root == null) {
            return;
        }
        flatten(root.left);
        TreeNode next = root.right;
        if (root.left != null) {
            curr = root.left;
            while (curr.right != null) {
                curr = curr.right;
            }
            curr.right = next;
            root.right = root.left;
            root.left = null;
        }
        flatten(root.right);
    }
}
```



### 138. Copy List with Random Pointer

https://leetcode.com/problems/copy-list-with-random-pointer



题目里面给出的表示是index 但是实际上random还是一个指针，需要用一个HashMap<Node, Node> 来进行copy 不能用HashMap<Integer, Node> 因为会存在重复元素 Integer 作为key是没有办法区分相同val的元素的

random 

```java
/*
// Definition for a Node.
class Node {
    int val;
    Node next;
    Node random;

    public Node(int val) {
        this.val = val;
        this.next = null;
        this.random = null;
    }
}
*/

class Solution {
    public Node copyRandomList(Node head) {
        if (head == null) {
            return null;
        }

        Node copyHead = new Node(head.val);
        Node curr = copyHead;
        Node currHead = head;
        HashMap<Node, Node> map = new HashMap<>();

        while (currHead != null) {
            map.put(currHead, curr);
            if (currHead.next != null) {
               curr.next = new Node(currHead.next.val); 
            }
            curr = curr.next;
            currHead = currHead.next;
        }
        curr = copyHead;
        currHead = head;
        while (currHead != null) {
            if (currHead.random != null) {
                curr.random = map.get(currHead.random);
            }
            curr = curr.next;
            currHead = currHead.next;
        }
        
        return copyHead;
    }
}
```









```Python
"""
# Definition for a Node.
class Node:
    def __init__(self, x: int, next: 'Node' = None, random: 'Node' = None):
        self.val = int(x)
        self.next = next
        self.random = random
"""

O(2n) 解法 遍历两次list 第一次先把所有的Node都copy并且添加到dict当中
class Solution:
    def copyRandomList(self, head: 'Node') -> 'Node':
        copy = dict()
        m = n = head
        while m:
            copy[m] = Node(m.val)
            m = m.next
        while n:
            copy[n].next = copy.get(n.next)
            copy[n].random = copy.get(n.random)
            n = n.next
        return copy.get(head)


# O(n) 解法 用到了defaultdict 没有看懂 先跳过
class Solution:
    def copyRandomList(self, head: 'Node') -> 'Node':
        copy = collections.defaultdict(lambda: Node(0))
        copy[None] = None
        n = head
        while n:
            copy[n].val = n.val
            copy[n].next = copy[n.next]
            copy[n].random = copy[n.random]
            n = n.next
        return copy[head]
        
```





## 430. Flatten a Multilevel Doubly Linked List



递归 flatten

如果child != null 

https://leetcode.com/problems/flatten-a-multilevel-doubly-linked-list/



Double Linked List 专门用来增加麻烦的 每个Node上都需要处理next 和 prev两个指针

```python
"""
# Definition for a Node.
class Node:
    def __init__(self, val, prev, next, child):
        self.val = val
        self.prev = prev
        self.next = next
        self.child = child
"""

class Solution:
    def flatten(self, head: 'Node') -> 'Node':
        if head == None or (head.child == None and head.next == None):
            return head
        n = head;
        while n:
            if n.child:
                n.child = self.flatten(n.child)
                tail = n.child
                while tail and tail.next:
                    tail = tail.next
                tail.next = n.next
                if n.next:
                    n.next.prev = tail
                n.next = n.child
                n.child.prev = n
                n.child = None #这里需要将child指针指向None
            n = n.next
        return head
    
```



### 21.5.18



Topological Sort 基本模板





```c++
int h[N], e[N], ne[N], idx;

void add(int a, int b) {
  e[idx] = b, ne[idx] = h[a], h[a] = idx++;
}

idx = 0;
memset(h, -1, sizeof h);

bool topsort() {
  
  // hh 表示的是head 头结点
  int hh = 0, tt = -1;
  
  // d[i] 存点i的入度
  for (int i = 1; i <= n; i++) {
    if (!d[i])
      q[++ tt] = i; // 这里的q数组是用来模拟队列queue的
  }
  
  while (hh <= tt) {
    int t = q[hh++];
    for (int i = h[t]; h != -1; i = ne[i]) {
      int j = e[i];
      if (-- d[j] == 0) {
        q[+= tt] = j;
      }
    }
  }
  
  return tt == n - 1;
}
```





Y总的模板里面是用了数组来模拟单链表

这里的index是表示第几个边 

h 是存点



构造一个indegree 数组 在数组中记录节点的入度 

使用一个queue来将所有入度为0的记录一下 并按照顺序进行遍历 如果最后所有的node都遍历了 表示存在一个topological order 否则就不存在





### Course Schedule

使用拓扑排序模板 本质是按照一个特定的顺序来遍历整个的图 先处理入度为0的点 然后将相连的节点的度数减1 之后依次处理其他的点

```java
import java.util.Arrays;


class Solution {
    public static int N = 100010;
    public static int idx = 0;

    public static int[] h = new int[N]; 
    public static int[] e = new int[N];
    public static int[] ne = new int[N];
    // int[] h, e, ne = new int[N];

    void add(int a, int b){
        e[idx] = b;
        ne[idx] = h[a];
        h[a] = idx++;
    }
    
    public boolean canFinish(int nc, int[][] p) {
        for (int i = 0; i < N; i++) {
            h[i] = -1;
        }
        int complete = 0;
        int[] d = new int[nc];
        
        for (int i = 0; i < p.length; i++) {
            d[p[i][0]]++;
            add(p[i][1], p[i][0]);
        }
        
        Queue<Integer> q = new LinkedList<>();
        for (int i = 0; i < nc; i++) {
            if (d[i] == 0) {
                q.add(i);
                complete++;
            }
        }
    
        while (!q.isEmpty()) {
            int curr = q.poll();
            for (int i = h[curr]; i != -1; i = ne[i]) {
                int j = e[i];
                if (-- d[j] == 0) {
                    q.add(j);
                    complete++;
                }
            }
        }
        
        return complete == nc;
    }
}
```





```python
class Solution:
    def canFinish(self, n: int, p: List[List[int]]) -> bool:
        G = [[] for i in range(n)] #直接一行生成邻接矩阵
        d = [0] * n
        for b, a in p:
            G[a].append(b)
            d[b] += 1
        
        queue = [] #用一个list来作为queue
        for i in range(n):
            if d[i] == 0:
                queue.append(i)
        complete = 0
        
        while queue:
            c = queue.pop(0) #从queue中弹出元素使用pop
            complete += 1
            for ad in G[c]:
                d[ad] -= 1
                if d[ad] == 0:
                    queue.append(ad)
        
        return complete == n
```



### Course Schedule II

用一个list 来记录从queue中pop 出来的course, 最后记得check是否存在topological sort 如果存在的话 再返回res, 不存在的话直接return []

```python
class Solution:
    def findOrder(self, n: int, p: List[List[int]]) -> List[int]:
        G = [[] for i in range(n)] #直接一行生成邻接矩阵
        d = [0] * n
        for b, a in p:
            G[a].append(b)
            d[b] += 1
        res = []
        queue = [] #用一个list来作为queue
        for i in range(n):
            if d[i] == 0:
                queue.append(i)
        complete = 0
        
        while queue:
            c = queue.pop(0) #从queue中弹出元素使用pop
            complete += 1
            res.append(c)
            for ad in G[c]:
                d[ad] -= 1
                if d[ad] == 0:
                    queue.append(ad)
        if complete == n:
            return res
        return []

```



## 21.5.19

### Backtracking 

N queens

开额外的数组来记录位置上的信息



 根据是否允许重复来

#### Combination Sum



```java
List<List<Integer>> res = new ArrayList<List<Integer>>();

不能声明 List<List<Integer>> res = new ArrayList<ArrayList<Integer>>(); 

不能直接声明 new List<Integer>() 因为List是一个抽象类 必须要有具体的实例才行
  
  List<List<Integer>> res = new ArrayList<List<Integer>>();

System.out.println("currSum: %d" + currSum); 用+号来进行concanate 打印结果出来 不能用逗号分隔 不支持println(Stirng, int)操作
  
  class Solution {
    public List<List<Integer>> combinationSum(int[] nums, int t) {
        List<List<Integer>> res = new ArrayList<List<Integer>>();
        if (nums.length == 0)  {
            return res;
        }
        dfs(nums, t, 0, 0, new ArrayList<Integer>(), res);
        return res;
    }
    
    public void dfs(int[] nums, int t, int idx, int currSum, List<Integer> currList, List<List<Integer>> res) {
        if (currSum > t && !currList.isEmpty()) {
            return;
        }
        else if (currSum == t) {
            res.add(new ArrayList<>(currList));
            return;
        }
        else{
            for (int i = idx; i < nums.length; i++) {
                currList.add(nums[i]);
                dfs(nums, t, i, currSum + nums[i], currList, res);
                currList.remove(currList.size() - 1);
            }
        }
    }
}
```





```python
class Solution:
    def combinationSum(self, nums: List[int], t: int) -> List[List[int]]:
        res = []
        self.dfs(nums, t, 0, 0, [], res, 1)
        return res;
        
    def dfs(self, nums: List[int], t: int, start: int, currSum: int, currList: List[int], res: List[List[int]], d: int):
        # print(d, " level: ", " " * 2 * d, "start: ", start)
        if currSum > t:
            return
        elif currSum == t:
            # print(currList)

            res.append(currList[:])
            return
        else:
						# 这里的enumerate 的起点要从start开始 这样下标是和原数组元素保持一致的
            for i, num in enumerate(nums[start :], start=start):
                currList.append(num)
                self.dfs(nums, t, i, currSum + num, currList, res, d + 1)
                del currList[-1]
        
```





添加的是空list是因为没有使用new 关键字添加新的list





debug的时候 怀疑哪里有问题就直接打印出来那部分即可 

打印的时候可以使用template语法



直接在dfs里面有for loop 就不需要在外面加新的 

每一个

Subset

Word Search



和树上的DFS调用



树上的DFS调用

指针操作 + 递归 + Queue/Stack 的使用来进行特定顺序的记录





为什么最后返回的是空的list 呢? 感觉和 del currList[-1] 有关系? 

为什么会将[2, 2, 3] 给替换了呢? 加进去之后应该会一直保留的呀? 



```python
class Solution:
    def combinationSum(self, nums: List[int], t: int) -> List[List[int]]:
        res = []
        self.dfs(nums, t, 0, 0, [], res)
        print("res after dfs: ", res)
        return res;
        
    def dfs(self, nums: List[int], t: int, start: int, currSum: int, currList: List[int], res: List[List[int]]):
        print("res: ", res)
        if currSum > t:
            return
        elif currSum == t:
            print(currList)
            res.append(currList)
            print("res: ", res)
            return
        else:
            for i, num in enumerate(nums[start :]):
                currList.append(num)
                self.dfs(nums, t, i, currSum + num, currList, res)
                # print("res after dfs: ", res)
                del currList[-1]
        
在哪里发生了替换操作? append是存了个指针 没有存拷贝 

```



`enumerate` 会默认每次从0开始做标记 return an enumerate object



```python
>>> seasons = ['Spring', 'Summer', 'Fall', 'Winter']
>>> list(enumerate(seasons))
[(0, 'Spring'), (1, 'Summer'), (2, 'Fall'), (3, 'Winter')]
>>> list(enumerate(seasons, start=1))
[(1, 'Spring'), (2, 'Summer'), (3, 'Fall'), (4, 'Winter')]

def enumerate(sequence, start=0):
    n = start
    for elem in sequence:
        yield n, elem
        n += 1
```



数组/字符串中的递归调用



直接append的话 是没有进行copy操作的 如果之后currList被修改了 res中的List也会被修改 可以通过打印地址来进行验证 

```python
res.append(currList)


# copy a new list
res.append(currList[:])

# print out the addres of object
print(id(object))
```



打印n个space 

```python
print(" " * n)
```



使用`str.format() `来进行格式替换

```python
print("{}. {} appears {} times.".format(i, key, wordBank[key]))
```





#### Combination Sum II

每个数字只能使用一次



input: [1,2,3,1,5] target: 4

[[1,1,2], [1,3]]

可以出现[1,1,2] 这种存在多个相同数字的结果, 但是只能出现一次 去重的意思是要求重复数字只使用一次 



```python

# 这个循环不work 的原因在于 i+=1 并不影响 for 循环中i的遍历 for 循环

for i in range(len(nums)):
            while i > start and nums[i] == nums[i - 1]:
                print(i)
                continue
            currList.append(nums[i])
            self.dfs(nums[i+1 :], t, i + 1, currSum + nums[i], currList, res)
            del currList[-1]
            
          
```



去重一次是不够的 需要一直用while loop 跳过多个相同数字



#### Subset

无重复数组

```python
class Solution:
    def subsets(self, nums: List[int]) -> List[List[int]]:
        res = []
        self.dfs(nums, 0, [], res)
        return res
    
    def dfs(self, nums: List[int], start: int, path: List[int], res: List[List[int]]):
        if (start > len(nums)):
            return
        else:
            res.append(path)
        for i in range(start, len(nums)):
            path.append(nums[i])
            self.dfs(nums, i + 1, path[:], res)
            del path[-1]
        
```





#### Subset II

有重复数字

```python
class Solution:
    def subsetsWithDup(self, nums: List[int]) -> List[List[int]]:
        res = []
        nums.sort()
        self.dfs(nums, 0, [], res)
        return res
    
    def dfs(self, nums: List[int], start: int, path: List[int], res: List[List[int]]):
        if (start > len(nums)):
            return
        else:
            res.append(path)
        for i in range(start, len(nums)):
            if i > start and nums[i] == nums[i - 1]:
                continue
            path.append(nums[i])
            self.dfs(nums, i + 1, path[:], res)
            del path[-1]
```



跳过重复元素即可 不需要重新append 只需要第一个重复元素 正常append 得到subset 即可 

[1, 2, 2]

for i in range(start, len(nums))

1 直接append

dfs(nums, 0, [], res)

​	dfs(nums, 1, [1], res) 

​		dfs(nums, 2, [1, 2], res)

 			dfs(nums, 3, [1, 2, 2], res)

​	dfs(nums, 2, [2], res)

​        dfs(nums, 3, [2, 2], res) -> 将[2, ,2]加到res之后 for loop 不执行 return 回到上一层





5.21 



这两个是背包问题的变体 物品 重量/体积  价值 

求最大 方案数 

Combination Sum III

https://leetcode.com/problems/combination-sum-iii/

Combination Sum IV 

https://leetcode.com/problems/combination-sum-iv/



背包问题还可以用滚动数组优化 



#### Combinations

https://leetcode.com/problems/combinations/submissions/



和subset 类似 只是return的条件有点区别

dfs search 就是穷举 把所有的状态都搜一遍



```python
class Solution:
    def combine(self, n: int, k: int) -> List[List[int]]:
        res = []
        self.dfs(n, k, 1, [], res)
        return res
    def dfs(self, n: int, k: int, start: int, path: List[int], res: List[List[int]]):
        if len(path) == k:
            res.append(path)
        for i in range(start, n + 1):
            path.append(i)
            self.dfs(n, k, i + 1, path[:], res)
            del path[-1]
        
```



#### Permutations

https://leetcode.com/problems/permutations/

每个元素都可以选择取/不取 不需要添加start 直接从头开始遍历整个list 即可

```python
class Solution:
    def permute(self, nums: List[int]) -> List[List[int]]:
        res = []
        used = [False] * len(nums)
        self.dfs(nums, used, [], res)
        return res
    
    def dfs(self, nums: List[int], used: List[bool], path: List[int], res: List[List[int]]):
        if len(path) == len(nums):
            res.append(path)
            return
        for i in range(len(nums)):
            if not used[i]:
                path.append(nums[i])
                used[i] = True
                self.dfs(nums, used, path[:], res)
                del path[-1]
                used[i] = False
        
        
```


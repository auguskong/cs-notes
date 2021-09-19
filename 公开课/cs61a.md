



Website: https://inst.eecs.berkeley.edu/~cs61a/fa20/ 2020Fall

# Lab

```pyt
f = max() 

max 是内置函数
```

integer division // 

Floor division (`//`): divides the first number by the second and then rounds down, evaluating to an integer





```
def twenty_twenty():
    """Come up with the most creative expression that evaluates to 2020,
    using only numbers and the +, *, and - operators.

    >>> twenty_twenty()
    2020
    """
    return ______
```



The lines in the triple-quotes `"""` are called a **docstring**, which is a description of what the function is supposed to do. When writing code in 61A, you should always read the docstring!

The lines that begin with `>>>` are called **doctests**. Recall that when using the Python interpreter, you write Python expressions next to `>>>` and the output is printed below that line. Doctests explain what the function does by showing actual Python code. It answers the question: "If we input this Python code, what should the expected output be?"



Python Coding Style: https://inst.eecs.berkeley.edu/~cs61a/fa20/articles/composition.html





print 和 return 有区别

```python
>>> def how_big(x):
...     if x > 10:
...         print('huge')
...     elif x > 5:
...         return 'big'
...     elif x > 0:
...         print('small')
...     else:
...         print("nothin")
>>> how_big(7)
? big
-- Not quite. Try again! --

? 'big'
-- OK! --

>>> how_big(12)
? 'huge'
-- Not quite. Try again! --

? huge
-- OK! --
```









```python
>>> print(print(1), print(2))
1
2
None None

# The special value None represent Nothing in Python 
# A function that does not explicitly return return a value will return None
```

![image-20210521153014007](C:\Users\bjfuk\AppData\Roaming\Typora\typora-user-images\image-20210521153014007.png)



variable name 需要在envirotnment / context中 来确定真正的含义

An environment is a sequence of frames. 

A name evaluates to the value bound to that name in the earliest frame of the current environment in which that name is found

![image-20210521153431357](C:\Users\bjfuk\AppData\Roaming\Typora\typora-user-images\image-20210521153431357.png)



```python
False values in Python: False, 0, '', None
True values in Python: Anything else (True)
while 0 是False 
其他数字都是True 包括负数

'''
To evaluate the expression <left> and <right>:

Evaluate the subexpression <left>.
If the result is a false value v, then the expression evaluates to v.
Otherwise, the expression evaluates to the value of the subexpression <right>.
To evaluate the expression <left> or <right>:

Evaluate the subexpression <left>.
If the result is a true value v, then the expression evaluates to v.
Otherwise, the expression evaluates to the value of the subexpression <right>.
To evaluate the expression not <exp>:

Evaluate <exp>; The value is True if the result is a false value, and False otherwise.
'''

>>> True and 13
? True
-- Not quite. Try again! --

? 13
-- OK! --

>>> False or 0
? 0
-- OK! --

>>> not 10
? False
-- OK! --

>>> not None
? True
-- OK! --

```

`python3 ok -q sum_digits --trace`: look at an environment diagram to investigate a failing test for question



convert int to string count the number 



## Lab 2

assignment 就是直接赋值

def 就是指针声明



知识点

### Lambda

基本定义: 

![cs61a-Lambda](D:\repos\cs-notes\公开课\screenshot\cs61a-Lambda.PNG)





```python
Q: When is the return expression of a lambda expression executed?
A: When the function returned by the lambda expression is called.

>>> b = lambda x: lambda: x  # Lambdas can return other lambdas!
>>> c = b(88)
>>> c
? Function
-- OK! --

>>> c() # the function is called
? 88
-- OK! --

>>> d = lambda f: f(4)  # They can have functions as arguments as well
>>> def square(x):
...     return x * x
>>> d(square)
? 16
-- OK! --


>>> higher_order_lambda = lambda f: lambda x: f(x)
>>> g = lambda x: x * x
>>> higher_order_lambda(2)(g)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "<stdin>", line 1, in <lambda>
TypeError: 'int' object is not callable
>>>

def curry2(f):
    def g(x):
        def h(y):
            return f(x, y)
        return h
    return g

curry2 = lambda f: lambda x: lambda y: f(x, y)
```



### Decorator

```python
# Python provides special syntax to apply higher-order functions as part of executing a def statement, called a decorator. Perhaps the most common example is a trace.

>>> def trace(fn):
        def wrapped(x):
            print('-> ', fn, '(', x, ')')
            return fn(x)
        return wrapped
>>> @trace
    def triple(x):
        return 3 * x
>>> triple(12)
->  <function triple at 0x102a39848> ( 12 )
36
```



#### Q2: WWPD: Higher Order Functions

```python
>>> def cake():
...    print('beets')
...    def pie():
...        print('sweets')
...        return 'cake'
...    return pie
>>> chocolate = cake()
? beets
-- OK! --

>>> chocolate
? Function
-- OK! --

>>> chocolate()
(line 1)? sweets
(line 2)? cake
-- Not quite. Try again! --

(line 1)? sweets
(line 2)? 'cake'
-- OK! --

>>> more_chocolate, more_cake = chocolate(), cake
? sweets
-- OK! --

>>> more_chocolate
? sweets
-- Not quite. Try again! --

? Function
-- Not quite. Try again! --

? 'cake' # more_chocolate 是 chocolate()执行之后的结果 只保留了return语句中的 'cake'
-- OK! --
```



`is` 变量绑定的对象 

`==` : 检查值是否相等

```python
l1 = []
l2 = []
l3 is l1>>> l1 = []
>>> l2 = []
>>> l3 is l1
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'l3' is not defined
>>> l3 = l1
>>> l1 == l2
True
>>> l1 is l2
False
>>> l1 is l3
True
>>> l1 == l3
True
```



strat0 = lambda score, opponent: 1 - opponent // 10

这里要先算除法  然后再算减法 opponent == 0 的时候 结果是1



为什么both() 会交替输出? 因为print() 有自动换行? 

是在两个不同的print function 当中 所以调用的时候会直接换行

test 07的时候出问题 原因是因为 06 没有写完 醉了！！ 注意保证自己调用的dependency function都是work的

## Lab 4

max_subseq

```python
def max_subseq(n, t):
    """
    Return the maximum subsequence of length at most t that can be found in the given number n.
    For example, for n = 20125 and t = 3, we have that the subsequences are
        2
        0
        1
        2
        5
        20
        21
        22
        25
        01
        02
        05
        12
        15
        25
        201
        202
        205
        212
        215
        225
        012
        015
        025
        125
    and of these, the maxumum number is 225, so our answer is 225.
    >>> max_subseq(20125, 3)
    225
    >>> max_subseq(20125, 5)
    20125
    >>> max_subseq(20125, 6) # note that 20125 == 020125
    20125
    >>> max_subseq(12345, 3)
    345
    >>> max_subseq(12345, 0) # 0 is of length 0
    0
    >>> max_subseq(12345, 1)
    5
    """
    if n == 0 or t == 0:
        return 0
    with_last = max_subseq(n // 10, t - 1) * 10 + n % 10
    without_last = max_subseq(n // 10, t)
    return max(with_last, without_last)

```



我的思路是先for loop 找最大如果最大的满足要求 这个思路不是一个recursion的思路 recursion的思路更像是 

这里的base case 除了找到了最长的有效长度t 还需要考虑n == 0的时候 

如何不断地缩小范围: 不断地进行除法操作来去掉最后一位数字 

这里面构造数字的时候是用到了 * 10操作 将不同位数上的数字等比例放大 



## Lab 5

对应课本Chapter 2

知识点:

* Sequence
  * Sequence Iteration
  * Sequence Processing
  * Sequence Abstraction

```python
>>> [2, 7] + digits * 2
[2, 7, 1, 8, 2, 8, 1, 8, 2, 8]
# list 本身也可以进行*2 操作 

# for statement
for <name> in <expression>:
    <suite>
<expression> 必须yield an iterable value
```



sprout_leaves

没有加到原来的t上 应该是local 和 global 的区别

可变对象和不可变对象在传递值的时候会有区别

可变对象使用引用传递 直接修改相同的地址上的

```python

if is_leaf(t):
    for i in range(len(leaves)):
        # 这里如果直接用leaves 来进行操作的话 会导致tree()的嵌套 [2,5] [[2], [5]] [[[2]],[[5]]] 因为都是作用在同一个list leaves上的
        leaves[i] = tree(leaves[i])
        t = tree(label(t), leaves)
        return t
```



https://docs.python.org/3/faq/programming.html



## Lab 6



### 知识点

* **Nonlocal**: A variable is **nonlocal** to a frame if it is defined in the environment that the frame belongs to but not the frame itself, i.e. in its parent or ancestor frame.

* **Mutability**

  * *mutable*: an object is mutable if its state can change as code is executed

  * *mutation*: process of changing an object's state 

  * **==** vs. **is**

    * **==** check if two expressions evaluate to **equal** values

    * **is** check whether two expressions evaluate to the **same** values

      ```python
      >>> lst1 = [1, 2, 3, 4]
      >>> lst2 = [1, 2, 3, 4]
      >>> lst1 == lst2
      True
      >>> lst1 is lst2
      False
      
      # when we mutate an object, we simply change its state, not its identity
      >>> lst1 = [1, 2, 3, 4]
      >>> lst2 = lst1
      >>> lst1.append(5)
      >>> lst2
      [1, 2, 3, 4, 5]
      >>> lst1 is lst2
      True
      ```

      



### Q1: Make Adder Increasing

如何确定adder被call了几次呢?  肯定是要用一个count变量来记录的

count需要使用non local 这样才能跳出限制看到adder

每一次被call直接加到a上面就行了 不需要另外使用一个count变量来记录

```python
def make_adder_inc(a):
    """
    >>> adder1 = make_adder_inc(5)
    >>> adder2 = make_adder_inc(6)
    >>> adder1(2)
    7
    >>> adder1(2) # 5 + 2 + 1
    8
    >>> adder1(10) # 5 + 10 + 2
    17
    >>> [adder1(x) for x in [1, 2, 3]]
    [9, 11, 13]
    >>> adder2(5)
    11
    """
    "*** YOUR CODE HERE ***"
    def adder(x):
        nonlocal a
        res = a + x
        a += 1
        return res

    return adder
```



### Q2: Next Fibonacci

make_fib() 没有给出参数n 怎么声明nonlocal 变量？ 

`SyntaxError: no binding for nonlocal 'n' found`

`SyntaxError: name 'n' is parameter and nonlocal`

直接用两个变量来进行操作 不要用function call



### Q3: List-Mutation

Python Mutable Sequence Types Doc: https://docs.python.org/3/library/stdtypes.html#mutable-sequence-types

```python
>>> lst = [5, 6, 7, 8]
>>> lst.append(6)
? Nothing
______

>>> lst
? [5, 6, 7, 8, 6]
______

>>> lst.insert(0, 9)
>>> lst
? [9, 5, 6, 7, 8, 6]
______

>>> x = lst.pop(2)
>>> lst
? [9, 5, 7, 8, 6]
______

>>> lst.remove(x)
>>> lst
? [9, 5, 7, 8]
______

>>> a, b = lst, lst[:]
>>> a is lst
? True
______

>>> b == lst
? True
______

>>> b is lst
? False
______
```





### Q4: Insert Items





## Lab 7 



Topics:

* Iterators
  *  We define an iterable as an object on which calling the built-in function `iter` function returns an iterator
* Generators
* OOP



WWPD

### Q3

```

case 1
>>> deneros_car = Car('Tesla', 'Model S')
>>> deneros_car.model
______

>>> deneros_car.gas = 10
>>> deneros_car.drive()
______

>>> deneros_car.drive()
______

>>> deneros_car.fill_gas()
______

>>> deneros_car.gas
______

>>> Car.gas
______


case 2
>>> deneros_car = Car('Tesla', 'Model S')
>>> deneros_car.wheels = 2
>>> deneros_car.wheels
______

>>> Car.num_wheels
______

>>> deneros_car.drive()
______

>>> Car.drive()
______

Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: drive() missing 1 required positional argument: 'self'

>>> Car.drive(deneros_car)
______


case 3
>>> deneros_car = MonsterTruck('Monster', 'Batmobile')
>>> deneros_car.drive()
______

Vroom! This Monster Truck is huge!
'Monster Batmobile goes vroom!' 

# print() 和 return 的输出结果不一样 print()的输出不需要加 ''

>>> Car.drive(deneros_car)
______

'Monster Batmobile goes vroom!'

>>> MonsterTruck.drive(deneros_car)
______

>>> Car.rev(deneros_car)

Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
AttributeError: type object 'Car' has no attribute 'rev'

rev(self) 只在MonsterTruck class当中定义了 
```



```python
Traceback (most recent call last):
  File "/mnt/d/repos/cs61a-2020fall/lab07/classes.py", line 89, in __init__
    self.hand.append(self.deck[0])
TypeError: 'Deck' object is not subscriptable
```

What does it mean if a Python object is "subscriptable" or not?

https://stackoverflow.com/questions/216972/what-does-it-mean-if-a-python-object-is-subscriptable-or-not



```py
# built-ins that are subscriptable
string:  "foobar"[3] == "b"
tuple:   (1,2,3,4)[3] == 4
list:    [1,2,3,4][3] == 4
dict:    {"a":1, "b":2, "c":3}["c"] == 3
```



Deck class 中已经实现了一个`draw()` method



用`pop`从list当中取出并删除元素

# Project

`()`: 得到generator

`[]`: 得到一个新的List

## Project 1- cats

```python
def about(topic):
    """Return a select function that returns whether a paragraph contains one
    of the words in TOPIC.

    >>> about_dogs = about(['dog', 'dogs', 'pup', 'puppy'])
    >>> choose(['Cute Dog!', 'That is a cat.', 'Nice pup!'], about_dogs, 0)
    'Cute Dog!'
    >>> choose(['Cute Dog!', 'That is a cat.', 'Nice pup.'], about_dogs, 1)
    'Nice pup.'
    """
    assert all([lower(x) == x for x in topic]), 'topics should be lowercase.'
    # BEGIN PROBLEM 2
    "*** YOUR CODE HERE ***"

    def select(paragraph):
        paragraph = lower(paragraph)
        # 调用split(remove_punctuation(paragraph)) 传入的是相同的paragraph参数 有点functional programming的感觉了 不同的function之前可以嵌套
        words = split(remove_punctuation(paragraph))
        for t in topic:
            if t in words:
                return True
        return False

    return select
```



注意取两个list中长度较短的 

typed_words == [] 的时候直接return 0.0 来避除0错误

Problem 4 

等于1的时候是否可以?



## Project 2 - 

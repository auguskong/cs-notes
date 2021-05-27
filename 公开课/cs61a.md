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


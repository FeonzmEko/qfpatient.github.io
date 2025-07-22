# cs61a 2020 fall
### 2025/7/21: 
* 学习了`func` 和 `control`

### 2025/7/22:
* 判断中函数和控制语句的区别，调用`if_`函数时中每个都会计算，而不像判断语句进入条件分支
```python
def if_(c,t,f) :
    if c :
        return t
    else :
        return f
    
from math import sqrt

def real_sqrt(x) :
    return if_(x >= 0,sqrt(x),0)

real_sqrt(-4)
```
* 使用高阶函数来实现重复的逻辑，减少代码冗余，类似于`c++`中的模板
```python
def identity(k):
    return k

def cube(k):
    return pow(k,3)

def summation(n,term):
    """Sum the first N terms of a sequence
    
    >>> summation(5,cube)
    225
    """
    total, k = 0, 1
    while k <= n:
        total, k = total + term(k), k + 1
    return total

def sum_naturals(n):
    """Sum of the first N natural numbers.

    >>> sum_naturals(5)
    15
    """
    return summation(n,identity)

def sum_cubes(n):
    """Sum of the first N cube numbers.

    >>> sum_naturals(5)
    225
    """
    return summation(n,cube)

print(sum_naturals(5))
print(sum_cubes(5))
```
* 返回值为函数的高阶函数,下面的例子构造了一个`+3`的加法器
```python
def  make_adder(n) :
    """
    >>> add_three = make_three(3)
    >>> add_three(4)
    7
    """

    def adder(k) :
        return k+n
    return adder
```
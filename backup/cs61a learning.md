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
* 断言`assert`,其实就是偷懒版的`if`语句
```python
from math import pi

def area_circle(r):
    assert r > 0,'A lengath must be positive'
    return pi*r*r

area_circle(-1)
```
会出现以下报错
```shell
Traceback (most recent call last):
  File "d:\code\py\CS61A\CS61A-Assignments-main\test\7.22.py", line 20, in <module>
    area_circle(-1)
  File "d:\code\py\CS61A\CS61A-Assignments-main\test\7.22.py", line 17, in area_circle
    assert r > 0,'A lengath must be positive'
           ^^^^^
AssertionError: A lengath must be positive
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
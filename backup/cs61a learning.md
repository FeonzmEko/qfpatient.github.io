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
* 断言`assert`
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
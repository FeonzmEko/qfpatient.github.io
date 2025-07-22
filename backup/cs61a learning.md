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
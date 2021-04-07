# Python Modules - functools

[[Python Modules]]

---

## reduce 函数

`functools.reduce(fun,seq)` 将一个接受 **2 个参数**的函数 *fun* 以**累积**的方式从左到右依次作用到一个可迭代对象 *seq* 的所有元素上.

最简单的, 如**累加**, **连乘**等效果:

```py
import functools
seq = [1,2,3,4,5,6,7,8,9]
print(functools.reduce(lambda x,y: x+y, seq))
print(functools.reduce(lambda x,y: x*y, seq))
```

返回 $1+...+9 = 45$ 和 $1\cdot 2\cdots 9 = 362880$

[//begin]: # "Autogenerated link references for markdown compatibility"
[Python Modules]: Python Modules "Python Modules"
[//end]: # "Autogenerated link references"
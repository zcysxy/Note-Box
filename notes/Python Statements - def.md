# Python Statements - def

[[Python Statements]] | [[Python Functions]] | [[Python Keywords]]

---

## 基本语法

```py
def fun(arg1,...):
    '''documentation
    string'''
    function block
    return
```

## 参数 Attributes

* *arg1* 等括号内参数为==形参==, 函数调用时向其传递==实参==
* 一个函数可以没有形参 (括号 `()` 必须要有), 表示该函数不接受参数
* ++参数命名要符合变量命名同样规则++
* 形参其实为函数内部**中间变量**, 在函数执行结束后自动移除
* 实参向形参的传递实为**赋值**, 故若实参为**可变对象**, 且函数执行过程中++形参发生**原地**改变, 则对应实参也会改变++

    ```py
    >>> a = [1,2,3]
    >>> def test(b):
    ...     b.append('HA')
    ...
    >>> test(a)
    >>> print(a)
    [1, 2, 3, 'HA']
    ```

    * 仅限**原地改变**, 若对形参重新赋值, 则赋值后的操作不再对实参有影响

        ```py
        >>> a = [1,2,3]
        >>> def test(b):
        ...     b = b + ['HA']
        ...
        >>> test(a)
        >>> print(a)
        [1, 2, 3]
        ```

* 调用函数时实参可与形参同名, 因为它们属于不同的缓存空间
    * 形参在函数执行结束后自动移除
    * 如下图, 三个 %x% 都不同, 函数调用时两个 %x% 都独立地改变了, 但都不影响主函数空间地 %x%
    ![20201202203617](https://raw.githubusercontent.com/zcysxy/Figurebed/master/img/20201202203617.png)
* 函数参数种类可以分为: 普通参数, 默认值参数, 关键参数, 可变长度参数等
* 函数定义时无需指定参数类型或需要填入的数据类型, 应有**调用者**决定和判断

### 默认值参数

* 语法: `def fun(arg=default)`
* 若默认值参数与**普通参数**混用, 则任何一个默认值参数右边不能再有普通参数, 否则报错
* 调用带有默认值参数的函数时, 可以不对默认值参数进行赋值, 也可以赋值

#### 默认值参数陷阱

默认值参数如果使用不当, 会导致很难发现的逻辑错误, 例如:

```py
>>> def test(newitem, old_list=[]):
...     old_list.append(newitem)
...     return old_list
...
>>> print(test('a'))
['a'] # 正确
>>> print(test('b'))
['a','b'] # 错误
```

可以发现, 第二次调用函数值, 未给默认值参数赋值, 但默认值参数的实际值从设置的默认值 `[]` 变成了上次调用的结果 `['a']`.

原因是当一个函数有的某个默认参数默认值为**可变类型** (dict, list 等)时, 该默认值参数**只初始化**一次, 之后的每次操作, 都在前一次的操作基础上操作. 对于不可变类型的默认值参数 (tuple, string, int 等) 不会有这种情况.

于是上例可以改成:

```py
>>> def test(newitem, old_list=None):
...     if old_list == None:
...         old_list = []
...     old_list.append(newitem)
...     return old_list
...
>>> print(test('a'))
['a'] # 正确
>>> print(test('b'))
['b'] # 正确
```

!! 可以使用方法 `fun.__defaults__` 查看函数 *fun* 的默认参数的当前值

### 可变长度参数

* 语法: `def fun(*p)` 和 `def fun(**p)`
* 前者将**多个**实参合并为一个**元组**传递给 *p*; 后者将**多个键值对**合并为一个**字典**传递给 *p*
    * 键值对的格式与字典中的不同, 应该是: `fun(arg1=x1,arg2=x2,...)`
        * 其中 *arg1* 无需为字符串, 传递给 *p* 的时候自动转换为字符串
* 故若可变长度参数与其他参数混用时, 最好将它们放在**最右端**, 因为它们会将调用函数时某个实参之后所有的参数**合并**
* 混合使用例子:

    ```py
    >>> def test(a,b,c=3,*p,**h):
    ...     print(a,b,c)
    ...     print(p)
    ...     print(h)
    ...
    >>> test(1,2,4,4,5,6,7,x='hello',y=13,z=['W'])
    1 2 4
    (4,5,6,7)
    {'x':'hello', 'y':13, 'z':['w']}
    ```

!! 注意: 因为函数调用时[[Python Functions#关键参数|关键参数]]和可变长度字典参数的语法一样, 所以要避免字典中的键与关键参数的键同名

## 函数注释 Description

* 其中函数注释 *documentation string* 会在函数被调用时作为提示
    ![20201202194555](https://raw.githubusercontent.com/zcysxy/Figurebed/master/img/20201202194555.png)
    * 单引号也可

## 变量作用域

见 [[Python Scope]]

## Function Recursion

函数递归, 或递归函数, 即**在函数定义中调用自身**, 递归的思想同数学中的一致.

递归函数设计中最重要的是**递归终点**的设置.

最简单的例子 --- 整数阶乘:

```py
def f(n):
    if n == 0 or n == 1: # **递归终点**
        return 1
    return n * f(n-1)
```

若没有设置合适的递归终点, 则在调用函数时会抛出异常 **RecurssionError**.

### Examples

1. Greatest Common Divisor
    * 思想: $d|a, d|b \Rightarrow d|\max\{a-b,b-a\}$, 进而, $d=\text{gcd}(a,b) \Rightarrow d = \text{gcd}(\min\{a,b\},\max\{a-b,b-a\})$

    ```py
    def gcd(a,b):
        if a==b: # 递归终点
            return a
        else:
            return gcd(min(a,b),max(a-b,b-a))    
    ```

2. Fibonacci Sequence
    * 定义: $$fib(n) = \begin{cases}
        1, &n=1,2\\[2ex]
        fib(n-1) + fib(n-2), &n>2\\
    \end{cases} $$

    ```py
    def fib(n):
        if n == 1 or n == 2:
            return 1
        else:
            return fib(n-1) + fib(n-2)
    ```

3. 回文判断

    ```py
    def mirror(s):
        if s == '':
            return True
        elif s[0] != s[-1]:
            return False
        else:
            return mirror(s[1:-1])
    ```

4. [[Binary Search Algorithm]]

    ```py
    def bi_search(l,key,start,end):
        if start > end:
            return -1
        m = (start + end) // 2
        if key == l[m]:
            return m
        elif key < l[m]:
            return bi_search(l,key,start,m-1)
        else:
            return bi_search(l,key,m+1,end)
    ```

5. 质因数分解

    ```py
    def factorization(n):
        m = int(n**(1/2)) + 1
        for k in range(2,m):
            if n % k == 0:
                factors = [k]
                factors.extend(factorization(n//k))
                return factors
        return [n] # 递归终点, 即无非自身的质因数
    ```

6. 全排列

    ```py
    def permutation(l):
        '''l 是一个列表, 返回其元素的全排列列表'''
        if len(l) == 1:
            return [l]
        else:
            ans = []
            for i in range(len(l)):
                y = l.copy()
                item = y.pop(i)
                subPers = permutation(y)
                for each in subPers:
                    ans.append([item] + each)
            return ans
    ```

7. 原地逆序排列

    ```py
    def myReverse(l):
        def subReverse(l,start,end):
            if start < end:
                l[start], l[end] = l[end], l[start]
                subReverse(l, start+1, end-1)
        subReverse(l,0,len(l)-1)
    ```

8. 原地升序排列

    ```py
    def increase(l):
        def subIncrease(l,start,end):
            if start < end:
                t = l[start]
                move = 0
                for i in range(end-start):
                    if t > l[start+i+1]:
                        l.insert(start, l.pop(start+i+1)) # 将比 l[start] 小的元素排到它的左边去
                        move += 1
                subIncrease(l,start,start + move-1)
                subIncrease(l,start + move+1, end)
        subIncrease(l,0,len(l)-1)
    ```

## Other

* 若程序中定义了多个重名函数, 则**后面**的函数定义会取代**前面**的
* [[Python Statements - return|return]] 语句定义函数的返回操作并跳出函数, 非必需
* 可以有**嵌套函数定义**, 即函数定义中定义子函数并调用

[//begin]: # "Autogenerated link references for markdown compatibility"
[Python Statements]: Python Statements "Python Statements"
[Python Functions]: Python Functions "Python Functions"
[Python Keywords]: Python Keywords "Python Keywords"
[Python Scope]: Python Scope "Python Scope"
[//end]: # "Autogenerated link references"
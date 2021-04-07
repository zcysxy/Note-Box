---
alias:异常处理
---
# Python Exception Handling

[[Python]]

---

* 简单地说, 异常 exception 是指程序**运行时**引发的错误 error
* Python 程序运行时检测到一个错误 error 后, 解释器 interpreter 就会指出当前流无法继续执行下去, 即抛出异常 exception, 显示错误信息
* 如果这些错误得不到正确的处理将会**导致程序终止运行**, 而合理地使用异常处理结果可以使得程序更加健壮, 具有更强的**容错性**, 不会因为用户不小心的错误输入或其他运行时原因而造成程序终止
* 也可以使用异常处理结构为用户提供更加友好的提示
* 异常是指因为程序出错而在**正常控制流以外**采取的行为
    * 代码中的**语法错误**和**逻辑错误**不属于异常, 因为它们在控制流之内, 但它们可能导致异常
* 异常处理的使用范围：
    * [[Python Statements - def|函数定义]]
    * 主流程
    * **嵌套异常处理** (较少使用)

## 异常种类

> 仅常用异常种类, 详见[官方文档](https://docs.python.org/3/library/exceptions.html#exception-hierarchy)

* BaseException **所有内置异常**的统称
    * ArithmeticError
        * OverflowError 过量运算 (非内存不足导致)
        * ZeroDivisionError 除零错误
    * LoopError
        * IndexError 索引错误
        * KeyError 字典键错误
    * OSError
        * FileExistsError 文件已存在 (创建时)
        * FileNotFoundError 文件不存在 (打开时)
        * ConnectionError 网络异常
    * NameError 变量名字错误 (如变量不存在)
    * SyntaxError 语法错误
    * TypeError 类型错误
    * ValueError 值错误 (如传递参数时类型正确但不再取值范围内)
    * AssertionError [断言](#断言-assertion)错误, [[Python Statements - assert|assert]] 语句抛出的异常
    * RecursionError 超出[[Python Functions#Function Recursion|递归]]最大深度
    * KeyboardInterrupt 用户中断执行 (通常是输入^C)
    * EOFError input 函数未读取所需对象
    * IOError 输入/输出操作失败
    * SystemError 系统错误
    * MemoryError磁盘空间不足

以上展示了异常的 **class hierarchy** 结构, BaseException 是所有异常的 base class, 所以能接受所有异常. 同理底层的异常类能接受其包括的子异常, 反之则不能.

## 异常预防

### 无条件循环

利用 [[Python Statements - while|while]] 循环, 在无条件循环 `while True:` 语句下处理可能出现异常的内容, 当内容执行正常无异常时通过 [[Python Statements - break|break]] 语句跳出循环块.

❌ **缺点**:

* `while True:` **无条件循环**是个很**危险**的语句, 有可能造成**死锁**而无任何提示
* `while True:` 只相当于一个异常处理容器, 实质的异常处理还要另行设计

**例子** --- 检验用户合法输入:

```py
while True:
    s = input('请输入两个数(以逗号, 分割)')
    if s.fint(',') == -1: # find 方法未找到时返回 -1
        continue
    t = s.split(',')
    if len(t) != 2:
        continue
    areAllDigit = False
    for each in t:
        if not each.isdigit():
            break
    else:
        areAllDigit = True
    if areAllDigit:
        break
x,y = eval(s)
print('其算术平均值为 %.2f .' (x+y)/2)
```

可以看出, 仅使用 `while True` 语句处理异常是非常繁琐的, 而且上面的代码还无法识别浮点数, 复数等非整数数值.

### 正则表达式

对于**用户输入**等字符串不合法产生的异常, 经常可以利用 [[Python Modules - re|re 模块]]通过 [[Regular Expression]] 来**防止**出现异常.

如上例可改为:

```py
import re
patStr = r'^\s*[+|-]?\d+(\.\d+)?\s*,\s*[+|-]?\d+(\.\d+)?\s*$'
pattern = re.compile(patStr)
s = input('请输入两个数(以逗号, 分割)')
while not pattern.match(s):
    s = input('请输入两个数(以逗号, 分割)')
x.y = eval(s)
print('其算术平均值为 %.2f .' % ((x+y)/2))
```

✅ 优点:

* 更加简洁, 通适
* 可以使用 `while not patthern.match(s)` 语句防止使用无条件循环

❌ 缺点:

* 正则表达式只能检验字符串, 处理字符串相关异常, 而且也不能处理更复杂的字符串
* 构造正则表达式仍比较麻烦

## 异常处理

以上都是异常**预防**手段, 而 [[Python Statements - try|try]], [[Python Statements - except|except]] 等语句用于**异常处理**, 即若无此语句, 则运行代码时会抛出异常.

异常处理分为两个阶段:

1. **引发**异常
2. 检测并处理异常

关于异常的**引发**, 自然出现错误时会自动引发异常, 也可以通过 [[Python Statements - raise|raise]] 语句显式地引发异常.

由于异常处理要比异常预防地效率更低, 所以应该避免过多地依赖异常处理机制, 也不要使用异常处理来替代常规的异常预防检查, 如 *if*...*else* 语句

### 异常处理流程

异常处理完整的语句流程为: [[Python Statements - try|try]] --> [[Python Statements - except|except]] --> [[Python Statements - else|else]] --> [[Python Statements - finally|finally]]

```py
try:
    body
except ExceptionA:
    handler1
except ExceptionB:
    handler2
...
except ExceptionN:
    handlerN
except:
    handlerExcept
else:
    processElse
finally:
    processFinally
```

对应流程图如下:

![20201210145404](https://raw.githubusercontent.com/zcysxy/Figurebed/master/img/20201210145404.png)

* 其中 [[Python Statements - else|else]] 和 [[Python Statements - finally|finally]] 语句都非必需
    * 因为 *else* 语句紧接着 *try* 语句的 *body*, 故可以直接将 *processElse* 合并到 *body* 中
    * *finally* 是在所有 *try*, *except*, *else* 执行完后**一定**会执行的语句, 不管前面有没有报错.
* 若 *body* 中的异常不属于 {*ExceptionA*,...,*ExceptionN*}, 则执行 *handlseExcept*
    * 此时若没有最后一个 *except* 语句, 则抛出异常

因此最简单的异常处理结构为:

```py
try:
    body
except:
    handlerExcept
```

又最简单的异常处理语句块为 [[Python Statements - pass|pass]] 语句, 这也体现了 [[Python Statements - pass|pass]] 语句的主要功能: 跳过未完成/未完善的语句块. 于是当我们并没有想好会出现什么样的异常, 或着如何处理时, 可用 [[Python Statements - pass|pass]] 语句处理异常.

### 异常处理中的异常

异常处理结构 ([[Python Statements - try|try blocks]]) 也有可能出现异常. 此类异常会有特殊的提示, 如下

```py
try:
    a = 1/0
finally:
    print(a)
```

报错为:

```txt
Traceback (most recent call last):
  File "d:/OneDrive1/Desktop/temp/temp.py", line 8, in <module>
    a = 1/0
ZeroDivisionError: division by zero

During handling of the above exception, another exception occurred:

Traceback (most recent call last):
  File "d:/OneDrive1/Desktop/temp/temp.py", line 10, in <module>
    print(a)
NameError: name 'a' is not defined
```

可以用嵌套异常处理来处理异常处理中的异常 (不建议), 否则程序终止并报错.

## *断言 Assertion

断言 assertion, 即 [[Python Statements - assert|assert]] 语句执行的特殊的**异常处理**方式.

[//begin]: # "Autogenerated link references for markdown compatibility"
[Python]: Python "Python"
[//end]: # "Autogenerated link references"
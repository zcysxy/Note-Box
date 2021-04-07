# Python Functions - eval

[[Python Function]]

* 返回字符串 **[[Python Expressions|表达式]]** 的值
    * 表达式可以很简单, 如 `'[1,2,3]'`, 则直接返回**列表** `[1,2,3]`
        * 相当于 [[Python Functions - str|str]] 函数的反操作
    * 也可以很复杂如 `1 if 1>2 else 3`, 则返回**整数** 3
* 表达式的结果是一个**操作**的话则执行该操作
    * 如 `eval("__import__('os').startfile(r'D:\\Desktop\\python.exe')")`
    * 无需 `print()`, 而是跟 [[Python Functions - print|print]] 函数一样直接被执行
* 使用场景:
    * 表达式是以字符串形式出现的时候
    * 处理 `input()`　输入的表达式
        * 可直接利用 eval 函数对输入序列进行[[Python Sequence Unpacking|序列解包]]

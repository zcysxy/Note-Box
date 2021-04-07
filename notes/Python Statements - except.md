# Python Statements - except

[[Python Statements]] | [[Python Keywords]]

---

* 在 [[Python Exception Handling]] 中接于 [[Python Statements - try|try]] 语句后使用, 它指定了 [[Python Statements - try|try]] 语句指定的语句块出现**某个**异常后应该运行的语句块

## 基础用法

```py
try:
    try_block
except:
    handler
```

以上语句在 *try_block* 出现**任何**异常后, 都会执行 *handler*

## 指定异常

```py
try:
    try_block
except exception1:
    handler1
except exception2:
    handler2
except:
    handler_else
```

* 如上, *except* 语句还可以**指定**特定的异常出现后执行特定的语句块
    * 可以指定内置[[Python Exception Handling#异常种类|异常类型]]或者自定义异常类型
    * 若指定的是未定义的异常名, 则若要执行相应 *except* 语句的话会[[Python Exception Handling#异常处理中的异常|再报错]]
* 类似于 [[Python Statements - elif|elif]] 语句, 各 *except* 语句是**并列**的, 它们地位相同, 但有判断的**先后**, 即若异常判断为 *exception1*, 则直接执行 *handler1*, 跳过之后的 *except* 语句
* 如果不能预测所有可能出现的异常, 最好最后补充一个不指定异常的 *except* 语句, 则出现未被列出的异常时也可以处理
    * 否则出现未被列出异常时, 程序终止, 系统报错 (相当于无异常处理)
    * 对于**意外异常**, 还可以通过 [[Python Statements - raise|raise]] 语句重新**报错**

### 相同异常处理

要对多个异常做相同的处理, 除了可以用多个 *except* 语句外, 还可以直接写成如下形式:

```py
try:
    try_block
except (exception1, exception2,...,exceptionn):
    handler
```

即将所有要指定的异常写进一个元组, 它们出现时统一都执行 *handler* 语句块

### 异常别名

通过 [[Python Keywords - as|as]] 关键字为指定异常创建别名, 主要用于处理该异常时要调用异常相关信息的情况, 例如

```py
try:
    try_block
except BaseException as be:
    print(type(be))
    print(be.args)
    print(be)
```

[//begin]: # "Autogenerated link references for markdown compatibility"
[Python Statements]: Python Statements "Python Statements"
[Python Keywords]: Python Keywords "Python Keywords"
[Python Exception Handling]: Python Exception Handling "Python Exception Handling"
[//end]: # "Autogenerated link references"
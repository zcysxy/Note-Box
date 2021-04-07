# Python Statements - raise

[[Python Statements]] | [[Python Keywords]]

---

* *raise* 语句用于在指定情况发生时抛出指定异常
* 主要使用场景
    * 抛出自定义异常
    * [[Python Exception Handling|处理异常]]后再次显示异常 (抛出当前异常)

## 抛出当前异常

用于在 [[Python Statements - except|except]] 语句下, 单独成句

```py
try:
    f = open('demo.txt','r')
    f.write('trytry')
    f.close()
except:
    f.close()
    raise
```

## 抛出自定义异常

```py
raise specifiedException("Error text")
```

* 其中 *specifiedException* 可以为内置异常或者自定义异常
    * 一般可用 *Exception* 来指代一切异常
* `("Error text")` 可无, 用来显示提供给用户的异常信息
* 例子

    ```py
    x = "hello"
    if not type(x) is int:
    raise TypeError("Only integers are allowed")
    ```

    terminal 内显示: ![20201211222859](https://raw.githubusercontent.com/zcysxy/Figurebed/master/img/20201211222859.png)

[//begin]: # "Autogenerated link references for markdown compatibility"
[Python Statements]: Python Statements "Python Statements"
[Python Keywords]: Python Keywords "Python Keywords"
[//end]: # "Autogenerated link references"
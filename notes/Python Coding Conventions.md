# Python Coding Conventions

[[Python]]

## 缩进

* 类定义, 函数定义, 选择结构, 循环结构, 行尾的**冒号**表示缩进的开始 ^61671b
* Python 程序是依靠代码块的缩进来体现代码之间的**逻辑关系**的, 缩进结束就表示一个代码块结束了
* 同一个级别的代码块的缩进量必须相同
* 一般而言, 以 **4 个空格**为基本缩进单位

## 注释

* 一个好的, 可读性强的程序一般包含 **30%** 以上的注释 ^03294b
* 注释方式:
    * 以 `#` 开始, 表示本行 `#` 之后的内容为注释
    * 包含在一对三引号 `'''...'''` 或 `"""..."""` 之间且不属于任何语句的内容将被解释器认为是注释

## 空格与空行

* 需加空格
    * 运算符两侧
    * 函数参数之间
    * 逗号后面
* 需加空行
    * 不同功能的代码块之间
    * 不同的函数定义之间

## 推荐程序结构

```python
import  some module   #导入外部模块

def  myFun(var1, var2):   #自定义函数


def  main():    #主流程, 亦是自定义函数, 可以是其他函数名
                                #调用 myFun() 等

if  __name__ == "__main__":
    main()    #执行主流程
```

^24e9cb

## 其他

* 每个 import 只导入一个模块
* 如果一行语句太长, 可以在行尾加上 `\` 来换行分成多行, 但是更建议使用括号来包含多行内容
* 适当使用异常处理结构进行容错
* 软件应具有较强的**可测试性**
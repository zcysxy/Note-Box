# Python Basics

[[Python]]

---

## 预备知识

程序 program
: 让计算机执行某项具体任务而提供给它的详细**指令集和**

人机界面 User Interface
: ![20200922143742](https://raw.githubusercontent.com/zcysxy/Figurebed/master/img/20200922143742.png)

* 计算机结构
    * IPO

        ```mermaid
        graph LR
        input --> process --> output
        ```

    * <img align="top" src="https://raw.githubusercontent.com/zcysxy/Figurebed/master/img/20200922144718.png">

</br>

* 比特/bit(s) = **binary digit**
* 1 字节/byte = 8 bits
    * 1 KB = 2^10^ bytes
    * 1 MB = 2^20^ bytes
    * 1 GB = 2^30^ bytes
    * 1 TB = 2^40^ bytes
    * 1 PB = 2^50^ bytes

^271806

* 程序设计语言种类

    ![20200922161527](https://raw.githubusercontent.com/zcysxy/Figurebed/master/img/20200922161527.png)

    * 高级语言特点分类
        * 面向**过程**语言: 程序必须详细地描述解题的过程和细节. 如 C 语言
        * 面向**对象**语言: 把问题中的对象抽象成类, 利用**继承机制**及多态特性提高程序的开发效率, 改善程序的可靠性及可维护性. 如 Python ^df6ffb
        * 面向**问题**语言: 程序只需告诉计算机做什么, 不必告诉计算机如何做. 应用范围较窄. 如 SQL

## Python 特点

### 优点

* 软件质量 (*特色*)  
  在很大程度上, Python 更注重**可读性**, **一致性**和软件质量, Python 的设计致力于可读性, 带来了比其他语言更优秀的**可重用性**和**可维护性**, Python 秉承了一种独特的简洁和高可读性的语法, 以及一种高度一致的编程序模式
* 提高开发者效率 (*特色*)  
  相对于 C, C++, Java 等编辑/静态类型语言, Python 的开发效率升了 3-5 倍, 也就是说代码量是其他编程语言的 1/5-1/3, 而且无需编译, 链接步骤, 提高程序员效率
* 程序可移植性  
  绝大多数 Python 程序能不做任何修改即可在所有主流计算机平台上运行, 此外, Python 提供多种可选的独立程序, 如用户图形界面, 数据库接入, 基于 web 系统, 还提供了操作系统接口等
* 标准库  
  Python 内置了众多**预编译并可移植的功能模块**, 涵盖了从字符模式到网络编程等一系列应用级编程任务; 此外, Python 可通过自行开发的库和众多的第三方库简化编程, 第三方库包括网站开发, 数值计算, 串口编写, 游戏开发等各个应用场景
* 组件集成  
  Python 脚本通过灵活的集成机制轻松地与应用程序的其他部分进行通信, 这种集成使得 Python 成为产品定制和扩展的工具. 如今, Python 程序可以与 C, C++ 相互调用, 可以与 java 组件集成, 与 COM, .NET 矿建通信.
* 享受编程乐趣  
  Python 的易用性和强大的内置工具和第三方库使得编程成为一种乐趣而不是琐碎的重复劳动

### 缺点

目前 Python 的标准实现方式是将源代码编译成**字节码**形式, 之后再将字节码解释执行, 由于考虑到平台移植性, 所以字节码被设计为一种与平台无关的格式. 然而由于 Python 没有将代码编译成底层的二进制代码, 所以一些 Python 程序将比像 C 这样的完全编译的语言慢.

## 软件基础

* 软件窗口
    * 交互式窗口

        ![20200922162349](https://raw.githubusercontent.com/zcysxy/Figurebed/master/img/20200922162349.png)
    * 文件窗口

        ![20200922162316](https://raw.githubusercontent.com/zcysxy/Figurebed/master/img/20200922162316.png)

/! 交互式窗口 VS. 文件窗口

* 相互触发
* 文件运行于交互式窗口内
* 简单的、临时性代码使用交互式窗口
* 复杂的、重复使用的代码使用文件窗口
* 使用文件窗口为主

!/

* 查看当前软件版本
    * [[Python Modules - sys]]
    * 交互式窗口

        ```Python
        >>> import sys
        >>> sys.version
        ```

    * 文件窗口

        ```Python
        import sys
        print(sys.version)
        ```

## 数值运算

[[Python Operators - Arithmetic Operators]]

* 乘 `*`
* 除 `/`
* 幂 `**`
* 赋值 `=`

## <kbd>[[Python Functions - print|print]]</kbd> & <kbd>[[Python Functions - input|input]]</kbd>

* ![[Python Functions - print#一行]]
* ![[Python Functions - print#多行]]
* ![[Python Functions - input#输入]]

## 自定义函数

[[Python Statements - def]]

例如:

```py
def main():
    print('hello')

main()
```

## 推荐程序结构

![[Python Coding Conventions#^24e9cb]]

## ⭐ 对象与变量

### 对象

* Python 中的**数据**都是 **"对象"**.

| 对象类型(数据类型)                  | 示例                              |
|-----------------------------------|-----------------------------------|
| [[Python Types - Number\|数字]]     | 1234, 3.14, 3+4++j++(复数)        |
| [[Python Types - String\|字符串]]   | 'jwfw', "I'm Josh", '''hello'''   |
| 日期                                | 2012-08-25                        |
| [[Python Types - List\|列表]]       | [1,2,3]                           |
| [[Python Types - Dictionary\|字典]] | {1:'food', 2:'taste', 3:'import'} |
| [[Python Types - Tuple\|元组]]      | (2,-5,6)                          |
| 文件                                | f=open('data.dat','r')            |
| [[Python Types - Set\|集合]]        | set('abc'), {'a','b','c'}         |
| [[Python Types - bool\|布尔型]]     | True, False                       |
| [[Python Types - NoneType\|空类型]] | None                              |
| 编程单元类型                        | 函数, 模块, 类                    |

* 对象是**内存中的一块区域**
    ![20200922195401](https://raw.githubusercontent.com/zcysxy/Figurebed/master/img/20200922195401.png)

### 变量

* Python 中, 不需要事先声明变量名及其类型, 直接**赋值**即可创建各种类型的对象变量 ^5d90d7
* **赋值**操作是**创建或改变**一个变量对一个对象的**指向**

/@

```py
y = 'hello world'
```

创建了变量 %y% 并赋值为字符串 'hello world'

@/

#### 变量命名规则

* 变量名是由**字母, 数字, 下划线**构成的字符序列, 不能有空格以及标点符号, 可以任意长度
* 变量名必须**以字母或下划线开头** ^749b64
    * 下划线开头的变量有**特殊含义**
* 变量不能以 [[Python Keywords]] 为名字

!! 以下划线开头的变量有特殊含义

* 变量名对英文字母的**大小写敏感**
* **不能使用[[Python Keywords|关键字]]**作变量名, 关键字在 Python 中有特殊含义；
* 不建议使用系统内置的模块名, 类型名或函数名以及已导入的模块名及其成员名作变量名, 这将会改变其类型和含义

#### 变量类型判断

* 函数 [[Python Functions - type|type(x)]] 返回变量 %x% 的类型
* 函数 [[Python Functions - isinstance|isinstance(x, type)]] 返回变量 %x% 是否为 type 类型变量的判断

/@

```py
>>> x = 'hello'
>>> y = 10
>>> type(x)
<class 'str'>
>>> isinstance(x, int)
False
>>> isinstance(y, int)
True
```

@/

#### ⭐ 变量的内存模型

* 变量实际上保存的是对象的**引用**
* `id(x)` 返回变量指向的对象在**内存中的位置**
* 给变量 %y% 赋值变量 %x% (`y=x`), 是将 %y% 也指向 %x% 指向的对象
* 对于**不可变对象**, 每次变动赋值是将变量指向一个新的对象, 而原对象不变, 故 `id(x)` 变化
* 非序列如数字自然为不可变对象, 序列对象**字符串**和**元组**也为不可变对象

##### 缓存重用

* 数字和**字符**会被缓存重用, 即它们在内存中的位置不变, 故 **id 不变**
* ~~针对访问频率所作的优化, 整数只有 -5 到 256 的**对象**缓存重用, 浮点数无法缓存, 总是新建新对象~~ (存疑)

/@

```py
x = 3
y = 4
z = x
print(id(x), id(y), id(z))
y = 3
x = y+1
print(id(x), id(y))
y = y+1
print(id(y))
```

output:

```text
140728238252496 140728238252528 140728238252496
140728238252528 140728238252496
140728238252528
```

@/

##### 序列变量

对于序列变量如 %s% 的如下变动

```py
s = 'hello'
s = 'world'
s = 'hello'
```

不准确理解:  
![20200922215743](https://raw.githubusercontent.com/zcysxy/Figurebed/master/img/20200922215743.png)

正确理解:
![20200922215822](https://raw.githubusercontent.com/zcysxy/Figurebed/master/img/20200922215822.png)

即 %s% 先指向的对象为**一组变量** [0]-[4], 它们又分别指向了一个字母. 因为字符串为不可变序列, 所以**这组变量的 id** (即 `id(s)`)每次都会变化

* 对于可变对象(序列), 赋值运算可以改变其内元素(变量)的指向而不改变整个变量的 id
* **[[Python Types - List|列表]]**, **[[Python Types - Dictionary|字典]]**, **[[Python Types - Set|集合]]**为可变序列

/@

```py
x = [1,2,3]
print(id(x))
x[0] = 4
print(x, id(x))
```

output:

```text
2797390680456
[4, 2, 3] 2797390680456
```

内存变化模型:

<img height=250px src="https://raw.githubusercontent.com/zcysxy/Figurebed/master/img/39A425BF-4EA4-4D67-AF76-C9DB13156606.jpeg">

@/

!! Python 中列表元素计数从 **0** 开始 ^9f62b1

!! 不可变序列如字符串, 元组不可以通过下标改变其内元素

#### 删除变量

* [[Python Statements - del|del]] 作为函数 `del(x)` 或作为语句 `del x` 可以删除变量 %x%, 则之后不能再引用变量 %x%
* 还可以删除可变序列的指定元素, 如 `del(x[0])`. 则 %x% 的元素数少一位, 其他元素相对位置不变. 不可变序列的元素不可以单独删除
    * 用 `del(x[i])` 删除可变序列元素仍然**不改变**变量 id

### 表达式

* 在 Python 中，以下属于合法的[[Python Expressions|表达式]]
    * 单个任何类型的常量
    * 单个任何类型的变量
    * 函数调用（包括嵌套调用）
    * 使用**运算符**连接的常量、变量、函数调用

## `dir` 和 `help` 函数

* ![[Python Functions - dir#Basics]]
* ![[Python Functions - help#Basics]]

[//begin]: # "Autogenerated link references for markdown compatibility"
[Python]: Python "Python"
[tocheck]: @ToCheck "🔍 @To Check"
[//end]: # "Autogenerated link references"

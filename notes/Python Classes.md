# Python Classes

[[Python]]

---

Python is an [[Object Oriented Programming|object oriented]] programming language. Almost **everything** in Python is an object, with its properties and methods.

一个类 class 就像一个对象 object 的容器, 定义了生成对象的范式. 定义类时用**变量形式**表示的对象属性的成员称为数据成员 data member 或成员属性 data attribute; 用**函数形式**表示的对象行为的成员称为成员函数 member function 或成员方法 member method. 两者统称为类的成员.

## Instance

[[Object Oriented Programming|OOP]] 中于类相对的一个很重要的概念就是实例 instance. 前面已经说了一个类就像一个对象的容器, 那么实例就是**属于一个类的对象**. 更抽象的, 实例作为一个形容词, 指的是类针对实例的属性和操作等.

比如**实例属性**, 就是指实例化后才有的一个对象的属性; 相对的**类属性**, 就是将类本身看作一个对象, 无需实例化就它就具有的属性. 又比如**实例方法**, 指的是作用于实例对象的方法.

## Class Definition

Use [[Python Statements - Class|class]] to to create a function definition

## Class Calling

Python 中访问类有两种方法: [类访问 attribute references](#attribute-references) 和[实例化](#instantiation).

以下列出两种访问方法的一些区别:

* 访问类**实例方法**时要传递 `self` 参数, 通过实例化后的对象调用时不用显式传递该参数, 而通过类访问则需要将一个实例对象显式地传递给 `self` 参数

    ```python
    class Cla():
        def __init__(self, x=1):
            self.x = x
        def fun(self):
            print(self.x)

    cl = Cla(2)
    cl.fun() # 无需传递 self 参数
    Cla.fun(Cla()) # 这里 Cla() 是传递给 self 地实例对象
    ```

## Attribute References

类访问即将类看作一个对象, 直接访问其成员,

## Instantiation

实例化即将一个类赋给一个变量并初始化该变量, 这样就得到了一个属于该类地**实例/对象**.

```python
cla = myCla()
```

之后就可以通过 `cla.member` 来访问类中的数据成员和成员方法. 并且实例化后调用类成员时无需传递 `self` 参数.

~~ Python 中方法和函数的一个重要区别就是, 一个对象方法其实是首先把对象作为第一个参数传递给了方法. 所以实例化后的对象方法实际上 `self` 参数就是对象本身.

## Class Modification

Python 中可以**动态**地为**类**和**实例**增加和修改属性, 如下例

```python
class Cla:
    length = 5

cla1 = cla()
cla1.height = 1 # 增加实例的属性
cla1.length = 10 # 修改实例的属性
Cla.width = 20 # 增加类的属性
Cla.length = 10 # 修改类的属性
```

!! 注意辨析这里实例的属性/类的属性与 [[Python Statements - Class|Class]] 定义中的实例属性/类属性. 两者有联系也有区别, 比如可以修改实例的实例属性和类属性, 但只能修改类的类属性.

* 修改实例的属性并不会影响类的属性和其他实例的属性
* 修改类的属性会影响所有实例的属性, 包括之前已实例化的对象

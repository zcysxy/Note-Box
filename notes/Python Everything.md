# Python Everything

[[Python]]

> for 2020 Fall Semester Python course

---

## Most Basic Syntax

* if, def 等语句后须有冒号 `:`, 表示缩进的开始 ^[[[Python Coding Conventions#^61671b]]]
* 任何语句后都无需结束符 `;`
* 数值运算特殊符号: 幂 `**`, 模 `%`, 整除 `//` ^[[[Python Basics#数值运算]]]
    * ++整除是[[Rounding to Integer#Round down 向下取整|向下取整]]++
* Python 中, 不需要事先声明变量名及其类型, 直接**赋值**即可创建各种类型的对象变量^[[[Python Basics#^5d90d7]]]
* 变量名区分大小写, 只能以字母(包括中文等字符)和下划线开头^[[[Python Basics#^749b64]]]

## General Knowledge

* 1 字节 byte = 8 比特 bit ^[[[Python Basics#^271806]]]
* 运行 Python 的方式有两种 ^[[[Python Basics#软件基础]]]
    * 交互式窗口 Python Shell
        * 这是直接打开 Python.exe 执行的程序
        * 不能在这个窗口内运行 `.py` 的 Python 程序
    * 命令提示符窗口 Prompt
        * 可以是系统的 Command Prompt, Anaconda Prompt 等
        * 通过命令行 `python file.py` 来用 Python 编译执行 `file.py` 文件
    * 可以直接在 Prompt 中使用 Python 的 CLI
* Python 是一种面向**对象**的语言, 把问题中的对象抽象成**类**，利用**继承机制**及多态特性提高程序的开发效率,改善程序的可靠性及可维护性. 区别于面向**过程**的语言和面向**问题**的语言 ^[[[Python Basics#^df6ffb]]]
* Python 用的是 UTF-8 编码 ^[[[Python Types - String#^ad6047]]]

*[CLI]: Command Line Interface

## Basics

* 注释很重要, 包括函数注释 ^[[[Python Coding Conventions#^03294b]]]^[[[Python Statements - def#函数注释 Description]]]
* Python 中所有内置的计数器/索引都是从 ++**0**++ 开始, 并且一般的 *end* 参数都不包括在遍历范围内^[[[Python Basics#^9f62b1]]]
* 索引还可以接受**负整数**, 相当于 `x + len(sequence)`, 如 `-1` 就是列表中最后一个元素
* 可变对象: 列表, 字典, 集合. 它们在内存中有两层结构, 首先一个指针指向它们, 它们又包含了一组指针指向它们的元素, 可变指的是第二层面, 即内部指针的增加, 改变, 删除不影响第一层指针(id 不变)
* 通过语句 `if __name__ == "__main__":` 来执行程序中的主函数 (一般是 main)^[[[Python Coding Conventions#^24e9cb]]]
* 变量的内存模型^[ [[Python Basics#缓存重用]] ]
    * 变量保存的是**对象的引用**
    * `id(x)` 返回的是变量 %x% 引用对象在**内存中的位置**
        * 故变量 id 改变的原因是引用不同的对象, 而不是对象的 id 改变
        * 一次程序运行中, 对象的 id 一般不会改变
    * 缓存重用: 简单的数字和字符对象在内存中位置恒不变 (无论是在运行什么程序文件), 故 id 不变
    * 序列变量储存的是**对一组变量的引用**
        * 这一组变量即为序列变量的元素
        * 于是可变序列指的是元素变换其引用对象时, 这组变量的 id (序列变量的 id) 不变
        * 不可变序列即元素变换其引用对象时, 整组变量的 id 改变, 序列变量变换其引用对象

## [[Python Types]]

* 可变类型: 列表, 字典, 集合
* 序列类型: 列表, 字符串, 元组, range, (字典, 集合)
* 类型名称 (作为函数 [[Python Functions - isinstance|isinstance]] 第二个参数)

    | 名称     | 数据类型                 |
    |----------|------------------------|
    | int      | 整数(包括不同进制)        |
    | float    | 浮点数(包括科学计数法)     |
    | complex  | 复数                    |
    | list     | 列表                    |
    | tuple    | 元组                    |
    | str      | 字符串                  |
    | dict     | 字典                    |
    | set      | 集合                    |
    | range    | range                   |
    | bool     | bool 值 *True*, *False* |
    | NoneType | 空值 *None*             |

### [[Python Types - Number]]

#### 注意

* 整数除 0 外其余数字不能前面添加不必要的 0, 如 `008` 是非法记法
    * 因为 0 是特殊前缀, 用来指示进制

#### 整数的不同进制

* 整数的表示
    * 二进制表示 `0b[0-1]+` 或 `0B[0-1]+`
    * 八进制表示 `0o[0-7]+` 或 `0O[0-7]+`
    * 十六进制表示 `0x[0-9a-fA-F]+` 或 `0X[0-9a-fA-F]+`
* 不同进制的整数在内存中是一样的, 区别仅在于表示(显示)
* 不同进制表示的整数可以直接做运算
* [[Python Functions - print|print]] 函数输出的总是十进制
* 进制的转换
    * 函数 `bin(x)`
    * 函数 `oct(x)`
    * 函数 `hex(x)`
    * 以上函数返回整数(任何进制) %x% 转换为其二进制, 八进制, 十六进制的表示, 是**字符串**
* `int(str, i)` 返回 i 进制数字字符串 %str% 的**十进制**值, 是**整数**. i 默认为 10

#### 浮点数的表示

* 浮点数只有十进制
* 合法表示:
    * `x.y`
        * `0*x.y` 即浮点数前可以添加 `0`
    * `.y`
    * `x.`
    * `xey`, `xEy`
        * 科学计数法中 `x` 可以是任意浮点数, 而 `y` 必须为整数

#### 复数的运算

* 取实部 `.real`
* 取复部 `.imag`
* 取共轭 `.conjugate()`
* 复数乘法 `*`, 除法 `/`

### [[Python Sequence]]

#### 序列比较规则

* **字典序** + **包含序**
* 只有同类序列能够比较顺序, 且 [[Python Functions - range|range]] 和 [[Python Types - Dictionary|字典]] 无法比较顺序

#### [[Python Slice]]

* 作用相当于**浅拷贝**
* 索引值可以超出序列长度
* `sequence[::-1]` 相当于 `sequence[-1:-len(s)-1:-1]`, 而不是一般的 `sequence[0:len(sequence):-1]`

### [[Python Types - List]]

#### 注意

* 列表 "乘法" `*` 是浅拷贝
* 因为切片可以超出索引范围, 所以可以利用切片为列表原地增添元素
    * 如 `l[len(l):] = append_seq`, 相当于 `l.extend(append_seq)`
* 创建长度为 *n* 的 "空列表" 时, 不能用 `[] * n`, 这样创建的仍是 `[]`, 可先用其他元素 "占位"

#### [[List Comprehension]]

* 表达式可为复杂表达式, 可调用函数
    * 复杂表达式如**条件运算**: `v**2 if v%2 == 0 else v+1`
* 可以有多个 *for* 循环, 它们自动按先后顺序(如[[Python Statements - for|for]] 语句中一样)形成嵌套
* 列表推导式创建的是**新列表**, 虽然生成元素时需要用到其他可迭代对象, 但与其(**第一层**)互不影响

#### 列表方法

|         方法          | 说明                                            |
|:---------------------:|-----------------------------------------------|
|    list.append(x)     | 将元素 x 添加至列表尾部                         |
|    list.extend(L)     | 将序列 %L% 中所有元素添加至列表尾部             |
| list.insert(index, x) | 在列表指定位置 index 处添加元素 x               |
|    list.remove(x)     | 在列表中删除**首次出现**的指定元素              |
|    list.pop(index)    | 删除并返回列表对象指定位置 index 处的元素       |
|     list.clear()      | 删除列表中所有元素，但保留列表对象               |
|     list.index(x)     | 返回值为x的**首个元素**的下标, 不存在则出错     |
|     list.count(x)     | 返回指定元素 x 在列表中的出现次数, 不存在返回 0 |
|    list.reverse()     | 对列表元素进行**原地**(即不产生新列表)倒序      |
|      list.sort()      | 对列表元素进行原地排序                          |
|      list.copy()      | 返回列表对象的浅拷贝                            |

* 一般先用 `list.count` 判断某元素是否存在, 再执行 `list.remove`, `list.index` 等操作
* 以上除了 `list.copy()` 方法外均为**原地操作**, 区别于函数 [[Python Functions - sorted|sorted]] 和 [[Python Functions - reversed|reversed]] 产生的是新对象
* `list.sort()` 参数及用法同函数 [[Python Functions - sorted|sorted]]
* 以上除了 `list.insert()` 之外涉及索引的方法若索引超出范围都会报错, 区别于 [[Python Slice]]
    * `list.insert(len(list),x)` 可将 *x* 添在列表 *list* 最后一位
* `list.pop()` 默认删除并返回**最后**一个元素

### [[Python Types - Tuple]]

#### 注意

* 无括号的序列一般默认为元组
* 创建只含单个元素时, 元素后要补充逗号 `,`, 因为不补充逗号, 圆括号被识别为运算优先级规定
* 用 `()` 和 [[List Comprehension]] 的格式创建的是可迭代对象 [[Python Types - Generator]], 而非直接是元组
    * [[Python Types - Generator]] 中的元素只能访问一次

### [[Python Types - Dictionary]]

#### 注意

* 虽说字典的元素是**键值对**, 但更根本的就是**键**
    * 序列排序时是对**键**排序
    * 序列成员测试是对**键**测试
    * 序列解包得到的是**键**
    * `for x in Dict` 等价于 `for x in Dict.keys()`
* 字典中元素以 `,` 分隔
    * Python 中不会用到符号 `;`
* 字典的键需是**不可变对象**, 特别地, 使用 [[Python Functions - dict|dict]] 函数创建字典时键只能是符合**变量命名规则**的字符, 然后自动转换为**字符串**
* 字典中键不允许重复, 否则新值覆盖旧值
* 访问字典元素时可以键作为"下标": `dict[key]` 返回 *key* 对应的值
    * 访问不存在的键报错
* `{}` 创建的是空字典, 而非空集合

#### 字典方法

|        方法         | 说明                                               |
|:-------------------:|--------------------------------------------------|
|    dict.get(key)    | 返回键 *key* 对应的值, *key* 不存在时返回指定值    |
|     dict.keys()     | 返回包含键列表的可迭代对象                         |
|    dict.values()    | 返回包含值列表的可迭代对象                         |
|    dict.items()     | 返回包含键值对元组列表的可迭代对象                 |
| dict.update(dict_2) | 将 %dict_2% 的键值对添加(若重复则覆盖)到 %dict% 中 |
|    dict.pop(key)    | 删除并返回键 *key* 对应的值                      |
|   dict.popitem()    | 删除并返回字典中的某个元素                         |
|    dict.clear()     | 删除字典所有元素                                   |

* `dict.get(key, [noneValue])`
    * 返回 *key* 对应的值, *key* 存在时等价于 `dict[key]`
    * 若无 *key* 键, 则返回 *noneValue*, 不报错
        * *noneValue* 为可选参数, 默认为**空值** *None*
    * *noneValue* 常设为一个空序列(空列表, 空元组, 空字符串等), 配合 `dict['key'] = dict.get('key',<>)` 来为不存在的键设置初始值, 同时也不影响存在的键值对

#### [[Python Functions - dict]]

* 用于创建字典, 3 种语法:
    * `dict(<(key1,value1),...,(keyn,valuen)>)`
        * `<>` 可为任意括号, 不能无, 区别于 [[Python Slice]]
    * `dict(key1=value1,...,keyn=valuen)`
        * *keyi* 需符合变量命名规则, 且会被自动转换为**字符串**
    * `dict.fromkeys(seq)`
        * 返回以可迭代对象 *seq* 中元素为**键**, 对应值为 *None* 的字典
            * 所以 *seq* 中元素需为不可变对象
        * *seq* 也可以是**字典**, 则返回键同字典 *seq*, 而值为空的**新字典**
            * 即之后若字典 *seq* 键改变也不会影响函数创建的新字典

### [[Python Types - Set]]

#### 注意

* 集合等价于没有值的[[Python Types - Dictionary|字典]], 即其中元素限制跟字典键一样, 只能为不可变对象, 且不能重复
    * 所以创建集合的函数 [[Python Functions - set|set]] 还有去除可迭代对象**重复元素**的作用

#### 集合方法

|              方法                | 说明                                   |
|:-------------------------------:|--------------------------------------|
|           set.add(x)            | 将 *x* 作为元素添加到集合 %set%          |
|            set.pop()            | 返回并删除集合 %set% 中某个元素          |
|          set.remove(x)          | 直接删除集合 %set% 中元素 *x*, 若无则报错 |
|          set.discard(x)         | 直接删除集合 %set% 中元素 *x*, 若无不报错 |
|           set.clear()           | 删除集合 %set% 中所有元素               |
|           set.copy()            | 返回集合 %set% 的拷贝                  |
|      set.issuperset(set_2)      | 判断集合 %set% 是否为集合 %set_2% 的超集 |
|       set.issubset(set_2)       | 判断集合 %set% 是否为集合 %set_2% 的子集 |
|      set.isdisjoint(set_2)      | 判断集合 %set% 与集合 %set_2% 的交集是否为空 |
|        set.union(set_2)         | 返回 %set% 和 %set_2% 的并集           |
|     set.intersection(set_2)     | 返回 %set% 和 %set_2% 的交集           |
|      set.difference(set_2)      | 返回 %set% 减去 %set_2% 的差集         |
| set.symmetric_difference(set_2) | 返回 %set% 和 %set_2% 的对称差集        |
| set.update(set_2)               | 将 %set% 原地更新为和 %set_2% 的并      |
| set.intersection_update(set_2)  | 将 %set% 原地更新为和 %set_2% 的交      |
| set.difference_update(set_2) 等 | 同上                                  |

* 集合的 `.pop()` 方法不接受参数传递
* 集合运算
    * `A.union(B)` = `A | B`
    * `A.intersection(B)` = `A & B`
    * `A.difference(B)` = `A - B`
    * `A.symmetric_difference(B)` = `A ^ B`
* 以上运算都生成**新集合**, 区别于所有**原地**更新的 *update* 方法
* 集合比较(包含关系)
    * `A.issuperset(B)` = `A >= B`
    * `A.issubset(B)` = `A <= B`

### [[Python Types - String]]

#### 注意

* 字符串的三引号由**最后**一个字符决定
    * 若最后一个字符非引号, 则三单引号和三双引号都行
    * 若最后一个字符为单引号, 则需用三双引号
    * 若最后一个字符为双引号, 则需用三单引号
* 也可以使用转移符号 `\` 使引号变为普通打印符号

#### 主要字符串方法

| 字符串方法              | 说明                                     |
|-----------------------|-------------------------------------------|
| `.startswith(string)` | 判断字符串是否已字符串 *string* 开始        |
| `.endswith(string)`   | 判断字符串是否已字符串 *string* 结束        |
| `string.join(iterable)` | 用字符串 *string* 作为中间间隔将可迭代对象 *iterable* 串联起来, 返回一个字符串 |
| `.strip(string)` | 删除原字符串**两端**出现的指定字符串 *string* 中的**元素**(默认为空白字符), 直到无法继续删除为止, 并**返回**删完后的新字符串 |
| `.rstrip(string)` | ... **右端** ... |
| `.lstrip(string)` | ... **左端** ... |
| `str1.find(str2,[start],[end])` | 返回字符串 *str2* 在原字符串指定范围 *str[start:end]* (默认从头, 到尾) 中**首次**出现的(第一个字符的)位置, 如果不存在则返回 ++-1++ |
| `str1.rfind(str2,[start],[end])` | ... **最后**出现 ... |
| `str1.index(str2,[start],[end])` | 同 `.find()`, 除了不存在则++报错++ |
| `str1.rindex(str2,[start],[end])` | 同 `.rfind()`, 除了不存在则++报错++ |
| `.count(string)` | 返回字符串 *string* 在原字符串中出现的次数 |
| `.replace(str1,str2)` | 将原字符串中的 *str1* 全部替换为 *str2*, 并返回新字符串 |
| `.translate(table)` | 按照映射表 *table* 转换原字符串并返回新字符串 |
| `.split(string, num)` | 以指定字符串 *string* 为分隔符(默认为空白符), 将字符串**从左端开始**分割成多个(至多 *num* + 1)字符串, 并返回分割结果**列表**(不含分隔符) |
| `.rsplit(string)` | ... **从右端开始** ... |
| `.partition(string)` | 以指定字符串 *string* 为分隔符将原字符串分割并返回为含 3 部分的**元组**: (**第一次出现**的分隔符前的字符串, 分隔符字符串 *string* , 第一次出现的分隔符后的字符串) |
| `.rpartition(string)` | ... **最后出现** ... |
| `.format(value)` | 将 *value* 赋值到字符串的对应占位符 |

* `translate(table)` 方法中的 *table* 由函数 `str.maketrans('str1', 'to_str2')` 生成

#### 字符串格式化

| 格式符    | 格式化方法     | 数据类型     |
|----------|--------------|------------|
| %d       | {:d}         | (十进制)整数 |
| %f 或 %F | {:f} 或 {:F} | 浮点数       |
| %c       | {:c}         | 字符        |
| %s       | {:s}         | 字符串       |

* 若要在字符串中表示 `%` 本身, 可用 `%%` (`\%`无效)
* `%c` **可以**用 ASCII/Unicode 表中的数字表示其字符, 也可以直接填入单个字符的字符串

| 辅助符号 | 格式化方法 | 说明                                        |
|---------|----------|--------------------------------------------|
| -       | {:<}     | 用做左对齐                                   |
| +       | {:+}     |在正数前面显示加号                             |
| 0       | {:0}     |显示的数字**前面**填充 0 而不是默认的空格         |
| m.n     | {:m.n}   | m 是显示的最小总宽度，n 是小数点后的位数(不足补 0) |

* `%d` 采用**向 0 取整**
* `%m.nf` 采用**四舍五入**
* `m.n` 还适用于 `%c` 和 `%s`

#### [[Python Modules - re]]

1. re 模块中的函数
    * 正则表达式为 *patStr*
    * `re.findall(patStr, longStr, flags)`
    * `re.split(patStr, longStr, flags)`
    * `re.match(patStr, longStr, flags)`
2. re 模块中对象的方法
    * 先构造正则表达式对象: `regex = re.compile(patStr, flags)`
    * `regex.findall(longStr)`
    * `regex.split(longStr)`
    * `regex.match(longStr)`

* 规范, 方便原因, 使用 raw string 构造模式字符串(正则表达式)
    * 查找 `a = r'abc\d'` 中的 `\` 字义符号, 以下两个方法等价
        * `re.findall('\\\\',a)`
        * `re.findall(r'\\',a)`

## [[Python Expressions]]

### 常见表达式

* `value_1 if condition else value_2`
    * 这是一个**表达式**, 因为它有返回值: 返回 *value1* 若条件 *condition* 满足; 否则返回 *value_2*
    * 所以没有 [[Python Statements - if|if]] 语句的种种限制, 该表达式可以出现在任何表达式可以出现的地方
* [[Python Conditional Expressions]]
* [[List Comprehension]]
* [[Python Lambda Function]]

### [[Python Operators]]

| 类别  | 运算符 | 备注 |
|------|-------|-----|
|[[Python Operators - Arithmetic Operators\|算术运算符]]| +, -, \*, /, //, %, **| `+` 还有连接**序列**的作用</br> `*` 还有重复**序列**的作用 </br> `-` 还是集合的差运算 |
|[[Python Operators - Comparison operators\|关系运算符]]| >, <, \==, <=, >=, !=       | 可以连用 |
|[[Python Operators - Membership Operators\|成员运算符]]| in, not in | `a not in b` 相当于 `not a in b` |
|[[Python Operators - Identity Operators\|身份运算符]]  | is, is not                  | `a is not b` 相当于 `not a is b`, 但 `a not is b` 非法 |
|[[Python Operators - Logical Operators\|逻辑运算符]]   | and, or, not                | `and` 和 `or` 惰性求值</br> 可以连用</br> 优先级: `not` > `and` > `or` |
|[[Python Operators - Bitwise Operators\|位运算符]]     | ~, &, \|,  ^,  <<, >>       |
|[[Python Operators - Assignment Operators\|赋值运算符]]| =, +=, -=, \*=, /=, //=, %= |

#### 逻辑运算符作为算数运算符

* `and` 运算 -- **找零值(空值)**
    * 两个分量有一个为零值(或空值), 则结果为这个分量的值, 即**零值(或空值)**
    * 两个分量都为零值(或空值)时, 则结果取**前一个**分量的值
    * 两个分量都为非零值(或非空值)时, 则结果取**后一个**分量的值
* `or` 运算 -- **找非零值(非空值)**
    * 两个分量有一个为零值(或空值), 则结果为另一个分量的值, 即**非零值(或非空值)**
    * 两个分量都为零值(或空值)时, 则结果取**后一个**分量的值
    * 两个分量都为非零值(或非空值)时, 则结果取**前一个**分量的值
* 以上规则总结为**惰性求值**
* 两种运算都不要求两边对象类型相同

#### 常见运算符优先级

运算有默认优先级, 可用括号`()`手动决定优先级

| 优先级 |           运算符             | 名称                        |
|:------:|:---------------------------:|-----------------------------|
|  最高  |         (), [], {}          | 括号                        |
|   v    | x[index], x[index,index], x(argument,...), x.attribute | subscription, [[Python Slice\|slice]], call, attribute reference |
|   v    |             **              | 指数运算                    |
|   v    |            +, -             | 一元正, 负运算              |
|   v    |        \*, /, //, %         | 乘, 除, 整除, 余数运算      |
|   v    |           +, -              | 二元加, 减运算              |
|   v    |              &              | bitwise AND                |
|   v    |          \^&#8203;          | bitwise XOR                |
|   v    |             \|              | bitwise OR                 |
|   v    |        <, <=, >, >=         | 大小比较运算                |
|   v    |           \==, !=           | 相等, 不等比较运算          |
|   v    |         is, is not          | 身份测试运算                |
|   v    |         in, not in          | 成员测试运算                |
|   v    |             not             | 逻辑否运算                  |
|   v    |             and             | 逻辑且运算                  |
|   v    |             or              | 逻辑或运算                  |
|   v    |          if - else          | 条件表达式                  |
|   v    |           lambda            | Lambda 表达式               |
|  最低  | =, +=, -=, \*=, /=, //=, %= | 赋值运算                    |

## [[Python Functions]]

### 函数调用

* 传递参数时可用 `(*sequence)` 对序列参数[[Python Sequence Unpacking|序列解包]]

### [[Python Statements - def]]

#### 参数

* 参数类型
    1. 普通参数 `(arg)`
    2. 默认参数 `(arg=default)`
        * 若与普通参数混用, 则默认值参数右边不能再有普通参数, 否则报错 (*SyntaxError*)
    3. 可变长度参数
        1. 元组参数 `(*p)`
        2. 字典参数 `(**p)`
            * 传递参数方法同 [[Python Functions - dict|dict]] 函数
            * 同时要避免键与关键参数的键同名
        * 与其他参数类型混用是要放在最右边
* 参数陷阱:
    1. 实参向形参的传递实为赋值, 故若实参为可变对象, 且函数执行过程中++形参发生原地改变, 则对应实参也会改变++
        * 但仅限原地改变, 若对形参重新赋值, 则赋值后的操作不再对实参有影响
    2. 默认值参数陷阱: 默认参数默认值为可变类型时, 该默认值参数只初始化一次

### [[Python Lambda Function]]

* Lambda 函数即作为**匿名对象**的函数, 其可以作为序列的元素等
* 可以作为 `.sort()` 方法和 [[Python Functions - sorted|sorted]] 函数的 *key* 参数的值
    * 则要求 lambda 函数的返回值可排序

### 重要内置函数

#### [[Python Functions - print]]

* print 函数**默认连接符**是空格 `' '`, 可用参数 `sep =` 来修改^[[[Python Functions - print#^40525a]]]
* 输出重定向参数: `file=`

#### [[Python Functions - min, max]]

* 传递多个参数 `a1,...,an` 时, 相当于填入元组 `(a1,...,an)`
* 传递的参数中的元素要可用[[Python Operators - Comparison operators]]排序
    * 如字典序, 包含序
* 不可填入**空对象**

#### [[Python Functions - sorted]]

* 参数: *reverse* 和 *key*
    * 常用的传递给 *key* 的函数有 [[Python Modules - operator|operator]] 模块中的 *itemgetter* 和 [[Python Lambda Function]]

#### [[Python Functions - enumerate]]

* 语法: `enumerate(sequence,[startIndex])`
    * *startIndex* 为枚举对应的序号初值, 默认为 0
* 返回**枚举对象**, 可迭代, 元素为 `(index, item)` 元组

#### [[Python Functions - zip]]

* 将多个序列对应位置元素组合为元组, 并返回包含这些元组的可迭代 zip 对象
* 常与 [[Python Sequence Unpacking]] 合用
    * 如二位列表转置: `list(zip(*Matrix))`

## [[Python File Handling]]

* 记得关闭文件!
* [[Python Functions - open|open]] 函数打开的文件是一个**可迭代对象**
* 读取内容
    1. 方法 `.read([n])`, 读取文件前 *n* 个字符(默认为整个文件), 返回**一个**字符串
    2. 方法 `.readline()`, 读取文件第一行前 *n* 个字符(默认为整行), 返回**一个**字符串
    3. 方法 `.readlines()`, 读取文件前 *n* 个字符涉及的行(默认为整个文件), 返回一个**列表**, 元素为文件的**每行**构成的字符串
    * `.readline()` 会++记录读取过的行数++, 因此可以循环读取下一行, 适用于大文件
    * `.readline()` 和 `.readlines()` 的 "每行" 都会包含**行末的换行符**
* 写入内容
    1. 方法 `.write(string)`, 写入**一个字符串** *string*
    2. 方法 `.writelines(strList)` 写入一个**列表**中 *strList* 的字符串元素
    * `.writelines(strList)` 相当于 `.write(''.join(strList))`, 并不直接分行, 需要手动在每个元素后添加换行符实现分行写入
* [[Python Statements - with|with]] statement:

    ```python
    with open('text.txt', 'r') as f_read:
        for eachline in f_read:
            with open('text_new.txt', 'a') as f_append:
                f_append.write(eachline.swapcase())
    ```

## [[Python Exception Handling]]

### 基本异常

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

### 异常处理语法

```python
try:
    try_body
except excerption_1 as e1:
    handler_1
    print(e1.args)
except (excerption_2,...,excerption_n):
    handler_other
except:
    handler_final
    raise
finally: # 绝对优先性
    final_block
    raise Exception('final_block executed')
else:
    else_block
```

## [[Python Scope]]

* [[Python Statements - nonlocal]] 一般只能上溯一层, 若上一层没有才会继续上溯. 且不能替代 [[Python Statements - global]]
* Python 没有 **block scope**, 即循环等语句块中的变量不是局部变量, 要注意区分

## [[Python Coding Conventions]]

```python
'''这是一个示例代码片段
用于说明 Python 的代码规范'''

import sys # 代码开头导入模块
from random import randint as ri # 一行只导入一个模块

a = [1, 2, 3] # 逗号, 井号后面一般要接**空格**
b = a + a # 运算符前后一般要有空格, 尤其是加号和减号
c = {
    'a': 1,
    'b': 2,
    'c': 3
} # 内容作为一行过长时, 推荐使用括号内换行增强可读性

# 不同功能的代码块之间要有空行, 如设置参数的代码和函数定义代码之间
def f(c, a=a, b=b):
    '''function to print a and b''' # 函数定义最好有注释说明
    try: # 合理使用异常处理结构进行容错
        print(a, b, c)
    except:
        pass

# 函数定义前后要有空行, 包括嵌套式定义
def g(n):
    '''print a square'''

    def h(n):
        print('*' * n)

    for i in range(n):
        h(n)

# 定义主函数
def main():
    f(1,1)
    g(10)

# 利用以下语句运行程序, 更方便调试和区分文件作为程序或模块 
if __name__ == "__main__":
    main()
```

## ❗ Attention

* 取整方式 [[Rounding to Integer]]:
    * 向下取整: 整商 `//`, 函数 `math.floor()`
    * 向 0 取整: [[Python Functions - int|int]], 字符串格式符 `%d`
    * 向上取整: 函数 `math.ceil()`
    * 远离 0 四舍五入: 函数 `round()`, `int(x+0.5)`

[//begin]: # "Autogenerated link references for markdown compatibility"
[Python]: Python "Python"
[Python Conditional Expressions]: Python Conditional Expressions "Python Conditional Expressions"
[Python Coding Conventions]: Python Coding Conventions "Python Coding Conventions"
[//end]: # "Autogenerated link references"
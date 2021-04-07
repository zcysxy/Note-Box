---
alias: 字符串
---

# Python Types - String

[[Python Types]] | [[Python Sequence]]

related: [[Character Encoding]]

---

* 用单引号, 双引号或三引号括起来的**符号系列**称为字符串
    * 符号系列采用 **UTF-8** 编码 ^ad6047
* 字符串属于**不可变序列**
    * 故字符串支持 [[Python Sequence]] 的通用方法, 如切片, 索引等
* **空串**表示为 `''` 或 `""`

## 引号

* 单引号, 双引号, 三单引号, 三双引号可以互相嵌套，用来表示复杂字符串
    * 单引号, 双引号, 三单引号, 三双引号一般情况下一样
    * 若输出内容包含单(双)引号, 则应用双(单)引号包裹内容
    * 若内容既含单引号, 又含双引号, 则应用三引号包裹内容
        * 若字符串最后一个元素不是引号, 则三单引号和三双引号都行
        * 若字符串最后一个元素是单引号, 则应用三双引号
        * 若字符串最后一个元素是双引号, 则应用三单引号
* 三引号'''或"""包裹内容保留换行，支持排版较为复杂的多行字符串；三引号还可以在程序中表示较长的注释
    * 见 [[Python Functions - print]]

/@

```py
print('she said "OMG"')
print(
  """she said
  'OMG'"""
)
```

@/

## 相关函数

* [[Python Functions - isinstance|isinstance]]
* [[Python Functions - str|str]]
* [[Python Functions - chr & ord|chr & ord]]
* [[Python Functions - eval|eval]]

## 字符串方法

!! 因为字符串为**不可变对象**, 故方法有返回操作的都是返回新列表(对象)

| 分类      | 字符串方法              | 说明                                     |
|----------|-----------------------|-------------------------------------------|
| 改变格式  | `.lower()`            | 返回小写格式字符串                          |
| ^        | `.upper()`            | 返回大写格式字符串                          |
| ^        | `.capitalize()`       | 返回首字母大写格式字符串                    |
| ^        | `.title()`            | 返回每个单词首字母大写格式(titlecase)字符串  |
| ^        | `.swapcase()`         | 返回大小写互换格式字符串                    |
| 判断      | `.startswith(string)` | 判断字符串是否已字符串 *string* 开始        |
| ^        | `.endswith(string)`   | 判断字符串是否已字符串 *string* 结束        |
| ^        | `.isalnum()`          | 判断字符串是否为数字和字母组成              |
| ^        | `.isalpha()`          | 判断字符串是否为字母组成                    |
| ^        | `.isdigit()`          | 判断字符串是否为数字组成                    |
| ^        | `.isspace()`          | 判断字符串是否为空白字符组成                |
| ^        | `.isupper()`          | 判断字符串是否为大写字母组成                |
| ^        | `.islower()`          | 判断字符串是否为小写字母组成                |
|串联       | `string.join(iterable)` | 用字符串 *string* 作为中间间隔将可迭代对象 *iterable* 串联起来, 返回一个字符串 |
|改变排列   | `.center(length,[string])` | 返回指定长度 *length* 的新字符串, 原字符串**居中**, 并使用指定字符串 *string* (默认为空格) 填充超出长度 |
|^         | `.ljust(length,[string])` | 返回指定长度 *length* 的新字符串, 原字符串**左对齐**, 并使用指定字符串 *string* (默认为空格) 填充超出长度 |
|^         | `.rjust(length,[string])` | 返回指定长度 *length* 的新字符串, 原字符串**右对齐**, 并使用指定字符串 *string* (默认为空格) 填充超出长度 |
|删减       | `.strip(string)` | 删除原字符串**两端**出现的指定字符串 *string* 中的元素, 直到无法继续删除为止, 并**返回**删完后的新字符串 |
|^         | `.rstrip(string)` | 删除原字符串**右端**出现的指定字符串 *string* 中的元素, 直到无法继续删除为止, 并**返回**删完后的新字符串 |
|^         | `.lstrip(string)` | 删除原字符串**左端**出现的指定字符串 *string* 中的元素, 直到无法继续删除为止, 并**返回**删完后的新字符串 |
|查找       | `str1.find(str2,[start],[end])` | 返回字符串 *str2* 在原字符串指定范围 *str[start:end]* 中首次出现的位置, 如果不存在则返回 ++-1++ |
|^         | `str1.rfind(str2,[start],[end])` | 返回字符串 *str2* 在原字符串指定范围 *str[start:end]* 中最后出现的位置, 如果不存在则返回 ++-1++ |
|^         | `str1.index(str2,[start],[end])` | 同 `.find()`, 除了不存在则++报错++ |
|^         | `str1.rindex(str2,[start],[end])` | 同 `.rfind()`, 除了不存在则++报错++ |
|^         | `.count(string)` | 返回字符串 *string* 在原字符串中出现的次数 |
|替换       | `.replace(str1,str2)` | 将原字符串中的 *str1* 全部替换为 *str2*, 并返回新字符串 |
|^         | `.translate(table)` | 按照映射表 *table* 转换原字符串并返回新字符串 |
|分割       | `.split(string)` | 以指定字符串 *string* 为分隔符, 将字符串**从左端开始**分割成多个字符串, 并返回分割结果**列表** |
|^         | `.rsplit(string)` | 以指定字符串 *string* 为分隔符, 将字符串**从右端开始**分割成多个字符串, 并返回分割结果**列表** |
|^         | `.partition(string)` | 以指定字符串 *string* 为分隔符将原字符串分割并返回为含 3 部分的**元组**: (**第一次出现**的分隔符前的字符串, 分隔符字符串 *string* , 第一次出现的分隔符后的字符串) |
|^         | `.rpartition(string)` | 以指定字符串 *string* 为分隔符将原字符串分割并返回为含 3 部分的**元组**: (**最后出现**的分隔符前的字符串, 分隔符字符串 *string* , 最后出现的分隔符后的字符串) |
|格式化     | `.format(value)` | 将 *value* 赋值到字符串的对应占位符 |

### 判断方法 `.is..()`

* 空白字符包括 `\t`, `\n` 等非打印字符
* 空字符串 `''` 在 `.is...()` 下返回均为 *False*
* 对于浮点数, 如 `'1.3'.isdigit()` 返回 *False*

### 串联方法 `.join()`

* `.join(iterable)` 中的可迭代对象 *iterable* 的元素需为**字符串**
* 处于效率考虑, 推荐使用 `.join()` 方法串联字符串, 而不是 `+` 运算符

### 改变排列方法 `.center()`, `.ljust()`, `.rjust()`

* 若原字符串长度大于等于指定长度, 则直接返回与原字符串相同的新字符串

### 删减方法 `.strip()`, `.rstrip()`, `.lstrip()`

* 无参数时默认删去**空白字符**

```py
>>> "aaabcede".strip("ae")
"bced"
>>> "aaabcede".lstrip("ae")
"bcede"
>>> "aaabcede".rstrip("de")
"aaabc"
```

### 查找方法之 `.find()`, `.rfind()`

* 无 *[start]* 和 *[end]* 参数则默认搜索整个字符串
* 无 *[end]*　参数则默认搜索至字符串尾端
* 返回的值为子字符串　*str2* 第一次(最后一次)出现时**第一个字符**所在位置

++ 字符串更高级的查找方法为利用 [[Python Modules - re|re 模块]]进行正则表达式查找

### 替换方法之 `.translate(table)`

* *table* 需由函数 `str.maketrans('str1','str2')` 生成, 供 `.translate()` 使用
    * 返回字符串 *str1* 一一映射到 *str2* 的映射表
    * 必须以 `str` 开头
    * *str1* 和 *str2* 的长度必须一致
* `.translate(table)` 中的 *table* 即由方法 `str.maketrans(str1,str2)` 生成的**映射表**
    * 此方法将原字符串中的 *str1* 中的元素全部替换为**对应的** *str2* 中的元素, 并返回替换后的新字符串
* ~~`.translate(table,str3)` 在**替换前**先删除原字符串中的 *str3* 中的元素~~ ++已过时++

### 分割方法之 `.split()`, `.rsplit()`

* 分割产生的字符串不再包括分隔字符
* 与 [`.join()` 方法](#串联方法-join)作用相反
* `.split()` 和 `.rsplit()` 有细微差别, 如:

    ```py
    >>> string = "1ababab2"
    >>> print(g.split("abab"))
    ['1','ab2']
    >>> print(g.rsplit("abab"))
    ['1ab','2']
    ```

* 若无法分割, 如原字符串中不含分隔符, 则直接返回只含原字符串一个元素的列表
* 若不指定分隔符, 则原字符串中的任何**空白符号** (如空格, 换行符\n, 制表符\t) 都将被默认为分隔符
    * 且连续的空白符号被视为**一个**分隔符
    * `.split(None)`, `.rsplit(None)` 即 "手动" 不指定分隔符
* `.split(string, num)`, `.rsplit(string, num)` 中的整数 *num* 指定**最大分割次数**, 则返回列表长度不超过 *num+1*
    * 指定最大分割次数后 `.split()` 和 `.rsplit()` 区别更明显

### 分割方法之 `.partition()`, `.rpartition()`

* 如果指定的分隔符不在原字符串中, 则返回的元组为: `(原字符串, '', '')` 或 `('','',源字符串)`

### 格式化方法 `.format()`

* 作用相当于用 `%` 构造的[string pattern](#string-pattern-字符串格式化)
* 语法: `pattern.format(value1,value2,...)`
    * 其中 *pattern* 中起作用的是**占位符 placeholder**, 格式有三种:
        * `{}`, 无内容, 则 *value1*, *value2*,... 按 `{}` 出现顺序填入占位符
            * 此时要求占位符个数小于等于值的个数
        * `{n}`, n 可看作元组 `(value1,value2,...)` 的索引, 因此对应值填入对应占位符
            * 此时对占位符的个数无限制, 因为可以出现多个 *n* 相同的占位符
            * 同时还可以用 `{n[index]}` 来指定填入第 *n* 个 *valuen* 的下标为 *index* 的元素
        * `{name}`, 这要求值是类似[[Python Types - Dictionary|字典]]中的 "键值对", 即 `(name1=value1,name2=value2,...)`, 则对应的 "值" 填入 *pattern* 中相应的 "键"
            * 同上, 此时可以有多个 *name* 相同的占位符, 故对占位符个数无限制
        * ++三种占位符命名方式不能混用++
* Formatting Types

    | formatting type | description                                           |
    |:--------------:|-------------------------------------------------------|
    | `:<`            | Left aligns the result (within the available space)   |
    | `:>`            | Right aligns the result (within the available space)  |
    | `:^`            | Center aligns the result (within the available space) |
    | `:=`            | Places the sign to the left most position             |
    | `:+`            | Use a plus sign or a minus sign to indicate if the result is positive or negative |
    | `:-`            | Use a minus sign for negative values only |
    | <code>: </code> |  Use a space to insert an extra space before positive numbers (and a minus sign before negative numbers) |
    | `:,`            | Use a comma as a thousand separator                   |
    | `:_`            | Use a underscore as a thousand separator              |
    | `:%`            | Percentage format                                     |
    | `:c`            | Converts the value into the corresponding unicode character |
    | `:n`            | Number format                                         |
    | `:f`            | Fix point number format                               |
    | `:F`            | Fix point number format, in uppercase format (show `inf` and `nan` as `INF` and `NAN`) |
    | `:b`            | Binary format                                         |
    | `:o`            | Octal format                                          |
    | `:d`            | Decimal format                                        |
    | `:x`            | Hex format, lower case                                |
    | `:X`            | Hex format, upper case                                |
    | `:e`            | Scientific format, with a lower case e                |
    | `:E`            | Scientific format, with an upper case E               |
    | `:g`            | General format                                        |
    | `:G`            | General format (using a upper case E for scientific notations)|

/! 辅助符号

* 冒号 `:` 在 "键" 之后
* `:m.nf`, `:#o` 等辅助符号的连用顺序和意义与 [string pattern](#string-pattern-字符串格式化) 中大致一样  
* 与 [string pattern](#string-pattern-字符串格式化) 不同的是, 格式化方法占位符指定的类型和填入的类型必须**一致**

@@ `'{:=+5}'.format(1)` 的输出正号 `+` 与数字 1 之间隔了 4 位

!/

## string pattern 字符串格式化

利用格式符(占位符) `%` 来构造 string pattern

| 格式符   | 数据类型                           |
|----------|----------------------------------|
| %d       | (十进制)整数                       |
| %f 或 %F | 浮点数                             |
| %c       | 字符                               |
| %s       | 字符串                             |
| %e 或 %E | 科学计数法                         |
| %b       | 二进制整数                         |
| %i       | 十进制整数                         |
| %o       | 八进制整数                         |
| %x 或 %X | 十六进制整数                       |
| %g 或 %G | 根据显示长度显示浮点数或科学计数法 |

/!

* 若要在字符串中表示 `%` 本身, 可用 `%%` (`\%`无效)
* `%c` 可以用 ASCII/Unicode 表中的数字表示其字符, 也可以直接填入单个字符的字符串

!/

*[ASCII]: American Standard Code for Information Interchange 美国信息交换标准代码

| 辅助符号 | 说明                                        |
|---------|--------------------------------------------|
| -       | 用做左对齐                                   |
| +       | 在正数前面显示加号                             |
| 0       | 显示的数字**前面**填充 0 而不是默认的空格         |
| m.n     | m 是显示的最小总宽度，n 是小数点后的位数(不足补 0) |
| *       | 定义宽度或者小数点精度                         |
| #       | 在八进制数前面显示 "0o"，在十六进制前面显示"0x"或者"0X"(取决于用的是"%x"还是"%X")    |
| (var)   | 映射变量（通常用来处理字段类型的参数）            |

/!

* `m.n` 采用四舍五入
    * 其实正好的 5 会舍掉, 但只要比 5 大任意小则进一位
* `m.n` 中的 m 考虑小数点 "."
* 使用 `m.n` 若数字不足则默认在数字**前面**填充空格, 再使用 `-` 的话变为数字后面填充空格
* `m` 还可以用于控制 `%c`, `%s` 的位数
* `n` 还可以用于控制 `%s` 截取字符串的前 *n* 位
    * 如 `'%.2s' % 'abc'` 返回 `'ab'`
* 一般辅助符号可以有多个, 但是如 `-` 和 `0` 就不能一起用
    * 对于多个辅助符号一般按上表顺序排列

!/

/@

```py
strpattern = (
    '''%d is for char "%c"
%f turns into %+-9.3f and %09.3f'''
)
output = strpattern % (60,60,7.123123,7.123123,7.123123)
print(output)
```

output:

```text
60 is for char "<"
7.123123 turns into +7.123    and 00007.123
```

@/

## 字符串驻留机制

对于**短字符串** (如仅含英文字母和数字的字符串), 将其赋值给多个不同的对象时, 内存中只有一个副本, 多个对象共享该副本. 长字符串不遵守驻留机制.

## 转义字符

* 通过转义符号 `\` 将普通符号变为特殊符号, 或反之
    * 在转义符号 `\` 前添加 `\` 则使后一个转义符号变为字义符号
        * 即使后一个转义符号可能没起到转义作用
* 在字符串前添加 `r` -> `r'str'` 则忽略字符串 `'str'` 中所有转移符号

| 转义字符 | 代表的符号              |
|----------|-----------------------|
| \n       | 换行符                  |
| \t       | 制表符                  |
| \’       | 单引号                  |
| \”       | 双引号                  |
| \\\      | 一个\                   |
| \ddd     | 3位八进制数对应的字符   |
| \xhh     | 2位十六进制数对应的字符 |

## 常用运算符

### "算术运算符"

* [[Python Operators - Arithmetic Operators#非 算术 功能]]
* 用 `+` 可以**合并连接**字符串 ^12974b
* 用 `*` 可以**重复**字符串
    * 如 `'hello' * 2 = 'hellohello` ^12974a

/@

```py
>>> a = 'hello'
>>> b = 'world'
>>> c = a + ' ' + b
>>> c
'hello world'
```

@/

### 成员判断运算符

* [[Python Operators - Membership Operators]]
    * 如 `'a' in 'apple'` 为 *True*

## 字符串常量

涉及模块: [[Python Modules - string|string]]

| 字符串常量      | 对应字符类 | 具体字符   |
|-----------------|--------|------------|
| `string.digits` | 数字字符   | 0123456789 |
| `string.punctuation` | 标点符号 | !"#$%&\\'()*+,-./:;<=>?@[\\]^_\`{\|}~ |
| `string.ascii_letters` | 英文字母 |ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz |
| `string.printable` | 可打印字符 |0123456789abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ!"#$%&\\'()*+,-./:;<=>?@[\\]^_\`{\|}~ \t\n\r\x0b\x0c |
| `string.ascii_lowercase`| 小写字母 | abcdefghijklmnopqrstuvwxyz |
| `string.ascii_uppercase` | 大写字母 | ABCDEFGHIJKLMNOPQRSTUVWXYZ |

!! 以上字符串常量返回的是**字符串**

## Examples

### Count Characters

@@ [CountChar](file:///D:/010%20LEARNING/Code/Python/Examples/count_char.py)

```python
# Count the frequency of characters from a character sheet in a given string
import string

def CountChar(string, charSet= string.ascii_letters + string.digits):
    stat = {}
    for char in string:
        if char in charSet:
            stat[char] = stat.get(char,0) + 1

    pattern = "The frequency of character %c is %d"
    for char in charSet:
        if stat.get(char,0) > 0:
            print(pattern % (char,stat.get(char)))
```

### Word Count

@@ [WordCount](file:///D:/010%20LEARNING/Code/Python/Examples/word_count.py)

```python
# Count the number of English words in a given string
# Assume that any character that is not an alphabet divides English words

import string

def WordCount(s):
    counter = 0
    inWord = False
    for char in s:
        if not inWord:
            if char in string.ascii_letters:
                inWord = True
                counter += 1
        else:
            if char not in string.ascii_letters:
                inWord = False
    return counter

print(WordCount(input()))
```

### Cycle Cypher

@@ [Cycle Cypher](file:///D:/010%20LEARNING/Code/Python/Examples/cycle_cypher.py)

m-循环加密方式: 对明文每 m 位提取出其字符附于密文列表, 到达明文末尾后在回至其开头, 已经提取出的明文字符不再提取

如 m=3 时, 明文: "abcde" ==> 密文: "caebd"

在已知 m 和密文的情况下如何破译出明文?

```python

# Encryption
def EnCycleCypher(plainText,m):
    plainText = list(plainText)
    cypherText = []
    curIndex = 0
    while plainText:
        curIndex = (curIndex + m - 1) % len(plainText)
        cypherText.append(plainText.pop(curIndex))
    return ''.join(cypherText)

# Decryption
def DeCycleCypher(cypherText,m):
    cypherText = list(cypherText)
    n = len(cypherText)
    index = list(range(n))
    plainText = [None] * len(cypherText)
    curIndex = 0
    for char in cypherText:
        curIndex = (curIndex + m - 1) % len(index)
        plainText[index.pop(curIndex)] = char
    return plainText
```

[//begin]: # "Autogenerated link references for markdown compatibility"
[Python Types]: Python Types "Python Types"
[Python Sequence]: Python Sequence "Python Sequence"
[Python Sequence]: Python Sequence "Python Sequence"
[Python Functions - print]: Python Functions - print "Python Functions - print"
[Python Operators - Membership Operators]: Python Operators - Membership Operators "Python Operators - Membership Operators"
[//end]: # "Autogenerated link references"
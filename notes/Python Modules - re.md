# Python Modules - re

[[Python Modules]]

related: [[Regular Expression]] | [[Python Types - String]]

---

/+

* re 模块是 Python 中的[[Regular Expression|正则表达式]]引擎
* Python 中[[Regular Expression|正则表达式]]即**模式子字符串**
* 用于[[Python Types - String|字符串]]的查找, 替换, 分割

+/

## 两种正则表达式实现方式

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

/! 两种方式的区别

* 这两种方法效果几乎完全一样
* 多个对象方法多了**位置参数**
* 将 pattern 转化为正则表达式对象可以提高对字符串处理速度

!/

## 注意事项

* Python 的字符串中已有含 `\` 的 **[[Python Types - String#转义字符|转义字符]]**, 故正则表达式字符串一般使用 `r'pattern'` 使得 *pattern* 中的 `\` 不被识别为**转义符号**
    * 其实因为 `\n` 等大部分非打印字符作为字符串的转义字符还是作为正则表达式的普通字符含义一致, 故实际影响不大
    * 但出于**规范原因**, Python 识别字符串是会尝试转义 `\` 符号, 而正则表达式中的元字符不是字符串的转义字符, Python 会识别不了
    * 同时出于**方便原因**, 使用原生字符串 raw string 可以专注于正则表达式而无需考虑任何转义字符
        * 比如查找 `a = r'abc\d'` 中的 `\` 字义符号, 以下两个方法等价
            * `re.findall('\\\\',a)`
            * `re.findall(r'\\',a)`
* 可构造查找函数重复使用

    ```python
    def Find(string, pattern):
        regex = re.compile(pattern)
        result = regex.findall(string)
        print(result)
    ```

## 主要函数

| 函数                          | 说明                                        |
|-------------------------------|--------------------------------------------|
|`re.findall(pat,str)`          |返回包含字符串 *str* 中模式 *pat* 所有的匹配项的列表|
|`re.search(pat,str)`           | 在字符串 *str* 中查找模式 *pat*, 若匹配则返回对应 **Match 对象**, 否则返回 *None* |
| `re.match(pat,str)`           | 从字符串 *str* **开始处**查找模式 *pat*, 若匹配则返回对应 **Match 对象**, 否则返回 *None* |
|`re.split(pat,str,[maxsplit])` | 以字符串 *str* 中模式 *pat* 的匹配项为分割符, 返回分割后的字符串**列表**. 可选参数 *maxsplit* 为最大分割次数 |
|`re.sub(pat,repl,str,[count])` | 用字符串 *repl* 替换字符串 *str* 中所有模式 *pat* 的匹配项, 并返回替换后的字符串. 可选参数 *count* 为最大替换次数, 默认为 0, 表示**不限次数** |
|`re.subn(pat,repl,str,[count])`| 用字符串 *repl* 替换字符串 *str* 中所有模式 *pat* 的匹配项, 并返回元组: (替换后的字符串, 替换次数). 可选参数 *count* 为最大替换次数, 默认为 0, 表示**不限次数**|
| `re.compile(pat)`             | 将模式 *pat* 变成一个 **re.Pattern** 对象并返回, 之后可用对象方法处理 |
| `re.escape(pat)`              | 转义模式 *pat* 中所有的元字符为字义符号, 并返回转义后字符串 |

!! 除了 `re.escape()` 上述函数都有可选参数 *flags* (匹配选项)

### `re.findall(pat,str)`

* 返回含字符串 *str* 中所有正则表达式 *pat* 查找到的子字符串的**列表**
* 返回查找值的时候, 转义符号, 非打印字符也会用 `\\`, `\n` 等表示
* 若 *pat* 中有**分组符** `()` 包裹的子模式, 则返回查找值的时候返回的时子模式匹配结果列表
    * 当有多个分组符 `()` 时, 返回的查找值列表每个元素为一个**元组**, 元组包含了每个 `()` 匹配的结果
        * 元组内顺序为从外到内, 从左到右
        * 即使是选择符 `|` 分开的同级子模式, 也会同时显示在元组里, 未被匹配的选择项返回空字符串 `''`
        * 带限定符的子模式, 如 `(pattern)+`, 也只返回**一个**子模式匹配项, 若要返回完整匹配项要用 `((pattern)+)`
    * 使用**非捕获元** `(?:)`, 则**取消该子模式按元组返回**
        * 若无取消所有所有子模式按元组返回, 则返回整体匹配项

/@ 含分组符

```py
>>> import re
>>> s = "this is a test string, a string you can test on"
>>> re.findall(r'a (test )?(str)ing',s) # 平行分组符
[('test ', 'str'), ('', 'str')]
>>> re.findall(r'(a (test )?string)',s) # 嵌套分组符
[('a test string', 'test '), ('a string', '')]
>>> re.findall(r'(a (test )?string|th(is)',s) # 分组符, 选择符混用
[('', '', 'is'), ('a test string', 'test ', ''), ('a string', '', '')]
>>> re.findall(r'a (test )?(?:str)ing',s) # 取消某个子模式按元组返回
['test ', '']
>>> re.findall(r'a (?:test )?(?:str)ing',s) # 取消所有子模式按元组返回
['a test string', 'a string']
>>> re.findall(r'(is )+') # 带限定符的子模式
['is ']
>>> re.findall(r'((is )+)') # 带限定符的子模式
['is is ', 'is ']
```

@/

### `re.search(pat,str)`

* 在字符串 *str* 中匹配模式 *pat*, 若有匹配项则返回对应 **Match 对象**，否则返回 *None*
* 只要字符串中有某一部分被匹配, 则不会返回 *None*
* 从左至右**惰性搜索**, 即找到第一个匹配项后就返回对应 **Match 对象**停止搜索
    * 要搜索全部结果可用 `.search(str,start)` [方法](#主要方法), 改变起始位置 *start* 循环搜索

### `re.match(pat,str)`

* 从字符串 *str* 的**开始处**匹配模式 *pat*, 若匹配则返回一个 **Match 对象**，否则返回 *None*
    * 只要字符串的前面一部分被匹配, 则不会返回 *None*, 故若要匹配**整个字符串**, 可用定位符 `$`

#### Match object

* Match 对象包含信息: 匹配长度, 匹配的子字符串
* Match 对象方法:

| method          | description                                            |
|-----------------|--------------------------------------------------------|
| `.group(index)` | 返回匹配结果的第 *index* 个匹配项, **默认为 0, 为整个模式的匹配项** |
| `.start(index)` | 返回匹配结果的第 *index* 匹配项的起始下标                    |
| `.end(index)`   | 返回匹配结果的第 *index* 匹配项的**结束下标 + 1**            |
| `.span(index)`  | 返回匹配结果的第 *index* 匹配项的范围元组: (起始下标,结束下标+1)|
| `.groups()`     | 返回包含匹配结果中所有子模式匹配项的元组                      |
| `.groupdict()`  | 返回包含匹配的所有命名子模式内容的字典                        |

/@

```py
>>> m = re.match(r'www\.(.*)\..{3}', 'www.python.org')
>>> m.group()
'www.python.org'
>>> m.group(0)
'www.python.org'
>>> m.group(1)
'python'
>>> m.start(1)
4
>>> m.end(1)
10
>>> m.span(1)
(4, 10)
```

@/

### `re.split(pat,str,[maxsplit])`

* 当 *pat* 只由普通字符组成时, 等价于[[Python Types - String|字符串]] 的方法: `str.split(pat,[maxsplit])`

### `re.sub(pat,repl,str,[count])`

* 捕获元不是 `$d`, 而是 `\d`! 记得用 `r` 取消转义符 `\` 作用

### `re.escape(pat)`

* 将 *pat* 中的所有**元字符**转义为普通字符
* 与在所有元字符前加 `\` 作用一致
* 返回的字符串不是 raw string, 故每个元字符前会有**两个 `\`**
    * 例如 `re.escape('http://www.python.org')` 返回 ~~`'http\\:\\/\\/www\\.python\\.org'`~~
        * 其使返回 `'http://www\\.python\\.org'`, 因为 `:` 不在 `[]` 里不被视为元字符

## 主要方法

* 先使用函数 `re.compile(pat,[flags])` 将模式 *pat* 编译为**正则表达式对象 re.Pattern**, 然后使用正则表达式对象的方法处理
    * 使用编译后的正则表达式对象可以**提高字符串处理速度**
* 除了[主要函数](#主要函数)中的 `re.escape()` 和 `re.compile()`, 其余的函数与主要对象方法一一对应, 只是参数有区别

| method                              | description of          |
|-------------------------------------|-------------------------|
| `regex.findall(str,[start, [end]])` | 在指定范围 *str[start:end]* 内查找. 默认范围为整个字符串 *str*, *end* 默认为尾端(包含)|
| `regex.search(str,[start, [end]])`  | 在指定范围 *str[start:end]* 内从左至右搜索. 默认值同上                             |
| `regex.match(str,[start, [end]])`   | 在指定范围 *str[start:end]* 内**从头**搜索. 默认值同上                           |
| `regex.split(str,[maxsplit])`       | 对应参数意义和默认值同函数 `re.split(pat,str,[maxsplit])`                      |
| `regex.sub(repl,str,[count])`       | 对应参数意义和默认值同函数 `re.sub(pat,repl,str,[count])`                     |
| `regex.subn(repl,str,[count])`      | 对应参数意义和默认值同函数 `re.subn(pat,repl,str,[count])`                     |

## Flags

正则表达式的**匹配选项**, 进一步提供匹配规则

| flag                    | description                               |
|-------------------------|-------------------------------------------|
| `re.I`, `re.IGNORECASE` | 忽略大小写                                |
| `re.M`, `re.MULTILINE`  | 多行匹配模式                              |
| `re.S`, `re.DOTALL`     | 使元字符 `.` 也匹配换行符                 |
| `re.U`, `re.UNICODE`    | 匹配 Unicode 字符                         |
| `re.X`, `re.VERBOSE`    | 忽略模式中的空格, 并允许使用 `#` 进行注释 |
| `re.L`, `re.LOCALE`     | 让 `\w\W\b\B\s\S` 与本地字符集有关        |
| `re.A`, `re.ASCII`      | 让 `\w\W\b\B\d\D` 使用 ASCII 字符集 (默认使用 Unicode 字符集) |

!! 用 `|` 组合多个 flags

## 子模式扩展语法

* 非捕获元 `(?=)` 等, 见 [[Regular Expression#非捕获元]]
* 反向引用
    * 命名: `(?P<groupname>)`
        * 命名规则同变量命名规则
    * 引用: `(?P=groupname)`
* 注释 `(?#)`
* 子模式匹配选项 `(?flags:)`
    * 这里的 *flags* 跟一般作为参数的 [flags](#flags)的区别有:
        * 无需前缀 `re.`
        * 要小写
        * 组合直接并写即可, 无需 `|` 分隔
    * 这里的 `:` 不同于非捕获元中的 `:`, 即这里仍是捕获元

[//begin]: # "Autogenerated link references for markdown compatibility"
[Python Modules]: Python Modules "Python Modules"
[Python Types - String]: Python Types - String "Python Types - String"
[//end]: # "Autogenerated link references"
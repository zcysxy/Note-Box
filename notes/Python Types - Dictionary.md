# Python Types - Dictionary

[[Python Types]]

---

## Basics

* 字典是**键值对**的**无序, 可变**对象
* 定义字典时, 每个元素的键和值用冒号 `:` 分隔, 元素之间用逗号 `,` 分隔, 所有的元素放在一对大括号 `{}` 中
* 字典中的每个元素包含两部分 `键: 值`, 向字典添加一个键的同时, 必须为该键增添一个值
* 字典中的键不允许重复
    * 若添加新键为重复键, 则新值覆盖旧值
    * 但字典的值可以重复, 也可以与任意键相同
* 字典中的键可以为**任意不可变数据**, 比如数值, 字符串, 元组等等

## 相关函数

* [[Python Functions - globals|globals]]
* [[Python Functions - locals|locals]]
* [[Python Functions - dict|dict]]

## 字典方法

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

## 访问字典元素

* 以键作为"下标": `dict[key]` 返回 *key* 对应的值
    * 若无 *key* 键, 则报错
* `dict.get(key, [noneValue])`
    * 返回 *key* 对应的值, *key* 存在时等价于 `dict[key]`
    * 若无 *key* 键, 则返回 *noneValue*, 不报错
        * *noneValue* 为可选参数, 默认为**空值** *None*
    * *noneValue* 常设为一个空序列(空列表, 空元组, 空字符串等), 配合 `dict['key'] = dict.get('key',<>)` 来为不存在的键设置初始值, 同时也不影响存在的键值对
* `dict.items()`
    * 将字典键值对组合成一个元组, 返回包含这些元组的 *dict_items* 可迭代对象
        * 可用元组解包提取字典键, 值
    * 例如

        ```py
        >>> Dict = {'x':1, 'y':2, 'z':3}
        >>> List = Dict.items()
        >>> type(List)
        <class 'dict_items'>
        >>> List = list(List)
        >>> List
        [('x', 1), ('y', 2), ('z', 3)]
        >>> for key, value in Dict.items():
        ...    print(key, value)
        ...
        x 1
        y 2
        z 3
        ```

* `dict.keys()`
    * 将字典所有键排成一个列表, 返回包含这个列表的 *dict_keys* 可迭代对象
    * `for x in Dict` 等价于 `for x in Dict.keys()`
* `dict.values()`
    * 将字典所有值排成一个列表, 返回包含这个列表的 *dict_values* 可迭代对象
* [[Python Sequence Unpacking|序列解包]]
    * 字典解包得到的是**键**

## 创建字典

* 赋值: `a = {'a':1, 'b':2, 'c':3}`
    * `a = {}` 建立空字典
* 函数 [[Python Functions - dict|dict]] `a = dict(seq)`
    * `dict()` 返回空字典

## 增添/修改字典元素

* 以指定键为"下标"直接添加/修改元素
    * 若键存在, 则修改该键的值
    * 若键不存在, 则字典添加一个键值对
* `dict.update(dict_2)`
    * 将 %dict_2% 的键值对添加到 %dict% 中
    * 若 %dict% 原有 %dict_2% 中的键, 则此方法**更新**对应值
    * 更新后的 %dict% 仍与 %dict_2% 无关, 两个字典互不影响

## 删除字典元素

* [[Python Statements - del|del]]
    * 可删除整个字典, 也可以删除指定键的键值对
* `dict.pop(key)`
    * 删除并返回键 *key* 对应的值
    * 若 *key* 不存在则报错
* `dict.popitem()`
    * 删除并返回字典中的随机某个元素(元组)
    * 无参数
    * 对同一个字典, 删除元素不随机
        * 删除"最后一个"(形式上)元素
* `dict.clear()`
    * 原地删除字典中所有元素
        * 将原字典变为空字典, 而不是也不会返回一个空字典

## Examples

求序列中每个字符重复出现的字数 [ch_frequency.py](file:///D:/010%20LEARNING/Code/Python/Examples/ch_frequency.py)

```py
# 生成包含 1000 个随机字符的字符串, 然后统计每个字符的出现次数

import string
import random
x = string.ascii_letters + string.digits + string.punctuation
# x = 'abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789!"#$%&\'()*+,-./:;<=>?@[\\]^_`{|}~'
x = [random.choice(x) for i in range(1000)] # 生成长度为 1000 的随机字符列表
x = ''.join(x)   # 将随机字符列表中元素直接(以'')相连形成随机字符串
d = dict() # 生成空的计数字典
for ch in x: # ch 表示字符串 x 中每一个字符
    d[ch] = d.get(ch, 0) + 1 # d.get(ch,0) 保证了若 x 中没有 ch 则计数始终为 0
print(sum(d.values()) == 1000) # 检验频数和是否为 1000
```

[//begin]: # "Autogenerated link references for markdown compatibility"
[Python Types]: Python Types "Python Types"
[//end]: # "Autogenerated link references"
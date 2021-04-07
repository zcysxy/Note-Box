# Python Types - List

# Python 列表

[[Python Types]]

---

## Basics

* 列表是 Python 中内置可变序列, 是一个元素的有序集合
    * 可变指允许改变元素, 增加元素, 删除元素三种操作
    * 因此排序, 倒序也不会改变列表 id
* 列表中的每一个数据称为 **==元素==**,列表的所有元素放在一对中括号 `[]` 中,并使用**逗号**分隔开
    * 无元素时 `[]` 表示**空列表**
* 当列表元素增加或删除时, 列表对象自动进行扩展或收缩内存, 保证元素之间没有缝隙
* 一个列表中的数据类型可以各不相同, 可以分别为整数、实数、字符串等基本类型, 甚至是列表、元素、字典、集合以及其他自定义类型的对象
    * 当列表以子列表为元素时, 称为[[Multi-dimensional List|多维列表]]相当于[[Tensor|张量]], 其中的[[Two-dimensional List|二维列表]]尤其重要, 相当于[[Matrix|矩阵]]

/! "可变"辨析

* 列表和列表中的元素都在缓存里, 列表指向其元素
* 改变列表元素不改变相关元素和列表的缓存, 只改变列表的指向
* 列表的 id 不同于其元素的 id; 不同的列表的元素可能有相同的 id, 都是那个元素本身的 id
* %a% 是一个列表, 则 `b = a` 将 %b% 指向 %a% 且两者 id 相同
    * 此时 %b% 非 %a% 的副本, 即 %a% 变动则 %b% 也变动

![20201010141234](https://raw.githubusercontent.com/zcysxy/Figurebed/master/img/20201010141234.png)

!/

/! 修改列表对象 vs. 修改列表元素

![20201012192811](https://raw.githubusercontent.com/zcysxy/Figurebed/master/img/20201012192811.png)

!/

### 访问列表元素

* `list[i]` 访问列表 %list% 的第 i 个元素, 下标(可正可逆)不能超出列表元素范围
* `list[i] = x` 将列表 %list% 的第 i 个元素改变为 x, 同样下标不能超出列表元素范围

## 相关函数

* [[Python Functions - len|len]]
* [[Python Functions - min, max|min, max]]
* [[Python Functions - sum|sum]]
    * 计算平均值: `sum(list) / len(list)`
* [[Python Functions - list|list]]
* [[Python Functions - sorted|sorted]]
* [[Python Functions - reversed|reversed]]
* [[Python Functions - zip|zip]]
* [[Python Functions - enumerate|enumerate]]

## ⭐️ 列表方法

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

/!

* `list.append(a,x)` 和 `a.append(x)` 作用相同
* 除 `list.copy()` 外其他列表方法均不改变列表对象 (id)
* 一般先用 `list.count` 判断某元素是否存在, 再执行 `list.remove`, `list.index` 等操作
* 注意区分 `list.reverse` 方法和 [[Python Functions - reversed|reversed]] 函数

!/

### list.sort

* 可选参数: **reverse**
    * `list.sort([reverse=True|False])`
    * 默认为 *True*, 表示升序; *False* 表示降序
* 可选参数: **key** (详见 [[Python Functions - sorted|sorted]] 函数, 与其用法一致)
* 不仅可以排列数值元素, 还可以排列元素如字符串(字典序), 列表(字典序), 元组(字典序)等
    * 不同类型元素混合如数值, 字符串混合则无法排序
* 注意与[[Python Functions - sorted|sorted]]函数区分, 一个是原地排序, 一个是产生新列表

### list.copy

* 是浅拷贝
    * **拷贝**指产生一个**副本**, 原列表与拷贝 id 不同. 若是完全拷贝, 则两个列表互不影响
    * "**浅**"指只拷贝一层, 若原列表有多层, 即有其他序列元素, 则作为元素的列表的改变会互相影响

/! 浅拷贝辨析

```python
a = [ [1,2,3], [4,5,6] ]
b = a.copy()
```

错误理解:

![20201010151322](https://raw.githubusercontent.com/zcysxy/Figurebed/master/img/20201010151322.png)

正确理解:

![20201010153009](https://raw.githubusercontent.com/zcysxy/Figurebed/master/img/20201010153009.png)

故改变作为元素的列表 `[1,2,3]` 和 `[4,5,6]` 时, %a% 和 %b% 都会改变

![20201010153249](https://raw.githubusercontent.com/zcysxy/Figurebed/master/img/20201010153249.png)

!/

## 创建列表

方法:

* 赋值: `a = [1,2,3]`
* 拷贝:
    * 列表方法 `list.copy()`: `b = a.copy`
    * [[Python Slice|切片]]: `b = a[::]`
* 函数 [[Python Functions - list|list]] 转化: `a = list((1,2,3))`
* [[List Comprehension|列表推导式]]

## 增添列表元素

* `+`
    * 合并两个列表, 创建一个**新列表**(不影响原来的两个列表)
    * 速度较慢，在涉及大量元素添加时不建议使用

^27efb3

* `*`
    * 将列表与整数相乘 `list * int`, 创建一个**新列表**
    * 新列表是原列表中元素的重复, 故新列表指向的缓存与原列表一样(缓存重用)
        * 因此该操作并不是拷贝 ➡ 重复多级列表时, 一个改变, 新列表也会相应地改变

^27efa3

* `list.append()`
    * 在列表尾部添加元素, **原地**修改列表(不创建新列表, 不改变列表对象)
    * 整个参数作为一个元素添加到列表尾部, 例如

        ```python
        >>> a = [1,2]
        >>> a.append([3])
        >>> a
        [1,2,[3]]
        ```

    * 速度较快, 推荐使用
* `list.extend()`
    * 在列表尾部添加另一个迭代对象的**所有元素**, **原地**修改列表
    * 例如

        ```python
        >>> a = [1,2]
        >>> a.extend((3,4))
        >>> a
        [1,2,3,4]
        ```

    * 不能添加不可迭代对象, 如数值
    * 添加的和被添加的列表互不影响 (不是拷贝)
* `list.insert(index,element)`
    * 将 element 添加至列表的 index 位置
    * 是原地操作
    * 会涉及到插入位置之后所有元素的移动, 影响处理速度, 应尽量避免
* [[Python Slice|切片]]
    * 通过切片操作可以为序列对象增加, 修改, 删除列表中部分元素
    * 由于切片可以超出序列范围, 故可以直接用切片增加元素
        * 如 `list[len(list):] = a` = `list.extend(a)` %a% 为列表

@@ [序列移位](file:///D:/010%20LEARNING/Code/Python/Examples/shift.py)
@@ [交错合并等长列表](file:///D:/010%20LEARNING/Code/Python/Examples/lists_interlaced_combination.py)
@@ [求列表中最长子序列](file:///D:/010%20LEARNING/Code/Python/Examples/longest_monotonic_sublist.py)

## 删除列表元素

* ![[Python Statements - del|del]]
* `list.pop(index)`
    * `list.pop()` 默认删除并返回 %list% 最后一个元素
    * 该操作返回被删除的元素
        * 例如: 对范围内 *index*, `list.insert(index,list.pop(index)) == list` 为真
* `list.remove(x)`
    * 若列表中指定元素 *x* 不存在则抛出异常
* [[Python Slice|切片]]
    * 如 `list[slice] = []` 删除 *slice* 范围中的元素
    * 可配合 [[Python Statements - del|del]] 使用
        * 如 `del list[slice]` 删除 *slice* 范围中的元素

@@ [间隔删除列表元素](file:///D:\010%20LEARNING\Code\Python\Examples\skip_delete_list_elements.py)

## Other

### 优先方法

* 考虑到执行速度, 相比可能引起元素移动的操作: `insert()`, `remove()`, `pop(index)`, `del`, 优先考虑 `append()`, `pop()`

### 可变与不变

循环访问列表元素时, 有时是将元素**拷贝**给**中间变量**, 故不会改变原列表值, 如下:

```py
a = [1,2,3]
for each in a:
    each = each + 1
print(a,each)
```

输出为 `[1,2,3] 4`, *each* 即为中间变量

故一种拷贝方式如下:

```py
a_copy = [each for each in a]
```

[//begin]: # "Autogenerated link references for markdown compatibility"
[Python Types]: Python Types "Python Types"
[//end]: # "Autogenerated link references"

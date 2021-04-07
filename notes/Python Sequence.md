# Python Sequence

# Python 序列

[[Python]] | [[Python Types]]

---

| 数据类型                            | 特点         | 形式                                |
|-----------------------------------|------------|-------------------------------------|
| [[Python Types - List\|列表]]       | 有序, 可变   | `['hello', 'world']`, `[1,2,3]`     |
| [[Python Types - Tuple\|元组]]      | 有序, 不可变 | `('hello', 'world')`, `(1,2,3)`     |
| [[Python Types - Dictionary\|字典]] | 无序, 可变   | `{'x':'hello', 'y':'world', 'z':3}` |
| [[Python Types - Set\|集合]]        | 无序, 可变   | `{'hello', 'world', 3}`             |
| [[Python Types - String\|字符串]]   | 有序, 不可变 | `'hello world'`                     |
| [[Python Functions - range\|range]] | 有序, 不可变, 一段范围内的数值序列 | `range(1,100)`|

!! Python 官方文档中的序列类型是 "strings, lists, tuples, buffers, range objects, binary data" 即上表中有序类型加 binary data

## 索引

* 除字典和集合之外, 列表, 元组, 字符串等序列均支持**双向索引**
    * 第一个元素下标为 ++0++, 第二个元素下标为 1, 以此类推
    * 最后一个元素下标为 ++-1++, 倒数第二个元素下标为 -2, 以此类推
* 序列长度函数 [[Python Functions - len|len]]

## 成员资格判断

* ![[Python Operators - Membership Operators]]

## 序列比较

* 关系运算符: `>`, `>=`, `<`, `<=`, `==`, `!=`
* 任意两个序列可用 `==`, `!=` 比较
* 可用 `>`, `>=`, `<`, `<=` 比较的两个序列需满足: **两个序列类型一样, 且不为 range 或字典序列**
* 可比较**有序**序列比较规则: **字典关系**
    1. 若前 *i* (*i*>=0) 个元素一样, 第 *i+1* 个元素序更大的序列更大
    2. 若前 *i* (*i*>=0) 个元素一样, 且一个序列只有 *i* 个元素, 另一个有多于 *i* 个元素的序列更大
        * ➡ 空集最小
* [[Python Types - Set|集合]]序列比较规则: **包含关系**

/!

bool 值 *True* 和 *False* 可以做数值运算, *True* 代表 1, *False* 代表 0. 故可通过 `(a > b) - (b > a)` 等类似的表达式来比较序列

!/

### 对象方法

对象方法与关系运算符等价, 也可以比较序列. 等价表:

| 关系运算符  |  对象方法     |
|------------|--------------|
| a > b      | a._\_gt__(b) |
| a >= b     | a._\_ge__(b) |
| a < b      | a._\_lt__(b) |
| a <= b     | a._\_le__(b) |
| a == b     | a._\_eq__(b) |
| a != b     | a._\_ne__(b) |

## 切片

![[Python Slice]]

## 序列解包

![[Python Sequence Unpacking]]

[//begin]: # "Autogenerated link references for markdown compatibility"
[Python]: Python "Python"
[Python Types]: Python Types "Python Types"
[Python Operators - Membership Operators]: Python Operators - Membership Operators "Python Operators - Membership Operators"
[Python Slice]: Python Slice "Python Slice"
[Python Sequence Unpacking]: Python Sequence Unpacking "Sequence Unpacking"
[//end]: # "Autogenerated link references"
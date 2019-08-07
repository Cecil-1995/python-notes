@[TOC](目录)
# 一、Python基础
## 1. 数据类型和变量
- 整数
	- ``//``表示地板除，整数地板除整数结果还是整数，保留整数部分
	- 没有大小限制
- 浮点数
	- 没有大小限制，超出了一定范围就直接使用``inf``（无限大）表示
- 字符串
	- 使用反斜杠``\``表示转义，如``\\,\t,\n,\'``
	- 使用``r''``表示``''``内部的字符串不转义
	- 使用``'''...'''``的格式表示多行
- 布尔值（``True``,``False``）
	- ``and`` 与运算，``or`` 或运算，``not`` 非运算
- 空值（``None``）
- 变量
	- 大小写字母、数字和_的组合，不能以数字开头
- 常亮
	- 通常使用全部大写的字母表示

## 2. 字符串和编码
* ``ASCII``编码，由美国人发明，无法表示中文等字符
* ``GB2312``编码，中国制定的，用来把中文编码进去。每个国家都制定了自己的编码，就出现了乱码的情况
* ``Unicode``编码，所有语言都编码在里面。ASCII 编码是 1 个字节，而 Unicode 编码通常是 2 个字节，造成了浪费
* ``UTF-8``编码，UTF-8 编码把一个 Unicode 字符根据不同的数字大小编码成 1-6 个字节，常用的英文字母被编码成 1 个字节，汉字通常是 3 个字节，只有很生僻的字符才会被编码成 4-6 个字节
* 对于单个字符的编码，``ord(char)``函数获取字符的整数表示，``chr(int)``函数把编码转换为对应的字符
```python
>>> ord('A')
65
>>> ord('中')
20013
>>> chr(66)
'B'
>>> chr(25991)
'文'
```
* Python 对``bytes``类型的数据用带b前缀的单引号或双引号表示：``x = b'ABC'``
* 以 Unicode 表示的 str 通过``encode(code)``方法可以编码为指定(code)的bytes。
* 反过来，使用``decode(code)``，如果bytes中只有一小部分无效的字节，可以传入errors='ignore'忽略错误的字节
```python
>>> b'\xe4\xb8\xad\xff'.decode('utf-8', errors='ignore')
'中'
```
* ``len(str)``获取字符串长度
* 格式化使用占位符（%d,%f,%s,%x(十六进制整数)）。如果要输出``%``，转义``%%``
* 另一种格式化字符串的方法是使用字符串的format()方法，它会用传入的参数依次替换字符串内的占位符{0}、{1}
```python
>>> 'Hello, {0}, 成绩提升了 {1:.1f}%'.format('小明', 17.125)
'Hello, 小明, 成绩提升了 17.1%'
```
## 3. list 和 tuple
### list
* list是一种有序的集合，可以随时添加和删除其中的元素
```python
>>> classmates = ['Michael', 'Bob', 'Tracy']
>>> classmates
['Michael', 'Bob', 'Tracy']
```
* ``len(classmates)``函数获取list元素的个数
* 使用从0开始的索引访问每个元素，超出范围，会报``IndexError``的错误
* 获取最后一个元素可以直接使用-1做索引，以此类推，倒数第二个-2，倒数第三个-3
* 使用``append(str)``追加元素，``classmates.append('Adam')``
* 使用``insert(index, str)``插入到指定index位置
* 使用``pop()``删除末尾元素，使用``pop(index)``删除索引为index的元素
### tuple
* 元组。一旦初始化，就不能修改了，和list相似。``classmates = ('Michael', 'Bob', 'Tracy')``
* 没有``append(),insert()``方法，获取元素的方法同 list,但是不能再进行赋值修改
* tuple 不可变，所以代码更安全。如果可能，能用 tuple 代替 list 就尽量用 tuple
* 如果要定义只有一个元素的 tulpe，加上逗号``,``和小括号区分开来，``a = (1,)``
* 可变元组
```python
>>> t = ('a', 'b', ['A', 'B'])
>>> t[2][0] = 'X'
>>> t[2][1] = 'Y'
>>> t
('a', 'b', ['X', 'Y'])
```
## 4. 条件判断
```python
if <条件判断1>:
    <执行1>
elif <条件判断2>:
    <执行2>
elif <条件判断3>:
    <执行3>
else:
    <执行4>
```
* ``int(str)``函数可以将字符串转成数字
## 5. 循环
* for...in循环
```python
names = ['Michael', 'Bob', 'Tracy']
for name in names:
    print(name)
```
* ``range(int)``函数生成从 0 到 int-1 的整数序列
* ``list()``函数转换为list
```python
>>> list(range(5))
[0, 1, 2, 3, 4]
```
* while循环
```python
sum = 0
n = 99
while n > 0:
    sum = sum + n
    n = n - 2
print(sum)
```
* ``break,continue``
## 6. dict 和 set
### dict
* 使用键-值存储的字典（dictionary）
```python
>>> d = {'Michael': 95, 'Bob': 75, 'Tracy': 85}
>>> d['Michael']
95
```
* 使用``in``判断key是否存在，``'Thomas' in d``
* 通过dict提供的``get(str, default)``方法，如果key不存在，可以返回None，或者自己指定的value，``d.get('Thomas', -1)``
* 使用``pop(key)``删除指定指定键值对
* key必须是不可变对象
### set
* set和dict类似，也是一组key的集合，但不存储value。由于key不能重复，所以，在set中，没有重复的key。
```python
>>> s = set([1, 2, 2, 3])
>>> s
{1, 2, 3}
```
* 使用``add(key)``函数添加元素到set
* ``remove(key)``删除元素
* set可以看成数学意义上的无序和无重复元素的集合，因此，两个set可以做数学意义上的交集、并集等操作
```python
>>> s1 = set([1, 2, 3])
>>> s2 = set([2, 3, 4])
>>> s1 & s2
{2, 3}
>>> s1 | s2
{1, 2, 3, 4}
```
# 二、函数
## 1. 调用函数
* 内置函数 https://docs.python.org/zh-cn/3/library/functions.html
* 函数名其实就是指向一个函数对象的引用，完全可以把函数名赋给一个变量，相当于给这个函数起了一个“别名”：
```python
>>> a = abs # 变量a指向abs函数
>>> a(-1) # 所以也可以通过a调用abs函数
1
```
## 2. 定义函数
* 定义一个函数要使用def语句，依次写出函数名、括号、括号中的参数和冒号:，然后，在缩进块中编写函数体，函数的返回值用return语句返回。
```python
def my_abs(x):
    if x < 0:
        return -x
    else:
        return x
```
* 定义一个空函数可以使用``pass``语句（暂时还不知道怎么写函数，占位符，使代码能够正常运行），pass 也可以用在其他地方，比如 if
* ``isinstance(param, (type1, type2))``函数检查param的数据类型是否为type1或者type2
* 返回多个值
```python
import math

def move(x, y, step, angle=0):
    nx = x + step * math.cos(angle)
    ny = y - step * math.sin(angle)
    return nx, ny

x, y = move(100, 100, 60, math.pi / 6)
print(x, y)
#151.96152422706632 70.0

#或者
r = move(100, 100, 60, math.pi / 6)
print(r)
#(151.96152422706632, 70.0)
#其实就是一个tuple
```
* 如果函数没有 return，会自动返回 None
## 3. 函数的参数
### 位置参数
* 类似于``def f(x, y):``这种
### 默认参数
* 类似于``def f(x, y = 1):``这种
* 必选参数在前，默认参数在后
* 调用时默认参数可以不按照顺序，把参数名加上即可。比如定义时``def enroll(name, gender, age=6, city='Beijing'):``，而调用时``enroll('Adam', 'M', city='Tianjin')``
* 默认参数必须指向不变对象
### 可变参数
* 传入的参数个数是可变的，可以是1个、2个到任意个，还可以是0个。使用一个*定义可变参数
```python
def calc(*numbers):
    sum = 0
    for n in numbers:
        sum = sum + n * n
    return sum

>>> calc(1, 2)
5
>>> calc()
0
```
* 如果调用时传的参数是 list 或者 tuple，则可以使用以下形式
```python
>>> nums = [1, 2, 3]
>>> calc(*nums)
14
```
*nums 表示把 nums 这个 list 的所有元素作为可变参数传进去
### 关键字参数
* 可变参数允许你传入0个或任意个参数，这些可变参数在函数调用时自动组装为一个 tuple。而关键字参数允许你传入0个或任意个含参数名的参数，这些关键字参数在函数内部自动组装为一个 dict。使用两个*定义关键字参数
```python
def person(name, age, **kw):
    print('name:', name, 'age:', age, 'other:', kw)
```
```python
>>> person('Michael', 30)
name: Michael age: 30 other: {}
>>> person('Bob', 35, city='Beijing')
name: Bob age: 35 other: {'city': 'Beijing'}
>>> person('Adam', 45, gender='M', job='Engineer')
name: Adam age: 45 other: {'gender': 'M', 'job': 'Engineer'}
```
* 如果有个 dict，则可以直接使用两个**进行调用
```python
>>> extra = {'city': 'Beijing', 'job': 'Engineer'}
>>> person('Jack', 24, **extra)
name: Jack age: 24 other: {'city': 'Beijing', 'job': 'Engineer'}
```
### 命名关键字参数
* 用来限制关键字参数的名字，只接受部分作为关键字参数
```python
def person(name, age, *, city, job):
    print(name, age, city, job)
```
* *后面的参数被视为命名关键字参数
* 如果函数定义中已经有了一个可变参数，后面跟着的命名关键字参数就不再需要一个特殊分隔符*了
```python
def person(name, age, *args, city, job):
    print(name, age, args, city, job)
```
* 命名关键字参数可以有缺省值，从而简化调用
```python
def person(name, age, *, city='Beijing', job):
    print(name, age, city, job)
```
### 参数组合
* 参数顺序：必选参数（位置参数）、默认参数、可变参数、命名关键字参数和关键字参数
* 对于任意函数，都可以通过类似func(*tuple, **dict)的形式调用它，无论它的参数是如何定义的
## 4. 递归函数
* 如果一个函数在内部调用自身本身，这个函数就是递归函数
* 函数调用是通过栈（stack）这种数据结构实现的，每当进入一个函数调用，栈就会加一层栈帧，每当函数返回，栈就会减一层栈帧。由于栈的大小不是无限的，所以，递归调用的次数过多，会导致栈溢出
* 尾递归是指，在函数返回的时候，调用自身本身，并且，return语句不能包含表达式
# 三、高级特性
## 1. 切片
## 2. 迭代
## 3. 列表生成式
## 4. 生成器
## 5. 迭代器

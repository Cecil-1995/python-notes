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
* 取一个 list 或 tuple 的部分元素
* ``L[0:3]``表示，从索引 0 开始取，直到索引 3 为止，但不包括索引 3。即索引 0，1，2，正好是 3 个元素
* 如果第一个索引是 0，则可以省略
* 倒数第一个的索引为 -1，使用负数时表示倒数切片，同理 -1 可以省略
* ``L[0:10:step]``表示取出前十个元素中每隔 step 的元素
* ``L[:]``表示复制一个 L
* 字符串``'xxx'``也可以看成是一种 list，每个元素就是一个字符
## 2. 迭代
* 默认情况下，dict迭代的是key。如果要迭代value，可以用for value in d.values()，如果要同时迭代key和value，可以用for k, v in d.items()
* 字符串也可以进行迭代。``for ch in 'ABC':``
* 通过 collections 模块的 Iterable 类型可以判断是否为可迭代对象
```python
>>> from collections import Iterable
>>> isinstance('abc', Iterable) # str是否可迭代
True
>>> isinstance([1,2,3], Iterable) # list是否可迭代
True
>>> isinstance(123, Iterable) # 整数是否可迭代
False
```
* ``enumerate(list)``函数可以把一个list变成索引-元素对，这样就可以在 for 循环中同时迭代索引和元素本身
```python
>>> for i, value in enumerate(['A', 'B', 'C']):
...     print(i, value)
...
0 A
1 B
2 C
```
## 3. 列表生成式
* 用来创建 list 的生成式
* 要生成``list[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]``可以用``list(range(1, 11))``
* ``[x * x for x in range(1, 11)]``用来生成``[1x1, 2x2, 3x3, ..., 10x10]``，即``[1, 4, 9, 16, 25, 36, 49, 64, 81, 100]``
* ``[要生成的元素 for 迭代元素 in 迭代对象 if 元素满足条件]``
* 还可以使用两层循环，可以生成全排列：
```python
>>> [m + n for m in 'ABC' for n in 'XYZ']
['AX', 'AY', 'AZ', 'BX', 'BY', 'BZ', 'CX', 'CY', 'CZ']
```
## 4. 生成器
* 一边循环一边计算的机制，称为生成器：``generator``
* 只要把一个列表生成式的 [] 改成 ()，就创建了一个 generator:
```python
>>> L = [x * x for x in range(10)]
>>> L
[0, 1, 4, 9, 16, 25, 36, 49, 64, 81]
>>> g = (x * x for x in range(10))
>>> g
<generator object <genexpr> at 0x1022ef630>
```
* 通过``next(generator)``函数 generator 的下一个返回值，或者也可以直接使用 for 循环进行迭代
* 如果一个函数定义中包含 yield 关键字，那么这个函数就不再是一个普通函数，而是一个 generator
* 函数是顺序执行，遇到 return 语句或者最后一行函数语句就返回。而变成 generator 的函数，在每次调用 next() 的时候执行，遇到 yield 语句返回，再次执行时从上次返回的 yield 语句处继续执行
* 用 for 循环调用 generator 时，拿不到 generator 的 return 语句的返回值。如果想要拿到返回值，必须捕获 StopIteration 错误，返回值包含在 StopIteration 的 value 中
## 5. 迭代器
* 可以被 next() 函数调用并不断返回下一个值的对象称为迭代器：Iterator。它们表示一个惰性计算的序列
* 生成器都是Iterator对象，但 list、dict、str 虽然是 Iterable，却不是 Iterator
* 把 list、dict、str 等 Iterable 变成 Iterator 可以使用 iter() 函数
* 凡是可作用于 for 循环的对象都是 Iterable 类型

# 四、函数式编程
## 1. 高阶函数
* 把函数作为参数传入，这样的函数称为高阶函数，函数式编程就是指这种高度抽象的编程范式
### map/reduce
* ``map(function,Iterable)``，对序列的每个元素执行 function 函数
* reduce 把一个函数作用在一个序列[x1, x2, x3, ...]上，这个函数必须接收两个参数，reduce 把结果继续和序列的下一个元素做累积计算，比如：
```python
reduce(f, [x1, x2, x3, x4]) = f(f(f(x1, x2), x3), x4)
```
### filter
* ``filter(function,Iterable)``，对序列的每个元素执行 function 函数，只返回为 True 的元素
### sorted
* ``sorted(list)``，从小到大排序
* ``sorted(list， k=abs)``，按照元素的绝对值从小到大排序，abs 是个函数
* 默认情况下，对字符串排序，是按照ASCII的大小比较的
* 对字符串忽略大小写进行排序。``sorted(['bob', 'about', 'Zoo', 'Credit'], key=str.lower)``
* 反向排序。加上第三个参数reverse，``sorted(['bob', 'about', 'Zoo', 'Credit'], key=str.lower, reverse=True)``
## 2. 返回函数
* A函数里面定义B函数，A函数最后 return B函数，调用A函数时返回函数，需要再次调用这个函数
* 返回函数不要引用任何循环变量，或者后续会发生变化的变量。（因为不是立即执行的）
## 3. 匿名函数
* ``lambda x: x * x``就是一个匿名函数，冒号前面的 x 表示函数参数
## 4. 装饰器
* 函数对象有一个``__name__``属性，可以拿到函数的名字
* 在代码运行期间动态增加功能的方式，称之为“装饰器”（Decorator）
* @语法
## 5. 偏函数
* 用来修改固定函数参数的默认值，返回一个新的函数
* ``functools.partial``
# 五、模块
* 一个.py文件就成为一个模块（Module）
* 按目录来组织模块的方法称为包（Package），之后每个模块名之前都加上这个包名。``package.module``
* 每个包的目录下面都必须包含一个``__init__.py``文件，可以为空，也可以有代码，本身就是一个模块，模块名就是这个报名
* 通过在交互环境下执行``import abc``，可以检测系统是否已经存在 abc 模块
* 任何模块代码的第一个字符串都被视为模块的文档注释
* ``__author__``变量表示作者，``__doc__``也可以用来表示文档注释
* ``sys``模块的``argv``变量用来保存命令行的所有参数
* 命令行运行模块式，``__name__``变量被置为``__main__``
* 类似``_xxx``和``__xxx``这样的函数或变量就是非公开的（private），**不应该**被直接引用。是**不应该**，不是**不能**
* 安装第三方模块，是通过包管理工具``pip``完成的
* [Anaconda](https://www.anaconda.com/)
* 搜索路径存在 sys 模块的 path 变量中
* 需要添加自己的搜索路径时，可以直接使用``sys.path.append('')``进行添加（运行时修改，运行结束失效）。也可以设置环境变量``PYTHONPATH``

# 六、面向对象编程
* 类型通常是大写开头的单词
```python
class Student(object):
    pass
```
object表示继承的类
* ``__init__``函数在对象初始化的时候执行，第一个参数``self``表示本身
* 类中定义的函数第一个参数永远是实例变量``self``
* __开头的变量为私有变量，只有内部才能访问（其实Python解释器把这个变量改成了``_类名__变量名``，所以其实可以通过``_类名__变量名``来访问这个变量，不同版本的解释器，名字可能不一样）
* ``file-like objec``鸭子类型，当某个方法需要某种类型的对象作为参数时，并不一定非要这种类型的对象才可以，只要这个对象有相应的方法就可以了（动态语言）
* ``type()``返回对应的类型
* types 模块，``types.FunctionType`` ``types.BuiltinFunctionType`` ``types.LambdaType`` ``types.GeneratorType``
* 如果要获得一个对象的所有属性和方法，可以使用``dir()``函数，它返回一个包含字符串的 list。``__xxx__``属性或者方法在调用时除了使用``'ABC.__xxx__()'``还可以直接使用``xxx('ABC')``，自己写的类，也可以定义成``__xxx__``形式
* ``hasattr(obj, 'x') # 有属性'x'吗`` ``setattr(obj, 'y', 19) # 设置一个属性'y'`` ``getattr(obj, 'y', default) # 获取属性'y'``
* 实例属性优先级高于类属性
* 使用``del s.name``删除实例 s 的 name 属性

# 七、面向对象高级编程
* 可以给实例绑定属性或者方法
* ``__slots__``变量限制实例添加的属性，对于继承的子类不起作用
```python
 __slots__ = ('name', 'age') # 用tuple定义允许绑定的属性名称
```
* ``@property``装饰器获取属性值，``@attr.setter``设置属性值
* 多重继承，集成多个父类，从而拥有多个父类的所有方法。这种设计称为``MixIn``
* ``__str__()``方法，``__repr__()``方法
* ``__iter__()``方法返回一个迭代对象，使类可以使用``for...in..``循环
* ``__getitem__()``方法使像 list 那样，可以按照下标取出元素
* ``__setitem__()``方法，把对象视作 list 或 dict 来对集合赋值
* ``__delitem__``方法，用于删除某个元素
* ``__getattr__()``方法，动态返回一个属性
* ``__call__()``方法，对实例本身进行调用
* ``Callable()``判断一个对象能否被调用
* 枚举类``Enum``，``@unique``装饰器检查保证没有重复值
* ``type()``函数可以查看一个类型或变量的类型
* ``type()``函数既可以返回一个对象的类型，又可以创建出新的类型
* ``metaclass``元类允许你创建类或者修改类
# 八、错误、调试和测试
## 1. 错误处理

# 文章参考
* Python 新员工教材(楚广明 2012)
* Python基础教程（第2版）

## Python 概述
1. Python 使用强制缩进的编码风格,并以此组织代码块
2. Python 语句结尾不用分号
3. Python 标明注释用#(单行)或三引号(多行)
4. Python 语言没有入口方法(main),代码会从头到尾顺序执行
5. Python 用 import 引用所需要的模块

## 基本数据类型
>一切数据是对象,一切命名是引用

Python 与 java 的变量(函数、类等其他标识符)的命名规范基本一样,同样对大小写敏感。不一样的地方
是Python 中以下划线开始或者结束的标识符通常有特殊的意义。例如以一个下划线开始的标识符如\_foo 不能用
from module import \*语句导入。前后均有两个下划线的标识符,如\_\_init\_\_被特殊方法保留。前边有两个下
划线的标识符,如\_\_bar,被用来实现类私有属性。

Python 没有常量,如果你非要定义常量,可以参考例子`const.py`和`use_const.py`

### 常见的数据类型
#### 空类型
空类型(None)表示该值是一个空对象,比如没有明确定义返回值的函数就是返回None。
空类型没有任何属性,经常被用做函数中可选参数的默认值。None 的布尔值为假。

#### 布尔类型
Python 中用 True 和 False 来定义真假
在Python中,None, 任何数值类型中的0, 空字符串'', 空元组(), 空列表[], 空字典{}都被当作False, 其他对象均为True.

#### 数值类型
Python 拥有四种数值类型: 整型(int)、长整型(long)、浮点类型(float)以及复数类型(complex)。
这些类型是不可变的，就是说整数对象一旦创建，其值便不可更改。相反，系统将创建新的简单类型对象并将其赋值给变量。通过 Python id 函数，可以查看基本 PyObject 标识的变更方式：
另外str类型同样是不可变的。
<pre>
eg:使用 Python id 函数
>>> i = 100 
>>> id(i)
8403284
>>> i = 101
>>> id(i)
8403296
</pre>

#### 列表(list)
Python包含6种内建的序列：列表，元组，字符串，Unicode字符串，buffer对象和xrange对象。

列表和远祖的主要区别在于：列表可以修改，元组则不能
##### 通用序列操作
1. 索引
<pre>
>>> a='hello'
>>> a[0]
'h'
>>> a[-1]
'o'
</pre>

2. 切片
分片操作是需要提供两个索引作边界的，第一个索引的元素是包含在分片内，第二个不包含
<pre>
>>> a='hello,world'
>>> a[2:6]
'llo,'
>>> a[-7:-1]
'o,worl'
# 切片中最左边的索引比最右边的在序列中晚出现，结果就是一个空的序列
>>> a[-2:-6]
''
>>> a[:3]
'hel'
>>> a[3:]
'lo,world'
>>> a[:]
'hello,world'

# 指定步长n，从开始到结束每隔(n-1)个元素
>>> a[::3]
'hlwl'
# 步长为负数时，从右开始往左数
>>> a[::-3]
'dooe'
# 步长不能为0
>>> a[::0]
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ValueError: slice step cannot be zero
</pre>

3. 序列相加
<pre>
>>> [1,2,3]+[3,4,5]
[1, 2, 3, 3, 4, 5]
>>> 'hello' + 'world'
'helloworld'
# 只有相同类型的序列才可以相加
>>> [1,2,3] +'hello'
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: can only concatenate list (not "str") to list
</pre>

4. 乘法
<pre>
>>> print '=' * 5
pythonpythonpythonpythonpython
>>> print 'x' * 10
xxxxxxxxxx
>>> [1,2,3] * 3
[1, 2, 3, 1, 2, 3, 1, 2, 3]
</pre>

5. 成员资格
<pre>
>>> a ='hello'
>>> 'h' in a
True
>>> 'w' in a
False
</pre>

6. 长度，最大值和最小值
<pre>
>>> a=[5,2,4]
>>> len(a)
3
>>> max(a)
5
>>> min(a)
2
>>>
</pre>

##### 列表常见操作
1. 赋值
<pre>
>>> x=[1,2,3]
>>> x[1]=4
>>> x
[1, 4, 3]
</pre>

2. 删除元素
<pre>
>>> x=[1,2,3]
>>> del x[1]
>>> x
[1, 3]
</pre>

3. 切片赋值
<pre>
>>> a=list('perl')
>>> a[2:]=list('ar')
>>> a
['p', 'e', 'a', 'r']
# 与原序列不等长赋值
>>> a[1:]=list('ython')
>>> a
['p', 'y', 't', 'h', 'o', 'n']
# 在不替换任何元素的情况下插入新元素
>>> b=[1,5]
>>> b[1:1]=[2,3,4]
>>> b
[1, 2, 3, 4, 5]
# 删除元素
>>> b[1:4]=[]
>>> b
[1, 5]
</pre>

4. 常用函数
append(x) 尾部追加 单个对象 x,使用多个对象会引起异常。
count(x) 返回对象 x 在 list 中出现的次数
extend(L) 将列表 L 中的项添加到表中
index(x) 返回匹配对象 x 第一个表项的索引,无匹配时产生异常
insert(i,x) 在索引‘i’的元素前插入对象 x
pop(x) 删除列表中索引 x 的表项,并返回同该表项的值,无参数删除最后一个元素
remove(x) 删除表匹配对象 x 的第一个元素,无匹配时异常
reverse() 颠倒列表元素的顺序
sort() 对列表排序

上面append， extend， insert， remove，reverse，sort都是直接修改原来的列表，而不是返回一个新的列表
<pre>
# append
>>> a=[1, 2, 3]
>>> b=a.append(4)
>>> b
>>> a
[1, 2, 3, 4]

# count
>>> b=list('hello')
>>> b.count('l')
2

# extend
>>> a = [1, 2, 3]
>>> b = [4, 5, 6]
>>> a.extend(b)
>>> a
[1, 2, 3, 4, 5, 6]

# index
>>> b=list('hello')
>>> b.index('e')
1
>>> b.index('w')
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ValueError: 'w' is not in list

# insert
>>> a = [1, 2, 3, 4]
>>> a.insert(2, 0)
>>> a
[1, 2, 0, 3, 4]

# pop
>>> a.pop()
4
>>> a
[1, 2, 0, 3]
>>> a.pop(2)
0

# remove
>>> a=list('hello')
>>> a.remove('l')
>>> a
['h', 'e', 'l', 'o']
>>> a.remove('w')
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ValueError: list.remove(x): x not in list

# reverse
>>> a=[1, 2, 3]
>>> a.reverse()
>>> a
[3, 2, 1]

# sort
>>> a = [4, 6, 5, 1, 7]
>>> a.sort()
>>> a
[1, 4, 5, 6, 7]

# sorted函数，会返回排好续的列表
>>> a = [4, 6, 5, 1, 7]
>>> b=sorted(a)
>>> b
[1, 4, 5, 6, 7]
>>> a
[4, 6, 5, 1, 7]
</pre>

5. 高级排序
<pre>
>>>help(list.sort)
#sort(...)
#    L.sort(cmp=None, key=None, reverse=False) -- stable sort *IN PLACE*;
#    cmp(x, y) -> -1, 0, 1
#(END)
</pre>
cmp(e1, e2) 是带两个参数的比较函数, 返回值: 负数: e1 < e2, 0: e1 == e2, 正数: e1 > e2. 默认为 None, 即用内建的比较函数. 
key 是带一个参数的函数, 用来为每个元素提取比较值. 默认为 None, 即直接比较每个元素. 
通常, key 和 reverse 比 cmp 快很多, 因为对每个元素它们只处理一次; 而 cmp 会处理多次.
<pre>
>>> students = [('john', 'A', 15), ('jane', 'B', 12), ('dave', 'B', 10)]
# sort by age
>>> students.sort(key=lambda student : student[2])
>>> students
[('dave', 'B', 10), ('jane', 'B', 12), ('john', 'A', 15)]


>>> students = [('john', 'A', 15), ('jane', 'B', 12), ('dave', 'B', 10)]
# sort by age
>>> students.sort(cmp=lambda x, y : cmp(x[2], y[2]))
>>> students
[('dave', 'B', 10), ('jane', 'B', 12), ('john', 'A', 15)]

>>> a = [4, 6, 5, 1, 7]
>>> a.sort(reverse=True)
>>> a
[7, 6, 5, 4, 1]
</pre>

#### 元组(tuple)
元组除了创建和访问元组元素之外，没有什么其他的操作
<pre>
>>> pprint.pprint(dir(tuple))
['__add__',
 '__class__',
 '__contains__',
 '__delattr__',
 '__doc__',
 '__eq__',
 '__format__',
 '__ge__',
 '__getattribute__',
 '__getitem__',
 '__getnewargs__',
 '__getslice__',
 '__gt__',
 '__hash__',
 '__init__',
 '__iter__',
 '__le__',
 '__len__',
 '__lt__',
 '__mul__',
 '__ne__',
 '__new__',
 '__reduce__',
 '__reduce_ex__',
 '__repr__',
 '__rmul__',
 '__setattr__',
 '__sizeof__',
 '__str__',
 '__subclasshook__',
 'count',
 'index']
</pre>

#### 字符串
所有前面介绍的标准的序列操作（索引，切片，乘法，成员资格判断，求长度，最大值，最小值）对字符串同样适用。
但是有一点需要注意的是字符串是不可变的，因此切片赋值是不可以的。

Python中普通的字符串在内部是以ASCII码存储的，而Unicode字符串在存储为16位的Unicode编码
在 Python 中定义一个标准字符串(str)可以使用单引号、双引号、三引号。
字符串前面加r,表示是原始字符串
<pre>
>>> a='Hello,\nWorld'
>>> b=r'Hello,\nWorld'
>>>print a
Hello, 
World
>>>print b
Hello,\nWorld
</pre>
字符串前面加u,表示Unicode字符串
<pre>
>>> a='hello'
>>> b=u'hello'
>>> print type(a)
<type 'str'>
>>> print type(b)
<type 'unicode'>
</pre>

同时需要注意的是的，在使用UTF-8编码时，非unicode字符中一个汉字的长度是3,
gbk是2.unicode字符中一个汉字的长度是1
<pre>
>>> a='中'
>>> a
'\xe4\xb8\xad'
>>> b=u'中'
>>> b
u'\u4e2d'
>>> c=b.encode('gbk')
>>> c
'\xd6\xd0'
>>> print len(a), len(b), len(c)
3 1 2
>>> 
</pre>


字符串格式
<pre>
>>> '%x' % 10
'a'
>>> '%X' % 10
'A'
>>> '%d' % 10
'10'
>>> from math import pi
# 保留小数位数
>>> '%.2f' % pi
'3.14'
# 右对齐
>>> '%10.2f' % pi
'      3.14'
# 左对齐
>>> '%-10.2f' % pi
'3.14      '
# 填充
>>> '%010.2f' % pi
'0000003.14'
# 格式化字符串里面包括百分号的时候，要用%%
>>> '%d%%' % 100
'100%'
</pre>

模板字符串
<pre>
from string import Template
>>> s=Template('Hello $x,my name is $y')
>>> d={'x': 'boy', 'y': 'Lucy'}
>>> s.substitute(d)
'Hello boy,my name is Lucy'
</pre>

常用函数
<pre>
>>> pprint.pprint(dir(str))
['__add__',
 '__class__',
 '__contains__',
 '__delattr__',
 '__doc__',
 '__eq__',
 '__format__',
 '__ge__',
 '__getattribute__',
 '__getitem__',
 '__getnewargs__',
 '__getslice__',
 '__gt__',
 '__hash__',
 '__init__',
 '__le__',
 '__len__',
 '__lt__',
 '__mod__',
 '__mul__',
 '__ne__',
 '__new__',
 '__reduce__',
 '__reduce_ex__',
 '__repr__',
 '__rmod__',
 '__rmul__',
 '__setattr__',
 '__sizeof__',
 '__str__',
 '__subclasshook__',
 '_formatter_field_name_split',
 '_formatter_parser',
 'capitalize',  # 首字母大写
 'center',      # center(width, fillchar) 按照制定的长度width，让字符串居中，填充fillchar
 'count',       
 'decode',
 'encode',
 'endswith',
 'expandtabs',
 'find',
 'format',
 'index',
 'isalnum',
 'isalpha', 
 'isdigit',
 'islower',
 'isspace',
 'istitle',
 'isupper',
 'join',
 'ljust',
 'lower',
 'lstrip',
 'partition',
 'replace',
 'rfind',
 'rindex',
 'rjust',
 'rpartition',
 'rsplit',
 'rstrip',
 'split',
 'splitlines',
 'startswith',
 'strip',
 'swapcase',
 'title',
 'translate',
 'upper',
 'zfill']
</pre>



#### 字典
字典的格式化
<pre>
>>> info = {'name':'lianglin', 'age':25}

>>> 'my name is %(name)s, my age is %(age)d' % info
'my name is lianglin, my age is 25'
</pre>

常用函数
has_keys(x) 若字典中有 x 返回 true
keys() 返回键的列表
values() 返回值的列表
dict.items() 返回 tuples 的列表。每个 tuple 有字典的 dict 的键和相应的值组成
clear() 删除词典的所有条目
copy() 返回字典的高层结构的拷贝,但不复制嵌入结构,而复制那些结构的引用。
update(x) 用字典 x 中的键/值对更新字典的内容。如果字典x中的键不存在元字典中，则原字典添加x字典的键/值信息。
get(x[,y]) 返回键 x。若未找到返回 None
<pre>
# copy 方法实际上是浅复制(shallow copy)
>>> x={'name': 'admin', 'machines': ['foo', 'bar', 'baz']}
>>> y=x.copy()
>>> y['name']='admin_y'
>>> y['machines'].remove('foo')
>>> x
{'name': 'admin', 'machines': ['bar', 'baz']}
>>> y
{'name': 'admin_y', 'machines': ['bar', 'baz']}
>>> 
# 深度复制（deep copy)
>>> from copy import deepcopy
>>> dc =deepcopy(y)
>>> dc
{'name': 'admin_y', 'machines': ['bar', 'baz']}
>>> dc['machines'].append('foo')
>>> dc
{'name': 'admin_y', 'machines': ['bar', 'baz', 'foo']}
>>> y
{'name': 'admin_y', 'machines': ['bar', 'baz']}

# update
>>> x={'name': 'admin', 'machines': ['foo', 'bar', 'baz']}
>>> x.update({'name':'admin_update'})
>>> x
{'name': 'admin_update', 'machines': ['foo', 'bar', 'baz']}
>>> x.update({'time':'now time'})
>>> x
{'name': 'admin_update', 'machines': ['foo', 'bar', 'baz'], 'time': 'now time'}
</pre>

#### 集合(set)
Python 中的集合是指无序的、不重复的
元素集,类似数学中的集合概念,可对其进行交、并、差、补等逻辑运算。
<pre>
>>> a = [2,3,4,2,1]
>>> set(a)
set([1, 2, 3, 4])

>>> a=set('abcd')
>>> b=set('defg')
# 交集
>>> a & b
set(['d'])
# 并集
>>> a | b
set(['a', 'c', 'b', 'e', 'd', 'g', 'f'])
# 差集
>>> a - b
set(['a', 'c', 'b'])
</pre>



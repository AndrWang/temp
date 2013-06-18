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
Python包含6种内建的序列：列表，元祖，字符串，Unicode字符串，buffer对象和xrange对象。

列表和远祖的主要区别在于：列表可以修改，元祖则不能
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



#### 字符串
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
 'capitalize',
 'center',
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

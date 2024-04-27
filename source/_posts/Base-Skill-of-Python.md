---
title: Base Skill of Python
categories: Tech
cover: /imgs/default.jpg
abstracts: SQL
tags:
 - Python
---


## 1. 字符串
*字符串是Python中最常用的数据类型，我们可以使用单引号'或双引号"来创建字符串。input函数获取的输入数据全是字符串类型。*

### 1.1 字符串运算符
字符串对象是不可变对象，无法修改内容，所谓"修改"只是创建新的字符串对象，并把原对象引用指向该新字符串对象。

|操作符|	描述|	实例 a='Hello', b='Python'|
|:---:|:--- |:--- |
|+|	字符串连接|	a+b输出: HelloPython|
|*|	重复输出字符串|	a*2输出: HelloHello|
|[]|	通过索引获取字符串中字符|	a[1]输出: e|
|[:]|	截取字符串的一部分|	a[1:3]输出: el|
|in|成员运算符 - 如果字符串中包含给定的字符返回 True|'H' in a输出: True
|not in|成员运算符 - 如果字符串中不包含给定的字符返回 True|	'A' not in a输出: True|
|r/R|原始字符串 - 原始字符串：所有的字符串都是直接按照字面的意思来使用，没有转义特殊或不能打印的字符。 原始字符串除在字符串的第一个引号前加上字母"r"（可以大小写）以外，与普通字符串有着几乎完全相同的语法。	|print(r'\n')输出: \n|

### 1.2 字符串格式化
*建议使用新的字符串格式化函数str.format()，通过{}和:来代替以前的%。format函数可以接受任意个数的参数，位置也可以不按顺序。*
```
In [1]: "{} {}".format("Hello", "World")
Out[1]: 'Hello World'

In [2]: "{0} {1}".format("Hello", "World")
Out[2]: 'Hello World'

In [3]: person = {'name': 'wangy', 'age': 18}

In [4]: print("姓名: {name}, 年龄: {age}".format(**person))
姓名: wangy, 年龄: 18

In [5]: learn = ['c', 'python']

In [6]: print("静态语言: {0[0]}, 动态语言: {0[1]}".format(learn))
静态语言: c, 动态语言: python
```

**数字格式化:**

- ^, <, >分别是居中、左对齐、右对齐，后面是宽度，:冒号后面是填充的字符，只能是一个字符，不指定则默认是用空格填充。
- +表示在正数前显示+，负数前显示-
- （空格）表示在正数前加空格
- b、d、o、x分别是二进制、十进制、八进制、十六进制
- 使用大括号{% raw %}{{}}{% endraw %}来转义大括号

```
In [1]: a = 'Hello'

In [2]: print('变量a的值: {}，它的对应位置是 {{0}}'.format(a))
变量a的值: Hello，它的对应位置是 {0}
```

### 1.3字符串内建函数
**(1) 字母大小写**
① ```S.upper()```
返回字符串中所有字母的大写形式。
```
In [1]: a = 'hello'

In [2]: a.upper()
Out[2]: 'HELLO'
```
② ```S.lower()```
返回字符串中所有字母的小写形式。
```
In [1]: a = 'HELLO'
In [2]: a.lower()

Out[2]: 'hello'
```
③ ```S.swapcase()```
将字符串中的字母大小写互换。
```
In [1]: a = 'Hello'
In [2]: a.swapcase()
Out[2]: 'hELLO'
```
④ ```S.capitalize()```
整个字符串中只有第一个单词的首字母大写。
```
In [1]: a = 'hello world'
In [2]: a.capitalize()

Out[2]: 'Hello world'
```
⑤ ```S.title()```
整个字符串中所有单词的首字母都大写。
```
In [1]: a = 'hello world'
In [2]: a.title()

Out[2]: 'Hello World'
```
**(2) 格式化**
① ```S.ljust(width[, fillchar])```
获取固定长度，左对齐，右边不够默认用空格补齐。
```
In [1]: a = 'hello'
In [2]: a.ljust(10)

Out[2]: 'hello     '
```
② ```S.rjust(width[, fillchar])```
获取固定长度，右对齐，左边不够默认用空格补齐。
```
In [1]: a = 'hello'
In [2]: a.rjust(10)

Out[2]: '     hello'
```
③ ```S.center(width[, fillchar])```
获取固定长度，中间对齐，两边不够默认用空格补齐。
```
In [1]: a = 'hello'
In [2]: a.center(10)

Out[2]: '  hello   '
```
④ ```S.zfill(width)```
获取固定长度，右对齐，左边不足用0补齐。
```
In [1]: a = 'hello'
In [2]: a.zfill(10)

Out[2]: '00000hello'
```

**(3) 搜索**
① ```S.find(sub[, start[, end]])```
在字符串中搜索子串第一次出现的位置（可以指定搜索范围，默认是整个字符串），如果搜索不到，则返回-1
```
In [1]: a = 'hello world, hello python'

In [2]: a.find('hello')
Out[2]: 0
```
S.find()可以用S.index(sub[, start[, end]])替代，只是如果没有查找到子串时，S.index()会抛异常ValueError
```
index(...)
    S.index(sub[, start[, end]]) -> int

    Like S.find() but raise ValueError when the substring is not found.
```

② ```S.rfind(sub[, start[, end]])```
在字符串中搜索子串最后一次出现的位置（可以指定搜索范围，默认是整个字符串），相当于从右边开始查找。如果搜索不到，则返回-1
```
In [1]: a = 'hello world, hello python'
In [2]: a.rfind('hello')

Out[2]: 13
```
S.rfind()可以用S.rindex(sub[, start[, end]])替代，只是如果没有查找到子串时，S.rindex()会抛异常ValueError

③ ```S.count(sub[, start[, end]])```
在字符串中搜索子串总共出现多少次（可以指定搜索范围，默认是整个字符串），如果搜索不到，则返回0
```
In [1]: a = 'hello world, hello python'
In [2]: a.count('hello')

Out[2]: 2
```

**(4) 替换**
① ```S.replace(old, new[, count])```
在字符串中将old子串替换为new子串，默认替换掉所有old子串
```
In [1]: a = 'hello world, hello python'

In [2]: a.replace('hello', '你好')
Out[2]: '你好 world, 你好 python'

In [3]: a.replace('hello', '你好', 1)
Out[3]: '你好 world, hello python'
```
② ```S[::-1]```
反转字符串
```
In [1]: a = 'hello world'
In [2]: a[::-1]

Out[2]: 'dlrow olleh'
```
**(5) 移除字符串头尾指定的字符**
默认移除空白符(包括\n, \r, \t, )

① ```S.strip([chars])```
移除字符串的首尾字符

In [1]: a = '  \t hello world \r\n '
```
In [2]: a.strip()
Out[2]: 'hello world'

In [3]: a = '---hello world---'

In [4]: a.strip('-')
Out[4]: 'hello world'
```
② ```S.lstrip([chars])```
移除字符串首部字符
```
In [1]: a = '  \t hello world \r\n '

In [2]: a.lstrip()
Out[2]: 'hello world \r\n '

In [3]: a = '---hello world---'

In [4]: a.lstrip('-')
Out[4]: 'hello world---'
```
③ ```S.rstrip([chars])```
移除字符串尾部字符
```
In [1]: a = '  \t hello world \r\n '

In [2]: a.rstrip()
Out[2]: '  \t hello world'

In [3]: a = '---hello world---'

In [4]: a.rstrip('-')
Out[4]: '---hello world'
```
**(6) 按指定子串分割字符串**
① ```S.split(sep=None, maxsplit=-1)```
默认按空白符(包括\n, \r, \t, )分隔为列表，如果指定了maxsplit，则仅分隔maxsplit个子串
```
In [1]: a = '  \t hello world \r\n '

In [2]: a.split()
Out[2]: ['hello', 'world']

In [3]: a = 'a-b-c-d-e'

In [4]: a.split('-')
Out[4]: ['a', 'b', 'c', 'd', 'e']

In [5]: a.split('-', maxsplit=3)
Out[5]: ['a', 'b', 'c', 'd-e']
```
② ```S.splitlines([keepends])```
按字符串中的换行符，分隔成一个包含各行的列表，默认时列表元素中不包含换行符，指定keepends且为True时（非0整数），列表元素中会保留换行符
```
In [1]: a = 'hello\n\tworld, \nhello\n\rpython\nabc'

In [2]: a.splitlines()
Out[2]: ['hello', '\tworld, ', 'hello', '', 'python', 'abc']

In [3]: a.splitlines(1)
Out[3]: ['hello\n', '\tworld, \n', 'hello\n', '\r', 'python\n', 'abc']

In [4]: a.splitlines(0)
Out[4]: ['hello', '\tworld, ', 'hello', '', 'python', 'abc']

In [5]: a.splitlines(True)
Out[5]: ['hello\n', '\tworld, \n', 'hello\n', '\r', 'python\n', 'abc']

In [6]: a.splitlines(False)
Out[6]: ['hello', '\tworld, ', 'hello', '', 'python', 'abc']
```
③ S.partition(sep)
在字符串中查看第一次sep，将字符串分隔成(head, sep, tail)，如果指定的sep不存在，则返回(S, '', '')
```
In [1]: a = 'hello world, hello python'

In [2]: a.partition('hello')
Out[2]: ('', 'hello', ' world, hello python')

In [3]: a.partition('world')
Out[3]: ('hello ', 'world', ', hello python')

In [4]: a.partition('china')
Out[4]: ('hello world, hello python', '', '')
```
④ S.rpartition(sep)
类似于S.partition(sep)，不过是从右边开始查找
```
In [1]: a = 'hello world, hello python'

In [2]: a.rpartition('hello')
Out[2]: ('hello world, ', 'hello', ' python')

In [3]: a.rpartition('china')
Out[3]: ('', '', 'hello world, hello python')
```

**(7) 判断**
① ```S.startswith(prefix[, start[, end]])```
判断字符串是否以prefix子串开头
```
In [1]: a = 'hello world'

In [2]: a.startswith('h')
Out[2]: True

In [3]: a.startswith('H')
Out[3]: False
```
② ```S.endswith(suffix[, start[, end]])```
判断字符串是否以prefix子串结尾
```
In [1]: a = 'hello world'

In [2]: a.endswith('d')
Out[2]: True

In [3]: a.endswith('D')
Out[3]: False
```
③ ```S.isalpha()```
如果字符串中的字符全是字母，则返回True

④ ```S.isdigit()```
如果字符串中的字符全是数字，则返回True

⑤ ```S.isalnum()```
如果字符串中的字符全是字母或数字，则返回True

⑥ ```S.isspace()```
如果字符串中的字符全是空白符(包括\n, \r, \t, )，则返回True

⑦ ```S.islower()```
如果字符串中的字符全是小写字母，则返回True

⑧ ```S.isupper()```
如果字符串中的字符全是大写字母，则返回True

**(8) 连接**
S.join(iterable)使用字符串连接可迭代对象
```
In [1]: a = ['hello', 'world']
In [2]: '_'.join(a)

Out[2]: 'hello_world'
```

## 2. 列表
### 2.1 循环遍历
```
In [1]: a = ['c', 'java', 'python']

In [2]: for i in a:
   ...:     print(i)
   ...:     
c
java
python

In [3]: i = 0

In [4]: while i < len(a):
   ...:     print(a[i])
   ...:     i += 1
   ...:     
c
java
python

In [5]: for key, value in enumerate(a):
   ...:     print('{0} ---> {1}'.format(key, value))
   ...:     
0 ---> c
1 ---> java
2 ---> python
```

### 2.2 常见操作
**(1) 添加元素**
① ```L.append(object)```
向列表末尾添加元素
```
In [1]: a = ['c', 'java', 'python']

In [2]: a.append([1, 2, 3])

In [3]: a
Out[3]: ['c', 'java', 'python', [1, 2, 3]]
```
② ```L.extend(iterable)```
将可迭代对象中的元素逐一添加到列表的末尾
```
In [1]: a = ['c', 'java', 'python']

In [2]: a.extend([1, 2, 3])

In [3]: a
Out[3]: ['c', 'java', 'python', 1, 2, 3]
```
③ ```L.insert(index, object)```
在列表中指定的索引下标位置处，插入元素
```
In [1]: a = ['c', 'java', 'python']

In [2]: a.insert(1, 'c++')

In [3]: a
Out[3]: ['c', 'c++', 'java', 'python']
```
**(2) 删除元素**
① ```del```
删除指定下标的元素或整个列表
```
In [1]: a = ['c', 'java', 'python']

In [2]: del a[0]

In [3]: a
Out[3]: ['java', 'python']

In [4]: del a

In [5]: a
---------------------------------------------------------------------------
NameError                                 Traceback (most recent call last)
<ipython-input-5-60b725f10c9c> in <module>()
----> 1 a

NameError: name 'a' is not defined
```
② ```L.pop([index])```
移除并返回指定下标的列表元素，当不指定下标时，默认删除末尾元素，当列表是空或者下标越界时抛IndexError异常
```
In [1]: a = ['c', 'c++', 'java', 'php', 'python']

In [2]: a.pop()
Out[2]: 'python'

In [3]: a
Out[3]: ['c', 'c++', 'java', 'php']

In [4]: a.pop(2)
Out[4]: 'java'

In [5]: a
Out[5]: ['c', 'c++', 'php']

In [6]: a.pop(5)
---------------------------------------------------------------------------
IndexError                                Traceback (most recent call last)
<ipython-input-6-ebc3db152037> in <module>()
----> 1 a.pop(5)

IndexError: pop index out of range

In [7]: a = []

In [8]: a.pop()
---------------------------------------------------------------------------
IndexError                                Traceback (most recent call last)
<ipython-input-8-353a8f813834> in <module>()
----> 1 a.pop()

IndexError: pop from empty list
```
③ ```L.remove(value)```
移除第一次出现的value元素，如果value不在列表中，则抛ValueError异常
```
In [1]: a = ['c', 'python', 'java', 'php', 'python']

In [2]: a.remove('python')

In [3]: a
Out[3]: ['c', 'java', 'php', 'python']

In [4]: a.remove('ruby')
---------------------------------------------------------------------------
ValueError                                Traceback (most recent call last)
<ipython-input-4-7c4d290ae769> in <module>()
----> 1 a.remove('ruby')

ValueError: list.remove(x): x not in list
```
**(3) 修改元素**
通过下标来确定列表元素，然后进行修改
```
In [1]: a = ['c', 'java', 'python']

In [2]: a[1] = 'php'

In [3]: a
Out[3]: ['c', 'php', 'python']
```
**(4) 查找元素**
① in 与 not in
- in 如果元素存在于列表中，则返回True，否则返回False
- not in 如果元素不存在于列表中，则返回True，否则返回False

```
In [1]: a = ['c', 'c++', 'java', 'php', 'python']

In [2]: 'c#' in a
Out[2]: False

In [3]: 'c#' not in a
Out[3]: True
```
② ```L.index(value, [start, [stop]])```
返回列表中第一次出现value元素的下标，如果value不存在，则抛ValueError异常
```
In [1]: a = ['c', 'python', 'java', 'php', 'python']

In [2]: a.index('python')
Out[2]: 1

In [3]: a.index('python', 2)
Out[3]: 4

In [4]: a.index('c#')
---------------------------------------------------------------------------
ValueError                                Traceback (most recent call last)
<ipython-input-4-9aedd273423d> in <module>()
----> 1 a.index('c#')

ValueError: 'c#' is not in list
```
③ ```L.count(value)```
返回列表中value出现的次数
```
In [1]: a = ['c', 'python', 'java', 'php', 'python']
In [2]: a.count('python')

Out[2]: 2
```
**(5) 排序**
① ```L.sort(key=None, reverse=False)```
默认按由小到大（ASCII）排序列表中的元素，如果reverse=True则反转排序
```
In [1]: a = ['c', 'python', 'java', 'php', 'python']

In [2]: a.sort()

In [3]: a
Out[3]: ['c', 'java', 'php', 'python', 'python']

In [4]: b = [9, 19, 2]

In [5]: b.sort()

In [6]: b
Out[6]: [2, 9, 19]
```
② ```L.reverse()```
将列表元素首尾倒置
```
In [1]: a = ['c', 'python', 'java', 'php', 'python']

In [2]: a.reverse()

In [3]: a
Out[3]: ['python', 'php', 'java', 'python', 'c']
```

## 3. 元组
*不可变对象，一旦创建了元组，则不能再修改元组的元素，包括不能删除其中的元素。*

- tuple.index('value')
- tuple.count('value')
## 4. 字典
- 删除字典元素del dict['name']
- 删除整个字典del dict
- 清空整个字典dict.clear()，变成空字典
- 返回字典中键值对的个数len(dict)
- 返回一个包含字典所有key的列表dict.keys()
- 返回一个包含字典所有value的列表dict.values()
- 返回一个包含字典所有(key, value)键值对元组的列表dict.items()
- 判断key是否在字典中dict.has_key('name')，如果存在键name，则返回True，否则返回False


## 5. 相同点
### 5.1 运算符

|运算符|Python表达式|结果|描述|支持的数据类型|
|:---:|:--- |:--- |:--- |:--- |
|+|[1, 2] + [3, 4]|[1, 2, 3, 4]|合并|字符串、列表、元组|
|*|['Hi!'] * 4|['Hi!', 'Hi!', 'Hi!', 'Hi!']|复制|字符串、列表、元组|
|in|1 in [1, 2, 3]|True|元素是否存在|字符串、列表、元组、字典|
|not in|4 not in [1, 2, 3]|True|元素是否不存在|字符串、列表、元组、字典|

### 5.2 方法

|方法|描述|
|:---:|:--- |
|cmp()	|比较两个值|
|len()	|计算容器中元素个数|
|max()	|返回容器中元素最大值|
|min()	|返回容器中元素最小值|
|del()	|删除容器或容器中元素|

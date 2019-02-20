变量
==

### 定义变量:

```python
a = 1
b = 2
c = 1.23
d = 'test'

# 多个变量赋值
x,y,z=1,'2',3.0
```

### 变量名规则:

* 变量名的长度不受限制，但其中的字符必须是字母、数字、或者下划线（\_），而不能使用空格、连字符、标点富豪号、引号或其他字符。
* 变量名的第一个字符不能是数字，而必须是字母或下划线。
* Python区分大小写。
* 不能将Python关键字用作变量名。

输入:

```python
Temp = input("输入想出入的字符:")
print(Temp)
```

### 输出:

```python
print('test')
```

数据类型:
=====

字符型:
----

### 格式化:

%d %s %f:

```python
# 字符串:
a = "xxx"
print("我宣你:%s" % a)

# %d数字型:
a = 10
b = 20
print("a = %d" % a)
print("%d + %d = %d" % (a, b, a + b))

# 浮点型:
a = 3.1415926
print("圆周率:%f" % a)

# 字典匹配 %s 字符型
a = {"name":"xxx"}
print("我宣你:%(name)s" % a)

```

深入阅读:<https://www.jb51.net/article/134290.htm>

formate:

```python
a = "xxx"
print("我宣你:{}".format(a))

li = ['henry',18]
dict = {'name':'henry','age':18}
# 位置参数
print("我是:{},今年{}岁".format("Henry","18"))
# 关键字参数
print("我是:{name},今年{age}岁".format(name="Henry",age=18))
# 索引参数
print("我是:{1},今年{0}岁".format("18","Henry"))
# 列表参数
print("我是:{},今年{}岁".format(*li))
# 字典参数
print("我是:{name},今年{age}岁".format(**dict))

# 填充与格式化
# :[填充字符][对齐方式 <^>][宽度]
# 右对齐
print('{0:*>10}'.format(10))
# 左对齐
print('{0:*<10}'.format(10))
# 居中对齐
print('{0:*^10}'.format(10))

# 精度与进制
print('{0:.2f}'.format(1 / 3))
print('{0:b}'.format(10))
# 八进制
print('{0:o}'.format(10))
# 16进制
print('{0:x}'.format(10))
# 千分位格式化
print('{:,}'.format(111111111))
```

### 编码:

decode():解码

encode():编码

注:py2默认ASCII码，py3默认的utf8

因为py2默认的是ASCII进行编码,所以当程序一旦出现中文就会无法解码,所以py2的程序中要在开头添加一行注释表明该py2文件要使用UTF-8进行编码

```python
#-*-coding:utf-8-*-
```

Python2

Unicode —\> Str

```python
# -*-coding:utf-8-*-

s = u'中文'
print type(s)

s = s.encode('utf-8')
print type(s)
```

GBK -Unicode-\>UTF-8

注: 将一个str直接编码城另一种编码,py解释会先将str编译成unicode编码再进行目标编码的转换.但由于py2默认是ascii编码,所以我们需要声明str字符串的编码格式

```python
# 声明编码格式
# 方法一
import sys
reload(sys) # Python2.5 初始化后会删除 sys.setdefaultencoding 这个方法，我们需要重新载入
sys.setdefaultencoding('utf-8')

# 方法二
s = '中文'
s.decode('utf-8').encode('gb18030')
```

```python
# -*-coding:utf-8-*-
# GBK -Unicode->UTF-8
s = u'中文'
print type(s)

s = s.encode('gbk')
s = s.decode('gbk').encode('utf-8')
print type(s)
```

Str —\> Unicode

```python
# -*-coding:utf-8-*-


s = u'中文'
print type(s)

s = s.encode('gbk')
s = unicode(s, 'gbk')
print type(s)
```

忽略错误编码

```python
# -*-coding:utf-8-*-


s = u'中文'
print type(s)

s = s.encode('gbk')
# decode("编码"默认:strict抛出异常)
# ignore: 忽略 非法字符
# replace:用?取代非法字符
# xmlcharrefreplace: 则使用XML的字符引用
s.decode('gbk', 'ignore').encode('utf-8')
print type(s)
```



深入阅读:

<https://www.jianshu.com/p/5682a0e0a9ba>

<https://www.cnblogs.com/jinhaolin/p/5128973.html>

python3

Str\<—\> Bytes

```python
s = '字符串'

s = s.encode()
print(type(s),s)
```

Bytes \<—\> Str

```python
s = '字符串'
s = s.encode()
print(type(s),s)

s = s.decode()
print(type(s),s)
```

总结:

py2和py3在编码最大的区别是py2默认的编码方式是Unicode而py3则是UTF-8.所以当我们在py2中想要将一个字符串转换成另一种编码,首先要将这个字符串decode解码成Unicode之后再eccode编码成指定类型.而在py3中默认是UTF-8编码,所以我们想将字符串转换成bytes类型,不再是解码而是直接编码成bytes,反之想将bytes转换成utf-8则需要decode解码.

深度阅读:<https://foofish.net/how-python3-handle-charset-encoding.html>

### 求长:

```python
s = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ'
T = len(s)
print(T)  # >>> 26
```

### 截取(切片):

```python
s = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ'
T = s[3:6]
print(T)  # >>> DEF
```

### 查找子串:

```python
# find() 查到返回索引,否则返回-f
s = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ'
T = s.find('EFG')
print(T)  # >>> 4

# index() 查到返回索引,否则抛出异常
s = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ'
T = s.index('2')
print(T)  # >>> ValueError: substring not found
```

### 拼接:

```python
s1 = 'ABCDEFGHIJKLMN'
s2 = 'OPQRSTUVWXYZ'
T = ','.join(s1+s2)
print(T)    # >>> A,B,C,D,E,F,G,H,I,J,K,L,M,N,O,P,Q,R,S,T,U,V,W,X,Y,Z
```

### 替换:

```python
s1 = 'A,B,C,D,E,F,G,H,I,J,K,L,M,N,O,P,Q,R,S,T,U,V,W,X,Y,Z'
T = s1.replace('D,E,F,G,H', 'd,e,f,g,h')
print(T)  # >>> A,B,C,d,e,f,g,h,I,J,K,L,M,N,O,P,Q,R,S,T,U,V,W,X,Y,Z
```

大小写转换:

```python
s1 = 'ABc dEf'
print(s1.upper())          # 把所有字符中的小写字母转换成大写字母
print(s1.lower())          # 把所有字符中的大写字母转换成小写字母
print(s1.capitalize())     # 把第一个字母转化为大写字母，其余小写
print(s1.title())          # 把每个单词的第一个字母转化为大写，其余小写

'''
>>>
ABC DEF
abc def
Abc def
Abc Def
'''
```

### 去空:

```python
s1 = '  ABc dEf  '

T = s1.strip()  # 把头和尾的空格去掉
print(T)
T = s1.lstrip()  # 把左边的空格去掉
print(T)
T = s1.rstrip()  # 把右边的空格去掉
print(T)

# 把所有的空个去掉
T = s1.replace(' ','')
print(T)
```

### 分割:

```python
s1 = 'A,B,C,d,e,f,g,h,I,J,K,L,M,N,O,P,Q,R,S,T,U,V,W,X,Y,Z'
T = s1.split(',', 3)
print(T)  # >>> ['A', 'B', 'C', 'd,e,f,g,h,I,J,K,L,M,N,O,P,Q,R,S,T,U,V,W,X,Y,Z']
```

### 正则表达式:



数字型
---

### 整形:

整型(Int) - 通常被称为是整型或整数，是正或负整数，不带小数点

```python
a = 10
```

### 长整型:

长整型(long integers) - 无限大小的整数，整数最后是一个大写或小写的L

注:long长整型旨在python2中出现,python3统一为int型

```python
a = 10L
print(a)
print(type(a))

# >>> 10
# >>> <type 'long'>
```

### 浮点型:

浮点型(floating point real values) - 浮点型由整数部分与小数部分组成，浮点型也可以使用科学计数法表示（2.5e2 = 2.5 x 102 = 250）

```python
a = 3.1415926
print(a)

# >>> 3.1415926
```

### 复数:

复数(complex numbers) - 复数由实数部分和虚数部分构成，可以用a + bj,或者complex(a,b)表示， 复数的实部a和虚部b都

列表
--

### 增:

```python
li = ['a', 'b', 12, 3.12, 'ab']

# 增
li.append(3, 'add')
print(li)
```

### 删:

```python
li = ['a', 'b', 12, 3.12, 'ab']

# 删
li.pop(1)
print(li)
```

### 改:

```python
li = ['a', 'b', 12, 3.12, 'ab']

# 改
li[1] = 'c'
print(li)
```

### 查:

```python
li = ['a', 'b', 12, 3.12, 'ab']

# 查
print(li)
```

### 切片:

num\_li[起始:结束-1:步长]

num = num\_li[-2:] 负数表示从列表反方向(从右往左)查找

```python
num_li = ['a', 'b', 'c', 'd', 'e', 'f']

# 切片
num = num_li[-2:]
print(num)  # ['e', 'f']
num = num_li[2:]
print(num)  # ['c', 'd', 'e', 'f']

num = num_li[:-4]
print(num)  # ['a', 'b']
num = num_li[:4]
print(num)  # ['a', 'b', 'c', 'd']

num = num_li[1:3]
print(num)  # ['b', 'c']

num = num_li[-3:-1]
print(num)  # ['d', 'e']

num = num_li[::2]
print(num)  # ['a', 'c', 'e']
num = num_li[::-2]
print(num)  # ['f', 'd', 'b']

```



### 遍历:

```python
num_li = ['a', 'b', 'c', 'd', 'e', 'f']
num_li2 = [('a', 'b'), ('c', 'd'), ('e', 'f'), ('g', 'h'), ('i', 'j')]
# 迭代
for i in num_li:
    print(i)
'''a
b
c
d
e
f
'''

for i, j in num_li2:
    print(i, j)
'''
a b
c d
e f
g h
i j
'''    

num_li = ['a', 'b', 'c', 'd', 'e', 'f']
# 角标迭代
for index, value in enumerate(num_li):
    print(index, v)
'''
0 a
1 b
2 c
3 d
4 e
5 f
'''    
```

### 常用方法:

```python
list1 = [0, 1, 2, 3, 4, 5, 5, 5,51]
list2 = [6, 7]

# 获取列表元素个数
print(len(list1)) # >>> 9
# 获取列表最大元素
print(max(list1)) # >>> 51
# 获取列表最小元素
print(min(list1)) # >>> 0

# 统计某个元素在列表中出现的次数
print(list1.count(5)) # >>> 3

# 在末尾添加另一个序列的多个值
list1.extend(list2)
print(list1) # >>> [0, 1, 2, 3, 4, 5, 5, 5, 51, 6, 7]

# 查找某个值第一个匹配项的索引位置
print(list1.index(51)) # >>> 8

# 查找某个值的第一次所在的位置并删除
list1.remove(51)
print(list1) # >>> [0, 1, 2, 3, 4, 5, 5, 5, 6, 7]

# 反向列表元素
list1.reverse()
print(list1) # >>> [7, 6, 5, 5, 5, 4, 3, 2, 1, 0]

# 对列表进行排序 reverse = True 降序， reverse = False 升序（默认)
list1.sort(reverse=False)
print(list1) # >>> [0, 1, 2, 3, 4, 5, 5, 5, 6, 7]

```

### 字典:

增:

```python
dict_1 = {'a': 1, 'b': 2, 'c': 3, 'd': 4, 'e': 5}

# 增
dict_1['f'] = 6
print(dict_1) # >>> {'a': 1, 'b': 2, 'c': 3, 'd': 4, 'e': 5, 'f': 6}
```

删:

```python
dict_1 = {'a': 1, 'b': 2, 'c': 3, 'd': 4, 'e': 5}

# 删
del dict_1['f']
print(dict_1) # >>> {'a': 1, 'b': 2, 'c': 3, 'd': 4, 'e': 5}
```

改:

```python
dict_1 = {'a': 1, 'b': 2, 'c': 3, 'd': 4, 'e': 5}

# 改
dict_1['c'] = 6
print(dict_1) # >>> {'a': 1, 'b': 2, 'c': 6, 'd': 4, 'e': 5}
```

查:

```python
dict_1 = {'a': 1, 'b': 2, 'c': 3, 'd': 4, 'e': 5}

# 查
print(dict_1['b']) # >>> 2
```

遍历:

```python
dict_1 = {'a': 1, 'b': 2, 'c': 3, 'd': 4, 'e': 5}

# 遍历

# 1）遍历key值
for key in dict_1.keys():
    print(key, '', dict_1[key])
# >>> a  1
# >>> b  2
# >>> c  3

# 2）遍历value值
for value in dict_1.values():
    print(value)
# >>> 1
# >>> 2
# >>> 3
    
# 3）遍历字典项
for kv in dict_1.items():
    print(kv)
# >>> ('a', 1)
# >>> ('b', 2)
# >>> ('c', 3)
    
# 4）遍历字典健值
for key, value in dict_1.items():
    print(key, '', value)
# >>> a  1
# >>> b  2
# >>> c  3    
```

常用方法:

```python
dict_1 = {'a': 1, 'b': 2, 'c': 3, 'd': 4, 'e': 5}

# 计算字典键的个数
len_num = len(dict_1)
print(len_num) # >>> 3

# 类型转化为字符串
str_dict = str(dict_1)
print(str_dict) # >>> {'a': 1, 'b': 2, 'c': 3}

# 返回一个字典的浅复制
dict_1.copy()

# 创建一个新字典,seq为键,value里的每个元素的集合为每个键的值
seq = ('I', 'love', 'you')
new_dict = dict.fromkeys(seq, '^_^')
print(new_dict) # >>> {'I': '^_^', 'love': '^_^', 'you': '^_^'}

# 判断键值是否在字典内 python2:dict.has_key()牙龈出血和洗牙两概念吧
key = dict_1.__contains__('a')
print(key) # >>> True

# 将字典键值转换为元祖,以列表形式返回[(key,value),(key,value),(key,value)]
items = dict_1.items()
print(items) # >>> dict_items([('a', 1), ('b', 2), ('c', 3)])

# 以列表返回字典里所有的键
key = dict_1.keys()
print(key) # >>> dict_keys(['a', 'b', 'c'])

# 以列表返回字典里所有的值
value = dict_1.values()
print(value) # >>> dict_values([1, 2, 3])

# 把dict2字典的键值更新到dict1
dict_2 = {'d': 4, 'e': 5}
dict_1.update(dict_2)
print(dict_1) # >>> {'a': 1, 'b': 2, 'c': 3, 'd': 4, 'e': 5}

# 返回指定键的值,如果没有返回default
value = dict_1.get('a')
print(value) # >>> 1

# 返回指定键的值,如果没有则添加键值为default
key_value = dict_1.setdefault('num', None)
print(key_value) # >>> None

# 删除指定键的值(返回值为被删除的值)
item = dict_1.pop('b')
print(item) # >>> 2
print(dict_1) # >>> {'a': 1, 'c': 3, 'd': 4, 'e': 5, 'num': None}

# 随机删字典中的键的值(返回值为被删除的值)
item = dict_1.popitem()
print(item) # >>> ('num', None)
print(dict_1) # >>> {'a': 1, 'c': 3, 'd': 4, 'e': 5}

# 删除字典内所有元素
dict_1.clear()
print(dict_1) # >>> {}

```

### set

```python

```

### 元组

```python

```

### 布尔

```python

```

条件判断
----

```python

```

### if/else/elif

```python

```

### \>\<=

```python

```

### in/not in

```python

```

循环
--

```python

```

### while

```python

```

### for

```python

```

### break/continue

```python

```
















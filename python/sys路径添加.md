# 设置路径和import导入要相互配合
```python
import 同级文件
```
在导入文件时,python会从同级以及同级以上的目录开始寻找需要的文件.寻找的顺序可以通过sys.path方法获得:
```python
import sys
print(sys.path)
'''
['/Users/HenryDu/PycharmProjects/untitled', 
'/Users/HenryDu/PycharmProjects/untitled', 
'/Users/HenryDu/anaconda3/envs/learn_py/lib/python37.zip', 
'/Users/HenryDu/anaconda3/envs/learn_py/lib/python3.7', 
'/Users/HenryDu/anaconda3/envs/learn_py/lib/python3.7/lib-dynload', 
'/Users/HenryDu/anaconda3/envs/learn_py/lib/python3.7/site-packages', 
'/Applications/PyCharm.app/Contents/helpers/pycharm_matplotlib_backend']
'''
```
sys.path返回的是一个列表的数据类型,所以当我们需要导入不同目录的文件时,可以通过向sys.path列表添加路径来使python解释器找到我们需要的文件.
```python
path = './mod2'
sys.path.insert(1, path)
import hihi
hihi.sea_hi()  # >>> hi
```
以上示例为两个包导入:mod2导入进mod1
```
.
├── mod1
│   ├── __init__.py
│   └── t.py
├── mod2
│   ├── __init__.py
│   ├── __pycache__
│   │   ├── __init__.cpython-37.pyc
│   │   └── hihi.cpython-37.pyc
│   └── hihi.py
└── test.txt

```

# 设置路径和导入要相互配合
```python
import 同级文件
from 同级目录 import 同级文件
```
在导入文件时,python会从同级以及同级以上的目录开始寻找需要的文件.寻找的顺序可以通过sys.path方法获得:
```python
import sys
print(sys.path)
```